# blynk-device-control
This project demonstrates how to control electrical devices remotely using a NodeMCU ESP8266 microcontroller and the Blynk IoT platform.

Project Overview
The system allows a user to turn four separate devices on and off from anywhere using a smartphone app or a web dashboard. It uses a NodeMCU to bridge the gap between the Blynk cloud service and a 4-channel relay module connected to the devices.

Core Components
The following hardware and software are required for this project:

Hardware

NodeMCU ESP8266 board 

4-Channel Relay Module 

Electrical devices (e.g., light bulbs and holders) 

Jumper wires 

USB to Micro-USB cable 

Software & Services


Arduino IDE: Used to program the NodeMCU.


Blynk Library: Needs to be installed in the Arduino IDE.


ESP8266 Board Manager: For Arduino IDE to recognize the NodeMCU.


Blynk IoT Cloud: A web server for creating and managing the project.


Blynk IoT App: A mobile application for controlling the devices.

System Architecture and Functionality
The project is built around the NodeMCU, which acts as the central controller connecting the physical hardware to the cloud.

Hardware Setup
The connections are laid out in the block diagram:

The NodeMCU's digital pins D1, D2, D5, and D6 are connected to the input pins (IN1, IN2, IN3, IN4) of the 4-channel relay module .

The relay module's output terminals are connected to four separate bulb holders, which act as the controllable devices.

Software and Logic
The system's logic is defined in the Arduino code and configured in the Blynk platform:


Blynk Configuration: In the Blynk IoT Cloud, four virtual pin datastreams (V1, V2, V3, V4) are created as integers with a range of 0 to 1 . These datastreams are then linked to switch widgets on both the web and mobile dashboards.

Arduino Code:

The code includes the Blynk and ESP8266 WiFi libraries and defines the credentials for the Blynk project and the Wi-Fi network .

The 

setup() function initializes serial communication, sets the relay pins as outputs, connects to Wi-Fi and the Blynk server, and sets the initial state of all relays to OFF (HIGH) .

The code uses BLYNK_WRITE(Vn) functions. These are special functions that are automatically called whenever the state of a widget on the Blynk app (linked to that virtual pin) is changed.

For example, when the switch connected to virtual pin V1 is toggled in the app, the BLYNK_WRITE(V1) function is executed. It reads the incoming value (0 or 1). If the value is 0, it turns off 

relay1 (digitalWrite HIGH); if it's 1, it turns on relay1 (digitalWrite LOW) . This logic is repeated for all four virtual pins and their corresponding relays.

The 

loop() function simply contains Blynk.run(), which keeps the NodeMCU connected to the Blynk server and handles all incoming and outgoing communication .
