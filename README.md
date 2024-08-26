# spaceros_gz_demos



https://github.com/user-attachments/assets/b5a11627-e0f3-451b-af0c-b0e76b30fb04



This is a ROS 2 package demonstrating how to use Gazebo for robotic simulations in the Space ROS environment. The simulated worlds include a submersible robot on Enceladus, the Perseverance rover and Ingenuity helicopter on Mars, a space capsule docking to the ISS, and two rovers on the Moon. Gravity of each world is set to their actual values, and the Moon uses the Selenographic Coordinate System (SCS). Perseverance and Ingenuity models are meant to be as close to their real-life counterparts as possible.

## Docker setup

If you don't have docker, install it with `sudo apt install docker.io`. If you get a permission denied error with the Docker daemon, you will have to add yourself to the docker user group with `sudo usermod -aG docker $USER`, then run `newgrp docker`. You may have also to run `xhost +local:docker` on your first time. You will need to log out and log back in for these changes to take effect on your system.

1. Navigate to the `docker` directory

2. Build the docker image locally with

    ```./docker_build.sh```

3. Start the container with

    ```./docker_start.sh```

4. Once you have a running container, to get another shell, run 

    ```./docker_shell.sh```

## Running code in the Docker container
1. Once you are in the Docker container, run `colcon build` (you should be in the `~/spaceros/ws` directory)

2. Run `source install/setup.bash`

3. Start one of the demos with `ros2 launch spaceros_gz_demos moon.launch.xml`, `mars.launch.xml`, or `enceladus.launch.xml`

## Moon
Launch the moon demo with the following command:

```ros2 launch spaceros_gz_demos moon.launch.xml```

This world contains an X1 rover holding a truss that can be detached, an X2 rover, and a solar panel with one controllable joint on a lunar environment.
Images, camera info, laser scans, point clouds, and odometry topics are provided for each robot.
Additionally, each rover can be commanded as a differential drive system via a commanded base twist.

| Topic Name | Topic Type | Description | 
| ---------- | ---------- | ----------- |
| /X1/camera_front/camera_info | sensor_msgs/msg/CameraInfo | Camera info for X1's front camera | 
| /X1/camera_front/image | sensor_msgs/msg/Image | Image on X1's front camera | 
| /X1/cmd_vel | geometry_msgs/msg/Twist | Used to command the X1 | 
| /X1/front_laser/scan | sensor_msgs/msg/LaserScan | Laser scan from the X1's camera | 
| /X1/front_laser/scan/points | sensor_msgs/msg/PointCloud2 | Point cloud from the X1's camera | 
| /X1/imu_sensor/imu | sensor_msgs/msg/Imu | IMU data from X1 | 
| /X1/odometry | nav_msgs/msg/Odometry | Base odometry topic from X1 | 
| /X1/odometry_with_covariance | nav_msgs/msg/Odometry | Odometry with covariance from X1 | 
| /X1/truss/attach | std_msgs/msg/Empty | Used to attach the truss on the back of the X1 | 
| /X1/truss/detach | std_msgs/msg/Empty | Used to detach the truss on the back of the X1 | 
| /X2/camera_front/camera_info | sensor_msgs/msg/CameraInfo | Camera info for X2's front camera | 
| /X2/camera_front/image | sensor_msgs/msg/Image | Image on X2's front camera | 
| /X2/cmd_vel | geometry_msgs/msg/Twist | Used to command the X2 | 
| /X2/front_laser/scan | sensor_msgs/msg/LaserScan | Laser scan from the X2's camera | 
| /X2/front_laser/scan/points | sensor_msgs/msg/PointCloud2 | Point cloud from the X2's camera | 
| /X2/imu_sensor/imu | sensor_msgs/msg/Imu | IMU data from X2 | 
| /X2/odometry | nav_msgs/msg/Odometry | Base odometry topic from X2 | 
| /X2/odometry_with_covariance | nav_msgs/msg/Odometry | Odometry with covariance from the X2 | 
| /solar_panel/joint | std_msgs/msg/Float64 | Used to command the joint of the solar panel | 
| /tf | tf2_msgs/msg/TFMessage | TF topic containing odometry from both the X1 and X2 | 


## Mars
Launch the mars demo with the following command:

```ros2 launch spaceros_gz_demos moon.launch.xml```

This world contains models of the Perserverance rover and the Ingenuity helicopter on a Martian surface.
The Ingenuity helicopter contains a rechargable battery that simulates it charging from its solar panel.
Ingenuity can be commanded to fly.
Perserverance can be commanded as a differential drive system, and its arm joints can also be commanded to move.
Odometry topics are also published for both robots.

