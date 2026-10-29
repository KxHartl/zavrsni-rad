# Path planning of a mobile robot with an indoor GPS system

**Planiranje putanje mobilnog robota unutarnjim GPS sustavom**

> Bachelor's thesis, BSc in Mechatronics and Robotics (Mehatronika i robotika), FSB, University of Zagreb, 2024. Mentor: M. Crneković

![ROS 2](https://img.shields.io/badge/ROS%202-22314E?logo=ros&logoColor=white)
![Python](https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white)
![Marvelmind](https://img.shields.io/badge/positioning-Marvelmind%20Indoor%20GPS-1F6FB2)
![RViz](https://img.shields.io/badge/viz-RViz2-22314E)

Code for the bachelor's thesis. A mobile robot is located with the Marvelmind indoor GPS system,
and a path to a goal is planned and followed with the artificial potential field method. The goal
attracts the robot, obstacles repel it, and the field and the planned path are shown in RViz.

## What's inside

The ROS 2 package `src/planiranje_putanje`:

| Node | What it does |
|---|---|
| `hedgehog_to_pose` | Turns the Marvelmind hedgehog position and angle into a pose (`/marvelmind_pose`) and a TF frame, and publishes each stationary beacon as a TF frame. |
| `odom_to_tf` | Publishes the robot's odometry as a TF frame. |
| `prikaz_polja` | Computes the potential field over the workspace and publishes it with the planned path and the goal for RViz. |
| `navigacija_mpp` | Potential field navigation: takes a goal from `/goal_pose`, plans the path and drives the robot through `/cmd_vel`. |

`pose_to_center.py` shifts the OptiTrack and Marvelmind poses to the robot's centre so the two can
be compared. It is not registered as a node in `setup.py`.

## How to run

The launch file needs the `marvelmind_ros2` driver and the robot description package `astro`,
which are not part of this repository.

```bash
colcon build
source install/setup.bash
ros2 launch planiranje_putanje planiranje_putanje.launch.py   # Marvelmind, robot model, pose and TF nodes, RViz
ros2 run planiranje_putanje navigacija_mpp                     # potential field navigation
```

Set the goal with *2D Goal Pose* in RViz.
