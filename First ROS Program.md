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
- #### package.xml: Have the dependencies of your project and your build type
## What is a Node
- ####  A node is a subpart of your application, responsible one thing
- #### A package should contain many nodes and the nodes can communicate with each other using ROS communication protocols even if the nodes are not in the same package
- #### Nodes reduce code complexity
- #### Fault Tolerance
- #### Node from different languages can communicate with each other
## Python Node - Minimal Code
- ####  you go inside the the folder with same name of your package 
- #### Code:
```python
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

def main(args=None):
	rclpy.init(args=args)
	node = Node("python_node") # Start a node with a specified name
	node.get_logger().info("Hello World") # Print in the terminal
	rclpy.spin(node) # Keep the node alive until you press ctrl+C
	rclpy.shutdown()

if __name__ == "__main__":
	main()
```
- #### How to add a script to setup.py
```python
entry_points={
	'console_scripts': [
			"py_node = my_py_pkg.first_node:main"
	],
},
```
	-py_node: The name of the executable
	-my_py_pkg: the name of your package
	-first_node: the name of the file without the extenstion
	-main: the of the function you want to run 
## Python Node - With OOP
- #### Code:
```python
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

class MyNode(Node):
	def __init__(self): # Create a class with the parent as Node
		super().__init__("py_test") # Give a name for the node
		self.get_logger().info("Hello World") # print at the termnial at startup
  
def main(args=None):
	rclpy.init(args=args)
	node = MyNode()
	rclpy.spin(node)
	rclpy.shutdown()

if __name__ == "__main__":
	main()
```
- #### A timer: is a function where it executes a certain function in a certain amount of time 
```python
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node

class MyNode(Node):
	def __init__(self):
		super().__init__("py_test")
		self.get_logger().info("Hello World")
		self.create_timer(1.0, self.timer_callback) # Creates a timer with give duration and the function to execute 

	def timer_callback(self):
		self.get_logger().info("Hello")

def main(args=None):
	rclpy.init(args=args)
	node = MyNode()
	rclpy.spin(node)
	rclpy.shutdown()

if __name__ == "__main__":
	main()
```
## C++ Node - Minimal Code
- #### You go in the `/src` folder and create your file
- #### Code
```cpp
#include "rclcpp/rclcpp.hpp"

int main(int argc, char **argv){
	rclcpp::init(argc, argv);
	auto node = std::make_shared<rclcpp::Node>("cpp_node");
	RCLCPP_INFO(node->get_logger(), "Hello ROS 2");
	rclcpp::spin(node);
	rclcpp::shutdown();
	return 0;
}
```
## C++ Node - With OOP
```cpp
1. #include "rclcpp/rclcpp.hpp"

2. class MyCustomNode : public rclcpp::Node
3. {
4. public:
5.     MyCustomNode() : Node("node_name") 
6.     {
7.     }

8. private:
9. };

10. int main(int argc, char **argv)
11. {
12.     rclcpp::init(argc, argv);
13.     auto node = std::make_shared<MyCustomNode>(); // MODIFY NAME
14.     rclcpp::spin(node);
15.     rclcpp::shutdown();
16.     return 0;
17. }
```
