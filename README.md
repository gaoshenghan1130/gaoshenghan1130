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

**Backend & Systems**: Python, Node.js/Express, SQL, REST APIs, CMake, Unity
**Tools & Practices**: Git, CI/CD, Unit Testing, Qt, OOP, Data Structures & Algorithms  
**Programming**: Python, C++, Lua, JavaScript, Java, MATLAB, Mathematica, C#, Elm  
**Robotics & Embedded**: ROS2, STM32, Arduino, Real-Time Systems, Pybind11  

## Project Portfolio

⭐️ Feel free to check out my projects and contributions!

<div style="border:1px solid #ccc; padding:10px; border-radius:5px; background:#f9f9f9;">
  <details open>
    <summary style="font-size:16px; font-weight:bold; ">Robotics and Embedded Systems</summary>
    <ul style="list-style:none; padding-left:15px;">
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
        <li>
        <details open>
            <summary>MRoboSub Team - UMich</summary>
            <ul>
                <li><a href="#teleop">Refactor Teleop Control Module</a></li>
            </ul>
        </details>
        </li>
    </ul>
    </details>
  <details open>
    <summary style="font-size:16px; font-weight:bold; ">Web(Backend) Development and Software Design</summary>
    <ul style="list-style:none; padding-left:15px;">
        <li>
        <details open>
            <summary>IEEE Student Branch - UMich</summary>
            <ul>
                <li><a href="#pointSystem">Point System for Event Participation</a></li>
            </ul>
        </details>
        </li>
        <li>
        <details open>
            <summary>Personal/Small Team Projects</summary>
            <ul>
                <li><a href="#javaMySQL">Java Based MySQL Client GUI</a></li>
                <li><a href="#odyssey">Time Wield - Time Travel Game</a></li>
                <li><a href="#afterDusk">After Dusk - 3D Unity Puzzle Game</a></li>
            </ul>
        </details>
        </li>
    </ul>
  </details>
  <details open>
    <summary style="font-size:16px; font-weight:bold; ">Embedded Systems</summary>
    <ul style="list-style:none; padding-left:15px;">
        <li>
        <details open>
            <summary>STM32 Microcontroller Applications in Unicycles</summary>
            <ul>
                <li><a href="#serialComm">Serial Communication Module</a></li>
                <li><a href="#crossIDE">Cross IDE Config&Build System</a></li>
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

**Task Stack**: C++, Python, Lua, Qt, Google Protobuf, OOP, Data Structures & Algorithms, Real Time Systems, Git, Unit Testing, Multithreading, Network Programming, UDP, CMake

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

**[MRoboSub Team - UMich](https://www.github.com/MRoboSub/mrobosub)**

**Role:** Software Developer – focusing on embedded systems and ROS2 integration

**Task Stack**: Python, ROS2, Real-Time Systems, Git, Unit Testing

- **Refactor Teleop Control Module** for improved responsiveness and reliability<a id="teleop"></a>
    - Reconstruct yaml file for parameter management: tie buttons to commands instead of commands to buttons, allowing for easier remapping and customization, reducing code size by 60%

- **Ongoing...**

### Web(Backend) Development and Software Design

**[IEEE Student Branch - UMich](https://ieee.eecs.umich.edu/)**

**Role:** Full Stack Developer – development of the branch's [official website](https://ieee.eecs.umich.edu/)

**Task Stack**: Node.js/Express, SQL, REST APIs, JavaScript, HTML/CSS, Git, CI/CD

- **Point System for Event Participation**:<a id="pointSystem"></a>
    - Backend API development using Node.js and Express
    - SQL database design for storing user points and event data
    - RESTful API endpoints for point retrieval and updates
    - Currently working on call UMich API for authentication and user data integration

**Personal/Small Team Projects**

**Role:** Full Stack Developer, Game Developer, Project Manager

**Task Stack**: Elm, Functional Programming, Git, HTML/CSS, JavaScript

- **[Java Based MySQL Client GUI](https://github.com/gaoshenghan1130/student_info)**<a id="javaMySQL"></a>
    - Developed a Java Swing application for managing MySQL databases
    - Implemented for collaborators unable to use command line tools (Intended for backend setup and management for IEEE Student Branch website)
    - Features include database connection management, query execution, and result visualization

- **[Time Wield - Time Travel Game](https://focs.ji.sjtu.edu.cn/git/SilverFOCS-24su/p2team07)**: A course team project for ENGR1000J in SJTU. The game features a unique time travel mechanic that allows players to accelerate or slow down time to solve puzzles and navigate through levels. This link is avaiable only with SJTU account, but the product can be found on [offical course website](https://focs.ji.sjtu.edu.cn/silverfocs/project/2024/p2).  Key contributions include:<a id="odyssey"></a>
    - Refactor OOP structure in Messager Engine, enabling easy addition of new message types and handlers, and connection between specific objects.
    - Rewrite logics in game engine, separating rendering collision detection and game logic collision detection, optimizing performance by 5000 times. Camera system combined with reduced collision detection area, further improving performance.

- **After Dusk - 3D Unity Puzzle Game**: A team project for a game design competition hosted by SJTU GameJam Club. Featuring a Mother and Daughter duo solving puzzles, with their actions mirroring each other. The club is no longer maintaining their website, so the link has lost. Key contributions include:<a id="afterDusk"></a>
    - Design and implement the dual moving mechanism
    - Develop puzzle mechanics and level design


### Embeded Systems

**[STM32 Microcontroller Applications in Unicycles](https://github.com/gaoshenghan1130/Unicycle)**

**Role:** Research Assistant – exploring STM32 microcontroller applications in unicycles, mentored by [Prof. Orosz](https://me.engin.umich.edu/people/faculty/gabor-orosz/).

**Task Stack**: C, Embedded Systems, Real-Time Systems, Control Systems, STM32, Serial Communication, Bluetooth, Git

- **Serial Communication Module** for real-time data transmission:<a id="serialComm"></a>
    - Convert TTL to RS485 for long-distance communication, raising voltage level to reduce noise interference, and establishing links between STM32WB55 Core Board and Client Motor
    - Debugging console with SWV (Serial Wire Viewer) for real-time monitoring and logging
    - Currently implementing Bluetooth module integration for wireless control and data transmission

- **Cross IDE Config&Build System**:<a id="crossIDE"></a>
    - Wrapped a standard STM32 project with CMake for cross-IDE compatibility (supporting STM32CubeIDE, and VSCode)
    - Able to flash and debug directly from VSCode using Cortex-Debug extension or Command Line Instructions

- **~~IMU Integration and Sensor Fusion~~** (Dumped)<a id="imuSensorFusion"></a>
    - Integrate BNO055 IMU for real-time orientation and motion data
    - Debugging for error out put for IMU data reading and calibration, finding out that tedious calibration is needed for accurate data

- **Fully Autonomous Unicycle Prototype** with self-balancing and path-following capabilities (Goal for 2025-2026)<a id="autonomousUnicycle"></a>
    - Mechanical design and assembly of the unicycle frame and components
    - Control algorithm development for self-balancing and navigation
    - Simulation and testing in a controlled environment

- **Ongoing...**