| Topic Name | Topic Type | Description | 
| ---------- | ---------- | ----------- |
| /ingenuity/battery_recharge_start | std_msgs/msg/Bool | Publish `True` to start recharging the battery, and `False` to stop | 
| /ingenuity/battery_state | sensor_msgs/msg/BatteryState | Used to view the curret battery charge | 
| /ingenuity/bottom_blades/thrust | std_msgs/msg/Float64 | Command thrust to the bottom set of blades | 
| /ingenuity/top_blades/thrust | std_msgs/msg/Float64 | Command thrust to the top set of blades | 
| /ingenuity/camera | sensor_msgs/msg/Image | Image from Ingenuity's camera | 
| /ingenuity/camera_info | sensor_msgs/msg/CameraInfo | Camera info from Ingenuity's camera | 
| /ingenuity/depth_camera | sensor_msgs/msg/Image | Depth image from Ingenuity's camera | 
| /ingenuity/depth_camera/points | sensor_msgs/msg/PointCloud2 | Point cloud from Ingenuity's camera | 
| /ingenuity/odometry | nav_msgs/msg/Odometry | Odometry from Ingenuity | 
| /ingenuity/swashplate_1/joint | std_msgs/msg/Float64 | Used to tilt Ingenuity's propellers around the x axis | 
| /ingenuity/swashplate_2/joint | std_msgs/msg/Float64 | Used to tilt Ingenuity's propellers around the y axis | 
| /perseverance/arm/joint_1 | std_msgs/msg/Float64 | Command joint 1 on Perserverance's arm | 
| /perseverance/arm/joint_2 | std_msgs/msg/Float64 | Command joint 2 on Perserverance's arm | 
| /perseverance/arm/joint_3 | std_msgs/msg/Float64 | Command joint 3 on Perserverance's arm | 
| /perseverance/arm/joint_4 | std_msgs/msg/Float64 | Command joint 4 on Perserverance's arm | 
| /perseverance/arm/joint_5 | std_msgs/msg/Float64 | Command joint 5 on Perserverance's arm | 
| /perseverance/camera | sensor_msgs/msg/Image | Image from Perserverance's camera | 
| /perseverance/camera_info | sensor_msgs/msg/CameraInfo | Camera info from Perserverance's camera | 
| /perseverance/camera_yaw | std_msgs/msg/Float64 | Used to tilt Perserverance's camera around the yaw/azimuth | 
| /perseverance/cmd_vel | geometry_msgs/msg/Twist | Used to command Perserverance's base velocity | 
| /perseverance/depth_camera | sensor_msgs/msg/Image | Depth image from Perserverance's camera | 
| /perseverance/depth_camera/points | sensor_msgs/msg/PointCloud2 | Point cloud from Perserverance's camera | 
| /perseverance/odometry | nav_msgs/msg/Odometry | Odometry from Perserverance | 
| /tf | tf2_msgs/msg/TFMessage | Topic containing odometry transforms for both robots | 


## Enceladus
Launch the Enceladus demo with the following command:

```ros2 launch spaceros_gz_demos moon.launch.xml```

This world contains a submarine model in a liquid ocean meant to simulate the surface of Encaledus.

| Topic Name | Topic Type | Description | 
| ---------- | ---------- | ----------- |
| /submarine/buoyancy_engine | std_msgs/msg/Float64 | Used to determine the volume of air in the buoyancy engine, which will either lower or raise the submarine. | 
| /submarine/left_thrust | std_msgs/msg/Float64 | Control the left thruster | 
| /submarine/right_thrust | std_msgs/msg/Float64 | Control the right thruster | 
| /submarine/odometry | nav_msgs/msg/Odometry | Odometry of the submarine | 
| /submarine/sonar | sensor_msgs/msg/LaserScan | Laser scan correspoinding to sonar points | 
| /submarine/sonar/points | sensor_msgs/msg/PointCloud2 | Submarine's point cloud | 



## Orbit
Launch the orbiter demo with the following command:

```ros2 launch spaceros_gz_demos orbit.launch.xml```

This world contains a model of the International Space Station in orbit above the Earth alongside a capsule that it can try to dock at.

| Topic Name | Topic Type | Description | 
| ---------- | ---------- | ----------- |
| /capsule/lidar | sensor_msgs/msg/LaserScan | Laser scan from capsule | 
| /capsule/lidar/points | sensor_msgs/msg/PointCloud2 | Point cloud from capsule | 
| /capsule/thrust/pitch | std_msgs/msg/Float64 | Control the pitch of the capsule | 
| /capsule/thrust/push | std_msgs/msg/Float64 | Control the push of the capsule | 
| /capsule/thrust/yaw | std_msgs/msg/Float64 | Control the yaw of the capsule | 
