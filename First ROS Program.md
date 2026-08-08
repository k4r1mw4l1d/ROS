## What is a workspace?
- #### A workspace is where you write and compile your ROS packages and code
- #### Basic commands:
```bash
	karims@karims:~/Desktop/ros_ws$ mkdir ros_ws
	karims@karims:~/Desktop/ros_ws$ mkdir src
	karims@karims:~/Desktop/ros_ws$ colcon build
	karims@karims:~/Desktop/ros_ws$ source install/setup.bash
```

## Create a Python Package
- #### A package allows you to separate your code into reusable blocks
- #### Commands:
```bash
karims@karims:~/Desktop/ros_ws/src$ ros2 pkg create my_py_pkg --build-type ament_python --dependencies rclpy
```
- #### package.xml: Have the dependencies of your project and your build type
## Create a C++ Package
- #### Commands:
```bash
karims@karims:~/Desktop/ros_ws/src$ ros2 pkg create my_cpp_pkg --build-type ament_cmake --dependencies rclcpp
```
