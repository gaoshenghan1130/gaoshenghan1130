# Hi, I'm Gao Shenghan

## About Me

- **Degree**: Undergraduate ECE [@ SJTU](https://www.sjtu.edu.cn/) & ME [@ UMich](https://www.umich.edu/)
- **Team Membership**: SJTU SRC Team (RoboCup SSL), UMich MRoboSub Team, UMich IEEE Student Branch  
- **Focus Areas**: Software architecture, robotics logic, embedded systems, web development  
- **Current Research**: STM32 microcontroller applications in Unicycles  
- **Looking For**: Summer 2026 internship opportunities


## Skills

**Backend & Systems**: Python, Node.js/Express, SQL, REST APIs, CMake  
**Tools & Practices**: Git, CI/CD, Unit Testing, Qt, OOP, Data Structures & Algorithms  
**Programming**: C++, Lua, JavaScript, Java, MATLAB, Mathematica, C#  
**Robotics & Embedded**: ROS2, STM32, Arduino, Real-Time Systems, Pybind11  

---

## Project Lists

### Robotics & Embedded Systems
**[RoboCup SSL Team - SJTU SRC (2023-2024)](https://github.com/sjtu-src/Falcon2023)**

**Role:** Software Team Leader – overseeing full software architecture and integration
- Determine software architecture and module division
- Decide on orientation of softw
- Lead final code review and debugging  
- Ensure system reliability and maintainability

**Task Stack**: C++, Python, Lua, Qt, Google Protobuf, OOP, Data Structures & Algorithms, Git, Unit Testing

A comprehensive overhaul of the software architecture for the RoboCup Small Size League team at SJTU, featuring recursive skill structures and two levels of FSM (Finite State Machine). Key contributions include:

- **UDP Python Server** for using Python libraries in a C++ codebase:
    - Multiprocessing architecture to handle client connections across threads and overcome GIL limitations for maximum performance
    - Asynchronous I/O for Python module communication (using `asyncio`)
    - RRCC (Request–Response–Confirm–ConfirmContinue) protocol for reliable communication; see [PyModule Protobuf Definition and RRCC](./PyModule/PYM_Protobuf&RRCC_Eng.md) (original Chinese version [here](./PyModule/PYM_Protobuf&RRCC.md))
    - Qt signal-slot wrapper for asynchronous communication on the C++ side
    - QThread wrapper for singleton thread pool management with direct return values from thread calls using hashed name-mapping, protected by mutex
    - Unit testing for each module to ensure reliability and correctness

- **Best Advancer Matcher Algorithm**:
    - Accounts for dynamic positions of robots and the ball
    - Solves a quartic equation (fourth-degree polynomial) using Ferrari's method in O(1) time complexity for best advancer selection
    - Achieved a 20% improvement in successful pass rate based on past failure logs

- **Chip Location Prediction with a Single Camera**:
    - Kalman filter for ball state estimation and prediction
    - Parabolic trajectory approximation using the least squares method (utilizing the Python server module above)
    - ±0.3 m accuracy in chip location prediction near the field boundaries; less accurate directly under the camera due to limited information, but sufficient for most field positions


**[RoboCup SSL Team - SJTU SRC (2025)](https://github.com/sjtu-src/Falcon2026)**

A next-generation software architecture for the RoboCup Small Size League team at SJTU, designed to enhance motion control, **REPLACEING LUA WITH PYTHON**, and improve overall system robustness. Key contributions include:


- Portation from Linux to Windows(Not using WSL, but rewriting CMakeLists.txt and codebase for Windows compatibility)
  - Reconfigure some of third party libraries for Windows compatibility and modern CMake usage and toolchains

- Modular Motion Test System Framework for new member D* Argorithm training and testing
  - CRTP(Curiously Recurring Template Pattern) based design for compile-time polymorphism, reducing runtime overhead, maintaining shorter and more readable code
  - Debug Engine based Vim-like UI for real-time parameter tuning and visualization
  - Unit Testing for motion algorithms to ensure reliability and correctness


### Some project may be on private repo



- [Odyssey - Time Travel Game](https://focs.ji.sjtu.edu.cn/git/SilverFOCS-24su/p2team07), *Require SJTU account to access*
A time travel game developed using Elm, a functional programming language for front-end web development. The game features a unique time travel mechanic that allows players to accelerate or slow down time to solve puzzles and navigate through levels.

## Contact
- Email: shenghan@umich.edu
- [LinkedIn](https://www.linkedin.com/in/your-link)  
- Personal Website (coming soon 🚧)

---
⭐️ Feel free to check out my projects and contributions!