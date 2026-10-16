# NEW ROBOT

- new arms
- new legs
- torso/head gets new motors
- face stays the same (same motors, that is)
- hands stay the same (same motors, that is)
- compute only 1 jetson for everything
- look at connectivity jetson/network/wifi
- ESP32 for motor control
- eyes ESP32 with displays
- speakers
- microphone
- head camera (2d rpicam)
- chest camera (3d realsense, used for locating humans and pointing at objects)
- mobile base sensors (arduino)
- lidar (usb)
- IMU (usb)

# ESP32 MOTOR CONTROLLERS

- for maybe 2 feetech TTL chain (face and jaw)
- for CANBUS motors (motors per chain: arms: 6, head/torso: 4, maybe camera)
- CANBUS motors used: Robstride 00 and Robstride 05 (48V already, need regulator)

- ESP32 for eyes can also control the jaw

- research if ESP32 can use USB for communication

- put all low-level high frequency motion control in ESP32
- attempt to connect all chains via single RS485 bus

# MOBILE BASE CONTROLLER

- USB upstream
- sensors
- wheels
- lidar
- IMU

- maybe design board with ESP32 for this as well

# JETSON STUFF

- find touchscreen solution for jetson
