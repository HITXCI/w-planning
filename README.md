# w-planning
" A Hierarchical Spatio-Temporal Trajectory Planning Framework for Autonomous Vehicles Incorporating Road Network Topology"的部分源代码
所有代码均为ROS格式功能包，包括了各个模块的主要代码以及自定义的消息。
# Environment
1.Ubuntu 20.04  
2.ROS-Noetic  
3.CUDA-11.3,pytorch 1.12.1 (only for perception)  
4.osqp and Eigen3  

**Lanelet**  
**高精地图ROS全局规划模块 lanelet**  
1.启动rviz可视化高精度地图以及全局路径规划  
```
roslaunch osmmap osmmap.launch
```
2.建图过程中串口数据转标准GPS数据格式模块 odometry_publisher  
* 全部GPS/IMU信息，发布fsd_common_msgs::comb, topic="/comb"
* 里程计信息，发布fsd_common_msg::GNSS, topic="/gnss_odom"
* IMU，发布sensor_msgs::IMU, topic="/gnss_imu"
* ROS标准GPS格式，发布sensor_msgs::NavSatFix, topic="/gnss/fix"
```
rosrun odometry_publishergnss_odom_pub
```
3.自定义msg fsd_common_msgs  
**全局路径规划plan**
* 在路网图中的A*算法
```
roslaunch plan plan_test.launch
```
* 根据xml文件绘制节点拓扑图发布为ROS的markerarray格式
```
roslaunch plan drawmap.launch
```

**绘制节点拓扑图 graph_tool**
* 根据pcd点云图或栅格地图，绘制节点拓扑图
* 启动标定程序，通过rviz 2D Pose Estimate 选定关键点，并自动给出序号
```
roslaunch graph_tool graph_tool.launch
```

**rough trajectory generation**
```
roslaunch freespace_planner astar_navi.launch
```

**back-end optimization**
```
roslaunch static_frenet static_frenet.launch
```
