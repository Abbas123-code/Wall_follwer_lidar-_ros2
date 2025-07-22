# Wall_follwer_lidar-_ros2
# 🚀 Square Wall Follower Robot with Camera Integration  

This project implements an autonomous wall-following robot using **ROS 2** and **Python**, capable of:  

✅ Following walls based on **LiDAR data** (`/scan`)  
✅ Detecting and reacting to **white & yellow lines** using a **camera feed** (`/camera/image_raw`)  
✅ Switching between **LiDAR-based navigation** and **camera-based decision-making**  

---

## 📌 Features  

- **Wall Following:**  
  Uses LiDAR to maintain a target distance (`0.25m`) from the wall.  

- **State Machine Based Navigation:**  
  - `approach_wall` – Move towards wall until target distance  
  - `align_to_wall` – Adjust orientation to align with the wall  
  - `follow_wall` – Follow the wall while maintaining distance  
  - `turn_corner` / `tight_corner` – Execute turns when corners are detected  
  - `camera_mode` – Stop or adjust movement when white/yellow lines are detected  

- **Camera-Based Line Detection:**  
  Uses **OpenCV + CvBridge** to detect white and yellow lines based on HSV thresholds.

---

## 🖼️ System Overview  

│ Camera (OpenCV) │
│ Detects white/yellow lines │
│ ↓ │
│ Switch to "camera_mode" │



│ LiDAR (/scan) │
│ Wall following + obstacle │
│ detection via state machine │


│ ROS 2 Node │
│ Publishes cmd_vel to robot │


---

## 🛠️ Requirements  

### ✅ **Software**  
- **ROS 2 (Humble or compatible)**  
- **Python 3.8+**  
- `opencv-python`  
- `cv_bridge`  
- `numpy`  

Install required Python dependencies:  

```bash
pip install opencv-python numpy
sudo apt install ros-${ROS_DISTRO}-cv-bridge
