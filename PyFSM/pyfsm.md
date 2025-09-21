# Python 层状态机/skill注册

---

**Author**: gsh
**Date**: 2025/7/23
**Version**: 1.0.0

---

### 说明

Python层目前主要有两个功能：

-  实现状态机分配skill集
-  将所有 skill 分配给具体的车

本文档主要介绍：
1. 如何包装skill，修改 skill 匹配方法
2. 如何创造并调用状态机

#### skill 包装和匹配

在`pybind`完成 skill 的绑定之后，即可在`Python`层的`CppPackage`中使用。但是在被状态机分配之前，需要对 skill 进行包装（参考`ZBin/PythonScripts/task_module/simpleGoto.py`）。请把包装后的文件放入`ZBin/PythonScripts/task_module/`目录下。

- Match Pos ：
    - 表示车的目标位置，在munkres算法中使用其计算代价矩阵。
    - 当直接指定为某辆车的位置时，即表示将该任务分配给该车，参考原`lua`层advance匹配。
    - 默认值为场上球位置。（不覆写setMatchPos时）

- setNumberHard:
    在初始化 + 每次任务分配时，都会调用此方法来设置车号。对应于原`Lua`层 match 时添加的括号，后文将举例说明。
    原`Lua`层的绑定方法在定义状态机某状态时定义，在`Python`层则对每类任务进行定义。作者认为这种方式更为清晰（例如对守门方法应对所有守门任务的实例绑定 0 号车，而不是在每次创建State之后在分配时定义）。

    - 普通的情况，无需覆写 `setNumberHard`方法。（原`Lua`层的中括号）
    - 直接指定车号时，覆写 `setNumberHard`方法，直接设置车号。（原`Lua`层在`Config.lua`中用字典绑定）
    ```python
    class SimpleGotoDirectlyAssign(SimpleGoto):
        @override
        def setNumHard(self):
            self.num = 0  # 直接指定车号为0
    
    ```
    - 实现在每个state绑定车号，在切换 state 时保持不变，如下：（对应于原`Lua`层的小括号绑定）
    ```python
    class SimpleGotoNumFixEachStateAssigned(SimpleGoto):
        @override
        def setNumHard(self):
            if not hasattr(self, 'num'):
                self.num = -1  # 初始状态为未绑定车号
            # else 车号会在第一次分配时设置，设置之后不再更新
    ```
    - 实现车号在分配第一次时固定为某个值，切换 state 时不变，如下：（对应于原`Lua`层的大括号绑定）
    ```python
    class SimpleGotoNumFixOnceAssigned(SimpleGoto):
        _number = -1  # 静态变量，跨 state 使用
        @override
        def setNumHard(self):
            if not hasattr(self, 'num'):
                self.num = _number  # number 会跨 state 使用（注意它对所有该skill都生效，如果同时调用同种该类skill，可能需要更复杂的逻辑避免静态变量碰撞）
            elif not self.num == -1 :
                _number = self.num # 如果已经绑定过车号，则记录绑定的车号（到下一个state时使用）
            #其余情况下setNumHard未重置每轮的车号，故可保证在每个state下固定
    ```

#### 状态机创建和调用

状态机模块位于`ZBin/PythonScripts/taskGroups_module/`目录下。状态机的创建和调用主要参考`ZBin/PythonScripts/taskGroups_module/sampleGroup.py`。后文依据此将解释如何创建状态机及调用原理等。

1. 创建状态

每个状态机由多个状态组成，每个状态对应一个技能集，在继承`State`类后即可自动进行球员任务分配。为方便管理，作者定义了`state_class`装饰器来标记状态类并实现需覆写的方法。
- `state_name`：状态名称，用于切换。
- `transfunc`：状态切换函数，返回下一个状态的`state_name`。
- `tasks`：状态下的任务列表，包含所有要执行的 skill 。

```python
@TaskGroup.state_class(
    # 状态名称，用于状态机识别和切换
    state_name="GO_FORWARD",
    # transition function, 用于状态切换
    transfunc=lambda: Global.Ball().Pos().x() > 0 and "GO_FORWARD" or "GO_BACKWARD",
    tasks=[
        # 所有要执行的任务列表
        SimpleGoto(C.CGeoPoint(1000, -500), 0, 0),
        SimpleGoto(C.CGeoPoint(1000, 500), 0, 0),
    ]
)
class GO_FORWARD:
    pass
```

2. 创建状态机

状态机的创建通过继承`TaskGroup`类来实现。同样定义装饰器`Group_states`简化状态机的创建。

Group_states装饰器参数：
- args[0]：状态机名称，暂时无具体功能，可通过.name属性获取。
- args[1:]：状态机的状态列表，必须是继承自`State`类的状态。第一个状态将作为初始状态。

```python
@TaskGroup.Group_states("SampleGroup", GO_FORWARD, GO_BACKWARD) 
class SampleGroup(TaskGroup.TaskGroup):
    """示例任务组：继承自 TaskGroup，定义具体的状态和任务"""
    pass
```

3. 调用状态机

在`Config.py`中定义了`blue`和`yellow`两个状态机实例。最终两个状态机实例将被传递给`Coaching`进行根据当前参数的分配（黄方或蓝方，是否进入正式比赛）。最终在 `selectPlaye.py` 中被`Cpp`层调用。

注：`Coaching`中的参数尚未部署完成，目前不支持具体依据黄方或蓝方执行不同脚本的功能。
