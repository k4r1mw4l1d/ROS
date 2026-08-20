## Introspect Your Nodes With ROS2 CLI
- #### You can view your node using `ros2 nodes list`
## Rename Your ROS Nodes At Startup
- #### You can rename your node to be able  to run the same node with different names using `ros2 run my_pkg py_node --ros-args -r __node:=abc`
## Colcon
- ####  You can build all the packages using `colcon build`
- #### To build a specific package use `--packages-select` flag
- #### You can use `--symlink-install` in python packages in order not to build again and again
## RQT & RGT_Graph
- #### Used in inspecting nodes and the relationship between each node