# ROS 2 square-wall follower with camera line stop (prototype)

Single ROS 2 node (`wall_follower.py`) that drives along a wall using `/scan` and stops/turns when a white or yellow line is seen in `/camera/image_raw`. Publishes `/cmd_vel`.

## What is implemented
- State machine: `approach_wall` → `align_to_wall` → `follow_wall`; `camera_mode` when a white line is detected.
- LiDAR indices (0, 90, 260–300) are read directly; **a 360-beam, 1° scan is assumed**.
- HSV thresholds detect white and yellow in the lower part of the image.

## Known limitations (not yet fixed)
- `follow_wall` computes the distance error to the wall (target 0.25 m) but does **not** yet apply a steering correction; it drives straight at constant speed.
- `turn_corner` and `tight corner` states exist in the code but are never entered.
- `latest_image`/`image_ready` are not initialised: the first LiDAR message before any image can raise `AttributeError`.
- The camera frame is decoded and displayed inside the LiDAR callback.
- No tests, launch file or package metadata; not validated on a physical robot.

## Requirements
ROS 2 (Humble or compatible), Python 3.8+, `opencv-python`, `numpy`, `cv_bridge`:
```bash
pip install opencv-python numpy
sudo apt install ros-${ROS_DISTRO}-cv-bridge
```
