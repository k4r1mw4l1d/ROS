## What is a ROS2 Topic
- #### A topic is a place where a publisher node publishes data and a subscriber node recieves data from
## Python Publisher
- #### Code:
```python
#!/usr/bin/env python3

import rclpy
from rclpy.node import Node
from example_interfaces.msg import String

class RobotNewsStationNode(Node):
	def __init__(self):
		super().__init__("robot_news_station")
		self.publisher_ = self.create_publisher(String, "robot_news", 10)
		self.timer_ = self.create_timer(0.5, self.publish_news)
		self.get_logger().info("Robot New has been installed")
	
	def publish_news(self):
		msg = String()
		msg.data = "Hello"
		self.publisher_.publish(msg)

def main(args=None):
	rclpy.init(args=args)
	node = RobotNewsStationNode()
	rclpy.spin(node)
	rclpy.shutdown()

if __name__ == "__main__":
	main()
```
## Python Subscriber
- #### Code:
```python
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node
from example_interfaces.msg import String

class MyNode(Node):
	def __init__(self):
		super().__init__("smartphone")
		self.subsriber_ = self.create_subscription(
		String, "robot_news", self.callback_robot_news, 10)
	
	def callback_robot_news(self, msg: String):
		self.get_logger().info(msg.data)
  
def main(args=None):
	rclpy.init(args=args)
	node = MyNode()
	rclpy.spin(node)
	rclpy.shutdown()

if __name__ == "__main__":
	main()
```
## Node Commands In ROS2
- #### `ros2 topic info` Provides information about the topic in the current systems
- #### `ros2 topic echo /topic_name` Subscribe to the topic and print is the published to the topic
- #### `ros2 topic hz /topic_name` print the average rate of publication
## Rename A Topic at RunTime
- #### `ros2 run my_py_pkg robot_news --ros-args -r robot_news:=abc` to rename the topic name
- #### `ros2 run my_py_pkg smartphone --ros-args -r robot_news:=abc` to rename the topic name