e## Python Service Server
- #### `create_service()`: takes the message type and the name of the service and a callback
- #### Code
```python
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node
from example_interfaces.srv import AddTwoInts

class AddTwoIntsServerNode(Node):
	def __init__(self):
		super().__init__("add_two_ints_server")
		self.server_ = self.create_service(AddTwoInts, "add_two_ints", self.callback_add_two_ints)
	
	def callback_add_two_ints(self, request: AddTwoInts.Request, response: AddTwoInts.Response):
		response.sum = request.a + request.b
		return response

  
  

def main(args=None):
	rclpy.init(args=args)
	node = AddTwoIntsServerNode()
	rclpy.spin(node)
	rclpy.shutdown()

if __name__ == "__main__":
	main()
```
## Python Client (No OOP)
- #### Code
```python
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node
from example_interfaces.srv import AddTwoInts  

def main(args=None):
	rclpy.init(args=args)
	node = Node("add_two_ints_clint_no_oop")
	client = node.create_client(AddTwoInts, "add_two_ints")
	while not client.wait_for_service(1.0):
		node.get_logger().warn("Waiting for the Server")
	
	request = AddTwoInts.Request()
	request.a = 3
	request.b = 8
	
	future = client.call_async(request)
	rclpy.spin_until_future_complete(node, future)
	respone = future.result()
	rclpy.shutdown()

if __name__ == "__main__":
	main()
```
## Python Client (OOP)