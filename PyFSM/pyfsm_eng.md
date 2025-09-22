# Python Layer State Machine / Skill Registration

---

**Author**: gsh  
**Date**: 2025/7/23  
**Version**: 1.0.0  

---

### Description

The Python layer currently has two main functions:

- Implementing state machines to assign skill sets  
- Assigning all skills to specific robots  

This document mainly introduces:  
1. How to wrap a skill and modify its matching method  
2. How to create and invoke a state machine  

---

#### Skill Wrapping and Matching

Once a skill has been bound in `pybind`, it can be used in the `CppPackage` at the Python layer.  
However, before being assigned by a state machine, the skill needs to be wrapped  
(see `ZBin/PythonScripts/task_module/simpleGoto.py` for reference).  
Place the wrapped file in the `ZBin/PythonScripts/task_module/` directory.  

- **Match Pos**:  
  - Represents the target position of the robot, used in the munkres algorithm to compute the cost matrix.  
  - When directly assigned to a robot’s position, it means this task is assigned to that robot (similar to the original `lua` layer "advance" matching).  
  - Default value is the ball’s position on the field (when `setMatchPos` is not overridden).  

- **setNumberHard**:  
  This method is called during initialization and at each task assignment to set the robot number.  
  In the original `Lua` layer, this was done by adding brackets during matching.  
  In the Python layer, it is defined per task type. The author believes this approach is clearer  
  (e.g., binding goalkeeper methods to robot 0 for all goalkeeper tasks, rather than defining it every time a State is created).  

  - Normal case: no need to override `setNumberHard` (equivalent to `Lua` square brackets).  
  - Directly assigning a robot number: override `setNumberHard` to fix the robot number (equivalent to dictionary binding in `Config.lua`).  
    ```python
    class SimpleGotoDirectlyAssign(SimpleGoto):
        @override
        def setNumHard(self):
            self.num = 0  # Assign robot number 0 directly
    ```
  - Fixing robot number per state (remains unchanged during state transitions, equivalent to `Lua` small parentheses binding):  
    ```python
    class SimpleGotoNumFixEachStateAssigned(SimpleGoto):
        @override
        def setNumHard(self):
            if not hasattr(self, 'num'):
                self.num = -1  # Initial state: unassigned
            # Once assigned, the number will not update again
    ```
  - Fixing robot number once at the first assignment (remains unchanged across state transitions, equivalent to `Lua` curly braces binding):  
    ```python
    class SimpleGotoNumFixOnceAssigned(SimpleGoto):
        _number = -1  # Static variable, shared across states
        @override
        def setNumHard(self):
            if not hasattr(self, 'num'):
                self.num = _number  
            elif not self.num == -1:
                _number = self.num  # Record assigned number for later states
            # Robot number is not reset each round, ensuring it stays fixed
    ```

---

#### Creating and Invoking a State Machine

The state machine module is located in `ZBin/PythonScripts/taskGroups_module/`.  
Its creation and invocation mainly reference `ZBin/PythonScripts/taskGroups_module/sampleGroup.py`.  

1. **Creating a State**

A state machine consists of multiple states.  
Each state corresponds to a skill set and, by inheriting from the `State` class,  
automatically handles task assignment.  
To simplify management, the author defined the `state_class` decorator to mark state classes  
and implement required overrides.

- `state_name`: State name, used for switching.  
- `transfunc`: Transition function, returns the next state’s `state_name`.  
- `tasks`: List of tasks (skills) executed in this state.  

```python
@TaskGroup.state_class(
    state_name="GO_FORWARD",
    transfunc=lambda: Global.Ball().Pos().x() > 0 and "GO_FORWARD" or "GO_BACKWARD",
    tasks=[
        SimpleGoto(C.CGeoPoint(1000, -500), 0, 0),
        SimpleGoto(C.CGeoPoint(1000, 500), 0, 0),
    ]
)
class GO_FORWARD:
    pass
```

2. **Creating a State Machine**

A state machine is created by inheriting from the `TaskGroup` class.  
To simplify the process, the `Group_states` decorator is provided.

- `args[0]`: The state machine name. (Currently, it has no specific functionality but can be accessed via the `.name` property.)  
- `args[1:]`: The list of states, each of which must inherit from the `State` class.  
  The first state in the list will be used as the initial state.  

```python
@TaskGroup.Group_states("SampleGroup", GO_FORWARD, GO_BACKWARD) 
class SampleGroup(TaskGroup.TaskGroup):
    """Example task group: inherits from TaskGroup and defines concrete states and tasks"""
    pass
```

3. **Invoking a State Machine**

In `Config.py`, two state machine instances, `blue` and `yellow`, are defined.  
These two instances are then passed to the `Coaching` module, which assigns tasks based on current parameters  
(e.g., whether the team is on the yellow or blue side, and whether the match is official).  

Finally, in `selectPlaye.py`, the state machine instances are called from the `Cpp` layer.  

> Note: The parameters in `Coaching` have not yet been fully implemented.  
> Currently, it does not support running different scripts depending on the yellow or blue side.  