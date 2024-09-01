# Robotics-Dojo-Technical-Paper-Draft
Contains all details and steps taken in the design of Robot for the Robotics Dojo 2024 competition.

# Progress
- Designing the 3D model of the robot chassis using Autodesk inventor. [View the image](https://discordapp.com/channels/1109024319046164490/1272787350056996927/1275323132995043359)
   - Creating a 3D model of the robot.
      - The .urdf file is used to describe the structure of the robot 
      - sudo apt install ros-foxy-xacro ros-foxy-joint-state-publisher-gui (to install xacro and joint state publisher gui.
      - colcon build --symlink-install (allows the package to be built automaticly after editing and needs to be run again only when a new file has been created).
      - Everytime you make a change you run ( ros2 launch your_package your_launch_file)
      - The purpose of the source command and how to use it is listed below : 
          1.Open your terminal
          2. Write the command --> gedit ~/.bashrc
            - I file will open on gedit
          3.Go to the bottom (the last line was  "source /opt/ros/your_workspace/setup.bash" ,
          4.Go under that line and write --> source [YOUR PATH]
          5.Save and exit
          Now with every new shell you open, it will source automatically launch rviz2 to visulaize your model.
             -When there's no transform in the left and right wheels, run the following:
           ``` bash
  ros2 run joint_state_publisher_gui joint_state_publisher_gui
            ```

- Installing Docker, pulling the image containing the Robot Operating System(ROS) and creating a container.Follow the steps [here](https://github.com/roboticsdojo/rdj-2024-docker/tree/v1.1.0?tab=readme-ov-file). Another option was setting up Ubuntu natively and installing ROS to your PC. 
- Use Arduino Mega microcontroller and the L298N motor driver to power a 12V DC motor, control its direction and speed using PWM (Pulse Width Modulation).
- Find the ratio of revolutions of the encoder to the motor shaft. (1:44)
- Laser cut the robot chasis by using a 2D drawing of the parts on a [PDF Drawing](https://discordapp.com/channels/1109024319046164490/1272787350056996927/1275471432641679500) and asseble the parts using screws , bolts and glue using glue gun.
- Learn how to create nodes (Publisher and Subscriber) in ROS that communicate with each other over a topic.
- Use Rplidar to scan and display a 2D image ,of its environment, in Gazebo.
- Implement PID control to two motors.
- Connect the Raspberry Pi through wifi and use the command window to program it. Install Ubuntu on an SD card and plug it to your Pi and install ROS2 in it.
  - Steps to setup your Raspberry Pi to wifi :
      1. [Install Angry IP Scanner](https://angryip.org/download/). This will allow you to find the IP Address of the Raspberry Pi when connected to your PC.
      2. Open the app and find the Raspberry Pi IP address and copy it.
      3. Run the following command on your Command Prompt
          ``` bash
         ssh pi@IP_ADDRESS
          ```
      5. You're now in the Pi and can now create and edit the files.
- Use nodes in ROS to send serial commands from Raspberry Pi to Arduino Mega which controls 2 motors in their speeds, direction mode of operation (open loop or closed loop).
- **Coming up ...** Use the RPlidar to map a room and send serial commands from the Pi to the arduino mega to control the motors accordingly. SLAM (Simultaneous Mapping ans Localization) will be implemented here.
 
