# Robotics Dojo Technical Paper Draft

Contains all details and steps taken in the design of the robot for the Robotics Dojo 2024 competition.

## Progress

### 1. Design & Modeling
- **Chassis Design:** Designing the 3D model of the robot chassis using Autodesk Inventor. [View the image](https://discordapp.com/channels/1109024319046164490/1272787350056996927/1275323132995043359).

### 2. Environment Setup
- **Option 1: Docker Setup:** Installing Docker, pulling the image containing the Robot Operating System (ROS), and creating a container. Follow the steps [here](https://github.com/roboticsdojo/rdj-2024-docker/tree/v1.1.0?tab=readme-ov-file).
- **Option 2: Native Setup:** Installing ROS on Ubuntu natively.

### 3. Robot Model Creation in ROS
- Created a 3D model of the robot in ROS using `.urdf` and `.xacro` files.
  
- **Packages Installed:**
  ```bash
  sudo apt install ros-foxy-xacro ros-foxy-joint-state-publisher-gui
  ```

- Building the Package:

   ``` bash
      colcon build --symlink-install
   ```

- Launching the Model:

``` bash
ros2 launch your_package your_launch_file
```

- Source Command Setup:

    - Open your terminal and run:

   ``` bash

    gedit ~/.bashrc
   ```
    - Add source [YOUR PATH] below the line that sources ROS.
    - Save and exit. Now, with every new shell you open, it will source automatically.

- Joint State Publisher GUI:

``` bash
    ros2 run joint_state_publisher_gui joint_state_publisher_gui
```
### 4. Simulate the Robot with Gazebo

  - Launch Robot State Publisher in Sim Mode:

   ``` bash
      ros2 launch your_package your_launch_file use_sim_time:=true
   ```
   -  Check if it worked by running:

``` bash
ros2 param get /robot_state_publisher use_sim_time
```
- Install and Launch Gazebo:

``` bash
sudo apt install ros-foxy-gazebo-ros-pkgs
ros2 launch gazebo_ros gazebo.launch.py
```
- Spawn Robot in Gazebo:
``` bash
ros2 run gazebo_ros spawn_entity.py -topic topic_name -entity your_bot_name
```
- Add Gazebo References to .xacro Files:

    - Add the <gazebo> tag around parts' descriptions to define properties such as color and friction.

    - Use Keyboard for Teleoperation:

``` bash
    ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
### 5. Hardware Control with Arduino Mega

  - Powered a 12V DC motor using an Arduino Mega and L298N motor driver.

  - Controlled motor speed and direction using PWM (Pulse Width Modulation).

  - Encoder Ratio: 1:44 (Revolutions of encoder to motor shaft).
    
  - use the code fiom `github.com/joshnewans/ros_arduino_bridge`
    ``` bash
    sudo apt install python3-serial
    ```
  - Send Serial Commands
    ``` bash
      miniterm -e /dev/ttyUSB0 57600
    ```
  - Equation relating encoder counts to revolutions of motor shaft: (counts/sec)*1/(counts/rev)=(rev/sec).
    
    ``` bash
    git clone https://github.com/joshnewans/serial_motor_demo.git
     ```
  - Tell the Pi to listen on a topic for motor speeds and send it to the Arduino.
    ``` bash
    ros2 run serial_motor_demo driver --ros-args -p serial_port:=/dev/ttyUSB0 -p baud rate:=57600 -p loop_rate:=30 -p encoder_cpr:=3450
    ```
  - Control the motor speeds through a gui
    ``` bash
      ros2 run serial_motor demo_gui 
    ```

### 6. Physical Assembly

   - Laser cut the chassis using a 2D drawing PDF Drawing.
   - Assembled parts using screws, bolts, and a glue gun.

### 7. ROS Communication

  - Created nodes (Publisher and Subscriber) in ROS that communicate over a topic.

### 8. Mapping & Control with RPLidar

   - Used RPLidar to scan and display a 2D image of the environment in Gazebo.
   - Implemented PID control for two motors.

### 9. Raspberry Pi Setup

  - Installed Ubuntu on an SD card and inserted it into the Raspberry Pi.

  - Connected the Raspberry Pi through Wi-Fi and used SSH to access it.

  - Steps to Setup Wi-Fi Connection:
      - Install Angry IP Scanner.
      - Use Angry IP Scanner to find the Raspberry Pi's IP address.
      - Connect via SSH:

     ``` bash

      ssh pi@IP_ADDRESS
     ```

### 10. Serial Communication with Arduino Mega
  - Used nodes in ROS to send serial commands from Raspberry Pi to Arduino Mega to control motor speed, direction, and mode of operation (open loop or closed loop).

**Coming Up ...**  SLAM Implementation: Use the RPLidar to map a room and send serial commands from the Pi to the Arduino Mega to control the motors accordingly.


