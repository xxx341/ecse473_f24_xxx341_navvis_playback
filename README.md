# Navvis Playback Package

This project focuses on replaying ROS bag files and visualizing sensor data and the robot's movement on a map using RVIZ. The lab includes configuring transforms, ensuring proper frame connections, and analyzing sensor data such as **`LaserScan`** and **`TF`**.

---

## Directory Structure
navvis_playback/
├── config/
│   └── config.rviz	# Asaved configuration for RVIZ
├── urdf/
│   └── navvis_bag_playback.urdf
├── launch/		# Launch files for RViz and Gazebo
│   ├── bag.launch
│   └── navvis_playback.launch
└── README.md

---

## Installation

### Prerequisites
Ensure that you have the following installed:
- **ROS Noetic** or another compatible ROS version.
- Required ROS packages:
  ```bash
  sudo apt install ros-noetic-map-server ros-noetic-tf2-ros ros-noetic-rviz
  ```

### Clone and Build
1. Clone this repository into your ROS workspace:
   ```bash
   cd ~/catkin_ws/src
   git clone <repository_url>
2. Build the workspace:
   ```bash
   cd ~/catkin_ws
   catkin_make
3. Source the workspace:
   ```bash
   source ~/catkin_ws/devel/setup.bash
   
### Files and Configuration
- Launch Files:
  - **`navvis_playback.launch`**: Main launch file for visualization.
  - **`bag.launch`**: For replaying ROS bag files.
- RVIZ Configuration:
  - **`config/config.rviz`**: Customized RVIZ settings for displaying sensor data.
- URDF/XACRO:
  - **`navvis_bag_playback.xacro`**: Robot description file for visualizing the robot model.
  
---
 
## Usage

1. Launching RVIZ
   To visualize the robot and sensor data, run:
   ```bash
   roslaunch navvis_playback navvis_playback.launch
   ```
2. Playing ROS Bag Files
   To play the ROS bag file:
   ```bash
   roslaunch navvis_playback bag.launch use_bag_gui:=false
   ```
3. Viewing the Map
   Add a **`Map`** display in RVIZ and set the topic to **`/map`**. Ensure the **Global Fixed Frame** is set to map.
4. Visualizing Sensor Data
   - LaserScan: Add **`LaserScan`** displays for:
     - **`/laser_vert_bottom/scan`**
     - **`/laser_vert_top_left/scan`**
     - **`/laser_vert_top_right/scan`**
   - **TF Frames**: Add a **`TF`** display to inspect the frame hierarchy.

5. Troubleshooting Transform Issues
   - If the robot does not move on the map, ensure the following transforms are published:
     - **`map -> odom`**
     - **`odom -> base_link`**
     - Use **`rosrun tf2_ros static_transform_publisher`** to simulate missing transforms.

---

## Example Visualization
In RVIZ:
  - The robot model appears on the map, moving as the ROS bag plays.
  - LaserScan points align with obstacles in the environment.
  - The TF tree is complete, showing **`map -> odom -> base_link`**.

---

## Testing
1. Verify the ROS bag topics:
   ```bash
   rostopic list
   ```
2. Inspect transform updates:
   ```bash
   rostopic echo /tf
   ```
3. Generate the TF tree:
   ```bash
   rosrun tf view_frames
   evince frames.pdf
   ```







