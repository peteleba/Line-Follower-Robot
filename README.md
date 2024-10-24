Project Title: Line Follower Robot

Objective:
Build a robot that autonomously follows a black line using infrared (IR) sensors.

Components:

Arduino Microcontroller: Acts as the brain of the robot, controlling the motors and sensors.
Motor Driver Module: Interfaces between the Arduino and the motors, allowing for speed and direction control.
2 Gear Motors and Wheels: Provide mobility, allowing the robot to move along the line.
Chassis: A platform for mounting motors, sensors, and other components.
2 IR Sensors: Detect the black line on the surface and guide the robot’s direction.
Battery Pack: Supplies power to the Arduino and motors.
LiPo Batteries: Lightweight batteries to power the robot.
Breadboard and Jumper Wires: For wiring and connecting all components.
Project Overview:
The Line Follower Robot is a fundamental robotics project designed to demonstrate how sensors and motors work together to perform a specific task. Using two infrared sensors, the robot detects a black line on a white surface and adjusts its direction accordingly, ensuring that it stays on the line.

This project is ideal for understanding the basics of robotics, microcontroller programming, motor control, and sensor integration.

Operation:
IR Sensors: These are mounted under the chassis and pointed towards the ground. They continuously detect the presence of a black line (the path). If the sensors detect white (no line), the robot moves forward; if one sensor detects the line, the robot adjusts by steering left or right.

Motor Control: The Arduino takes input from the IR sensors and controls the motor speeds through the motor driver. The robot adjusts its movement by rotating the motors accordingly:

Both sensors detect the white surface → Move straight.
Right sensor detects the line → Turn right.
Left sensor detects the line → Turn left.
Both sensors detect the line → Stop.
Assembly Process:
Mount the Motors and Wheels: Attach the motors to the chassis and connect the wheels.
Set Up the IR Sensors: Place the sensors under the chassis and connect them to the Arduino.
Connect the Motor Driver Module: Wire the motor driver to both the motors and the Arduino.
Wiring the Circuit: Use a breadboard and jumper wires to connect the sensors, motor driver, and battery pack to the Arduino.
Power Up: Use a LiPo battery to power the robot, ensuring that the power supply is stable.
Code Explanation:
The Arduino sketch for controlling the line follower robot uses two IR sensors to guide the movement. The logic is simple:

When neither sensor detects the black line, the robot moves forward.
When the left sensor detects the line, the robot turns left.
When the right sensor detects the line, the robot turns right.
If both sensors detect the line, the robot stops.
