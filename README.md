# Line Follower Robot

## Objective
Build a robot that autonomously follows a black line using infrared (IR) sensors.

---

## Components

- **Arduino Microcontroller**: Acts as the brain of the robot, controlling the motors and sensors.
- **Motor Driver Module**: Interfaces between the Arduino and the motors, allowing for speed and direction control.
- **2 Gear Motors and Wheels**: Provide mobility, allowing the robot to move along the line.
- **Chassis**: A platform for mounting motors, sensors, and other components.
- **2 IR Sensors**: Detect the black line on the surface and guide the robot’s direction.
- **Battery Pack**: Supplies power to the Arduino and motors.
- **LiPo Batteries**: Lightweight batteries to power the robot.
- **Breadboard and Jumper Wires**: For wiring and connecting all components.

---

## Project Overview
The **Line Follower Robot** is a fundamental robotics project designed to demonstrate how sensors and motors work together to perform a specific task. Using two infrared sensors, the robot detects a black line on a white surface and adjusts its direction accordingly, ensuring that it stays on the line.

This project is ideal for understanding the basics of:
- Robotics
- Microcontroller programming
- Motor control
- Sensor integration

---

## Operation

- **IR Sensors**: Mounted under the chassis and pointed toward the ground. These sensors continuously detect the presence of a black line (the path). If the sensors detect white (no line), the robot moves forward; if one sensor detects the line, the robot adjusts by steering left or right.
  
- **Motor Control**: The Arduino takes input from the IR sensors and controls the motor speeds through the motor driver. The robot adjusts its movement based on sensor input:

  - **Both sensors detect white** → Move straight.
  - **Right sensor detects the black line** → Turn right.
  - **Left sensor detects the black line** → Turn left.
  - **Both sensors detect the black line** → Stop.

---

## Assembly Process

1. **Mount the Motors and Wheels**: Attach the motors to the chassis and connect the wheels.
2. **Set Up the IR Sensors**: Place the sensors under the chassis and connect them to the Arduino.
3. **Connect the Motor Driver Module**: Wire the motor driver to both the motors and the Arduino.
4. **Wiring the Circuit**: Use a breadboard and jumper wires to connect the sensors, motor driver, and battery pack to the Arduino.
5. **Power Up**: Use a LiPo battery to power the robot, ensuring that the power supply is stable.

---

## Code Explanation

The Arduino sketch for controlling the line follower robot uses two IR sensors to guide the movement. The logic is simple:

- When neither sensor detects the black line, the robot moves forward.
- When the left sensor detects the line, the robot turns left.
- When the right sensor detects the line, the robot turns right.
- If both sensors detect the line, the robot stops.

Here’s the simplified Arduino sketch:

```cpp
#define IR_SENSOR_RIGHT A1
#define IR_SENSOR_LEFT A0
#define MOTOR_SPEED 220

//Right motor
int enableRightMotor = 5;
int rightMotorPin1 = 9;
int rightMotorPin2 = 10;

//Left motor
int enableLeftMotor = 6;
int leftMotorPin1 = 11;
int leftMotorPin2 = 12;

void setup() {
  // Setting up motor pins
  pinMode(enableRightMotor, OUTPUT);
  pinMode(rightMotorPin1, OUTPUT);
  pinMode(rightMotorPin2, OUTPUT);
  
  pinMode(enableLeftMotor, OUTPUT);
  pinMode(leftMotorPin1, OUTPUT);
  pinMode(leftMotorPin2, OUTPUT);

  // Setting up IR sensor pins
  pinMode(IR_SENSOR_RIGHT, INPUT);
  pinMode(IR_SENSOR_LEFT, INPUT);

  rotateMotor(0, 0);
}

void loop() {
  int rightIRSensorValue = digitalRead(IR_SENSOR_RIGHT);
  int leftIRSensorValue = digitalRead(IR_SENSOR_LEFT);

  if (rightIRSensorValue == LOW && leftIRSensorValue == LOW) {
    rotateMotor(MOTOR_SPEED, MOTOR_SPEED);
  } else if (rightIRSensorValue == HIGH && leftIRSensorValue == LOW) {
    rotateMotor(-MOTOR_SPEED, MOTOR_SPEED);
  } else if (rightIRSensorValue == LOW && leftIRSensorValue == HIGH) {
    rotateMotor(MOTOR_SPEED, -MOTOR_SPEED);
  } else {
    rotateMotor(0, 0);
  }
}

void rotateMotor(int rightMotorSpeed, int leftMotorSpeed) {
  if (rightMotorSpeed < 0) {
    digitalWrite(rightMotorPin1, LOW);
    digitalWrite(rightMotorPin2, HIGH);
  } else if (rightMotorSpeed > 0) {
    digitalWrite(rightMotorPin1, HIGH);
    digitalWrite(rightMotorPin2, LOW);
  } else {
    digitalWrite(rightMotorPin1, LOW);
    digitalWrite(rightMotorPin2, LOW);
  }

  if (leftMotorSpeed < 0) {
    digitalWrite(leftMotorPin1, LOW);
    digitalWrite(leftMotorPin2, HIGH);
  } else if (leftMotorSpeed > 0) {
    digitalWrite(leftMotorPin1, HIGH);
    digitalWrite(leftMotorPin2, LOW);
  } else {
    digitalWrite(leftMotorPin1, LOW);
    digitalWrite(leftMotorPin2, LOW);
  }

  analogWrite(enableRightMotor, abs(rightMotorSpeed));
  analogWrite(enableLeftMotor, abs(leftMotorSpeed));
}
