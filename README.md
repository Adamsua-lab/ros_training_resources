Below is a list of tutorials and other resources introducing concepts, software frameworks, libraries and tools that are required for using and developing software for our robotic WAAM system. 

Prelims/tools:

- Ubuntu 16.04 or Ubuntu 18.04. (16.04 is preferred currently) installation:
  - Dual-boot installation (for example alongside MS Windows) on a second partition or
  - https://www.virtualbox.org/wiki/Downloads
- [Git/GitHub](https://try.github.io/)
- C++  
  Particularly C++ for Linux compiled with GCC. ROS has build tools (catkin etc.) that make life easy though.
- Some Linux basics--should become apparent once going through the tutorials below. It is suggested to learn about specific concepts once one is confronted with them during the tutorials.

ROS:

1. http://wiki.ros.org/ROS/Tutorials
1. http://wiki.ros.org/ROS/Tutorials/WhereNext  
  Some tutorials for sensor data visualization and robot simulation (Rviz most importantly)
1. http://wiki.ros.org/Industrial/Tutorials (just Section 2.2 General)
1. http://wiki.ros.org/Industrial/Industrial_Robot_Driver_Spec  
  The specifications that a manipulator driver must satisfy to call itself a ROS-industrial-compatible driver (for example the motoman driver package further below). This site has relevant information to understand now information about the manipulator state can be obtained and how joint trajectories can be passed to the manipulator etc.
1. https://ros-planning.github.io/moveit_tutorials (a path planning framework for ROS)
1. https://github.com/ros-industrial/industrial_core  
  Is a dependency of the "motoman" package below, so should live in the same workspace as the "motoman" package. Needs to be built from source via catkin tool. Should be the same process as explained in tutorials above. Contains hardware-agnostic core packages that provide nodes and libraries for communication with industrial robot controllers. Also contains an industrial robot (manipulator) simulator.
1. https://github.com/Adamsua-lab/motoman  
  This is our lab's fork of the package containing motoman-specific driver nodes and libraries to communicate with robot controllers (especially multi-group systems), and support packages for specific Yaskawa Motoman manipulators. Our fork contains additional support packages for the manipulator (MA2010) and positioner (Motopos D500) used at InnoTech for metal AM, a merged PR for multi-group systems and some bug fixes. All this is combined in the "devel" branch. This package (the branch "devel") needs to be built from source using the catkin tool. Instructions are in the repo.
1. http://wiki.ros.org/actionlib  
  An alternative method for submitting joint trajectories to the manipulator, similar to services specifically made for an action such as a manipulator motion with appropriate feedback. Advantages are that feedback can be obtained during execution and the result of the motion can be obtained after execution (success, failure, aborted etc.). The motoman driver and industrial core each implement action servers. This is also the used method for submitting a goal trajectory in `ros_additive_manufacturing/ram_hw_interface`.
1. https://github.com/Adamsua-lab/motoman_ma2010_d500_waam_support  
  A support package providing a kinematic model (kinematic tree) combining the MA2010 manipulator and D500 positioner
1. https://github.com/Adamsua-lab/motoman_ma2010_d500_waam_moveit_config  
  A package containing the MoveIt! configuration for the manipulator and positioner combination. MoveIt! is used for path planning and conversion from cartesian space to joint space (inverse kinematics).
1. https://github.com/Adamsua-lab/ros_additive_manufacturing  
  This is a stack and framework for large-scale additive manufacturing. The ADAMS lab fork contains an additional package (hw_interface) for trajectory planning and execution with synchronized welder commands (arcon/arcoff etc.).
