# Procedure

This document describes how to set up and run the Autonomous Robot SLAM system.

---

## Downloads

Download the following pre-configured images from the Google Drive link provided in the README.

- Raspberry Pi OS Image
- Ubuntu VMware Image

These images already contain the required software and project workspace.

---

## Hardware Requirements

- Raspberry Pi 4
- YDLIDAR G2
- Differential Drive Robot
- Motor Driver
- MicroSD Card (32 GB or higher)
- Laptop/Desktop Computer
- Wi-Fi Network

---

## Software Requirements

- VMware Workstation
- Raspberry Pi Imager (or Balena Etcher)

---

# Raspberry Pi Setup

1. Flash the Raspberry Pi OS image to a microSD card.
2. Insert the microSD card into the Raspberry Pi.
3. Connect the LiDAR and motor controller.
4. Power on the Raspberry Pi.
5. Connect the Raspberry Pi to the same network as the Ubuntu virtual machine.

---

# Ubuntu Virtual Machine Setup

1. Install VMware Workstation.
2. Download the Ubuntu VMware image.
3. Open VMware Workstation.
4. Select **Open a Virtual Machine**.
5. Open the provided `.vmx` file.
6. Start the virtual machine.
7. Ensure the virtual machine is connected to the same network as the Raspberry Pi.

The virtual machine already includes:

- Ubuntu
- ROS 2 Humble
- RViz2
- SLAM Toolbox
- Required ROS packages
- Project workspace

No additional installation is required.

---

# Running the System

## Raspberry Pi

Open four terminals.

### Terminal 1

```bash
source ~/ros2_ws/install/setup.bash
ros2 run ydlidar_g2_node g2_node
```

### Terminal 2

```bash
source ~/ros2_ws/install/setup.bash
ros2 run motor_controller serial_bridge
```

### Terminal 3

```bash
source ~/ros2_ws/install/setup.bash
ros2 run motor_controller odometry_node
```

### Terminal 4

```bash
source ~/ros2_ws/install/setup.bash
ros2 launch motor_controller lidar_tf.launch.py
```

---

## Ubuntu Virtual Machine

Open two terminals.

### Terminal 1

```bash
source ~/ros2_ws/install/setup.bash
ros2 launch motor_controller slam.launch.py
```

### Terminal 2

```bash
source ~/ros2_ws/install/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

Drive the robot using the keyboard to generate the map.

---

# Saving the Map

```bash
ros2 run nav2_map_server map_saver_cli -f my_map
```

The following files will be generated:

- `my_map.pgm`
- `my_map.yaml`

---

# Notes

- Both systems must be connected to the same local network.
- The provided operating system images are pre-configured for this project.
- If the workspace is modified, rebuild it before running the project.

  <img width="1312" height="736" alt="🚗✨Lightning McQueen   Mater Aesthetic Cinematic Duo @theaiclip @a_rt _ verse     Lightning   Mater serving pure cinematic vibes 🎬✨ Emotional frames, Pixar energy, and wallpaper-level visuals in every shot 🚗💛 From side profiles to op" src="https://github.com/user-attachments/assets/2f0d68c2-e273-4812-991e-ee0cbf68df78" />

