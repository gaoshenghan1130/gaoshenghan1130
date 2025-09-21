# Hi, I'm Gao Shenghan

## About Me

- **Degree Persuing**: 
    - Undergraduate ECE [@ SJTU](https://www.sjtu.edu.cn/) 
    - Undergraduate ME [@ UMich](https://www.umich.edu/)
- **Team Membership**: 
    - [SJTU SRC Team (RoboCup SSL)](https://github.com/sjtu-src)
    - [UMich MRoboSub Team](https://github.com/MRoboSub/mrobosub)
    - [UMich IEEE Student Branch](https://ieee.eecs.umich.edu/)  
- **Focus Areas**: Software Architecture, Robotics Logic, Embedded Systems, Web Development  
- **Current Research**: STM32 microcontroller applications in Unicycles  
- **Looking For**: Summer 2026 internship opportunities


## Skills

**Backend & Systems**: Python, Node.js/Express, SQL, REST APIs, CMake  
**Tools & Practices**: Git, CI/CD, Unit Testing, Qt, OOP, Data Structures & Algorithms  
**Programming**: Python, C++, Lua, JavaScript, Java, MATLAB, Mathematica, C#，Elm  
**Robotics & Embedded**: ROS2, STM32, Arduino, Real-Time Systems, Pybind11  

## Project Context

⭐️ Feel free to check out my projects and contributions!

<div style="border:1px solid #ccc; padding:10px; border-radius:5px; background:#f9f9f9;">
  <details open>
    <summary style="font-size:16px; font-weight:bold; cursor:pointer;">Robotics and Embedded Systems</summary>
    <ul>
      <li>
        <details open>
          <summary>RoboCup SSL Team - SJTU SRC (2023-2024)</summary>
  <ul>
    <li><a href="#udp_server">UDP Python Server for C++ integration</a></li>
    <li><a href="#matcher_algo">Best Advancer Matcher Algorithm</a></li>
    <li><a href="#chip_pred">Chip Location Prediction with one camera</a></li>
  </ul>
        </details>
      </li>
      <li>
        <details open>
          <summary>RoboCup SSL Team - SJTU SRC (2025)</summary>
          <ul>
            <li><a href="portationL2W">Portation from Linux to Windows-Linux Cross Platform</a></li>
            <li><a href="#pyfsm">Python Based FSM (Finite State Machine)</a></li>
            <li><a href="#modularMotionTest">Modular Motion Test System Framework</a></li>
          </ul>
        </details>
      </li>
    </ul>
  </details>
</div>

## Contact
- Email: shenghan@umich.edu
- Mobile: +1 (734) 358-6704
- [LinkedIn](https://www.linkedin.com/in/shenghan-gao-30b029383)
- WeChat Id: Gshgsh1130
- QQ: 2893409370
- Instagram: [@gaoshenghan1130](https://www.instagram.com/gaoshenghan1130/)
- Personal Website (coming soon 🚧)

---

## Project Lists

### Robotics & Embedded Systems

**[RoboCup SSL Team - SJTU SRC (2023-2024)](https://github.com/sjtu-src/Falcon2023)<a id ="src2023"></a>**

**Role:** Software Team Leader – overseeing full software architecture and integration
- Determine software architecture and module division
- Decide on orientation of softw
- Lead final code review and debugging  
- Ensure system reliability and maintainability

**Task Stack**: C++, Python, Lua, Qt, Google Protobuf, OOP, Data Structures & Algorithms, Git, Unit Testing, Multithreading, Network Programming, UDP, CMake

A comprehensive overhaul of the software architecture for the RoboCup Small Size League team at SJTU, featuring recursive skill structures and two levels of FSM (Finite State Machine). Key contributions include:

- **UDP Python Server** for using Python libraries in a C++ codebase:<a id="udp_server"></a>
    - Multiprocessing architecture to handle client connections across threads and overcome GIL limitations for maximum performance
    - Asynchronous I/O for Python module communication (using `asyncio`)
    - RRCC (Request–Response–Confirm–ConfirmContinue) protocol for reliable communication; see [PyModule Protobuf Definition and RRCC](./PyModule/PYM_Protobuf&RRCC_Eng.md) (original Chinese version [here](./PyModule/PYM_Protobuf&RRCC.md))
    - Qt signal-slot wrapper for asynchronous communication on the C++ side
    - QThread wrapper for singleton thread pool management with direct return values from thread calls using hashed name-mapping, protected by mutex
    - Unit testing for each module to ensure reliability and correctness

- **Best Advancer Matcher Algorithm**:<a id="matcher_algo"></a>
    - Accounts for dynamic positions of robots and the ball
    - Solves a quartic equation (fourth-degree polynomial) using Ferrari's method in O(1) time complexity for best advancer selection
    - Achieved a 20% improvement in successful pass rate based on past failure logs

- **Chip Location Prediction with a Single Camera**:<a id="chip_pred"></a>
    - Kalman filter for ball state estimation and prediction
    - Parabolic trajectory approximation using the least squares method (utilizing the Python server module above)
    - ±0.3 m accuracy in chip location prediction near the field boundaries; less accurate directly under the camera due to limited information, but sufficient for most field positions


**[RoboCup SSL Team - SJTU SRC (2025)](https://github.com/sjtu-src/Falcon2026)**

**Role:** Software Team Leader (same as [above](#src2023))

**Task Stack**: Python, CMake, Qt, Pybind11, OOP, Unit Testing, Finite State Machine, Data Structures & Algorithms


A next-generation software architecture for the RoboCup Small Size League team at SJTU, designed to enhance motion control, **REPLACEING LUA WITH PYTHON**, and improve overall system robustness. Key contributions include:


- **Portation from Linux to Windows-Linux Cross Platform** (Not using WSL, but rewriting CMakeLists.txt and codebase for Windows compatibility) <a id="portationL2W"></a>
  - Reconfigure some of third party libraries for Windows compatibility and modern CMake usage and toolchains, listing in my respository including a old versiono of [ODE](https://github.com/gaoshenghan1130/ODE_modernRepair) (later found better version in vcpkg),  and [vartypes](https://github.com/gaoshenghan1130/VarTypes_Robocup) (provided by the [Robocup Official](https://www.robocup.org) without a Windowsos version).
  - Rewrite CMakeLists.txt in all modules, create a top-level CMakeLists.txt to manage all submodules, enable compilation either with each module or all-in-one.
  - Optimize cmake sturcture, create function automatically to recursively add all source files in a directory to target, avoiding manual adding. Shortening code size each module from 200-400 lines to less than 100 lines.
  - Refactor config-time generation of protobuf, lua and python bindings to compile time generation, monitoring changes in proto/lua/py files and auto-regenerate corresponding cpp/h files.

- **Python Based FSM (Finite State Machine)** for better modularity and maintainability: <a id="pyfsm"></a>
    - Each skill is represented as a state in the FSM, allowing for clear transitions and encapsulation of behavior
    - Simplifies the addition of new skills and modification of existing ones without affecting the overall system

- **Modular Motion Test System Framework** for new member D* Argorithm training and testing <a id="modularMotionTest"></a>
    - Modular design allows for easy integration of new motion algorithms and testing scenarios
    - Provides a controlled environment for algorithm development and performance evaluation
  - CRTP(Curiously Recurring Template Pattern) based design for compile-time polymorphism, reducing runtime overhead, maintaining shorter and more readable code
  - Debug Engine based Vim-like UI for real-time parameter tuning and visualization
  - Unit Testing for motion algorithms to ensure reliability and correctness


### Some project may be on private repo



- [Odyssey - Time Travel Game](https://focs.ji.sjtu.edu.cn/git/SilverFOCS-24su/p2team07), *Require SJTU account to access*
A time travel game developed using Elm, a functional programming language for front-end web development. The game features a unique time travel mechanic that allows players to accelerate or slow down time to solve puzzles and navigate through levels.

