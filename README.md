# Dynamic Traffic Light Control System using ESP32
Overview
The dynamic traffic light control system using an ESP32 microcontroller aims to enhance urban traffic management by adapting traffic light signals based on real-time vehicle density at intersections. This project leverages the ESP32's dual-core processor and WiFi connectivity to monitor vehicle density using sensor inputs and adjust the traffic signals accordingly. The ESP32 also serves as a web server, providing a user-friendly web interface for remote monitoring and control.

# Key Components
ESP32 Microcontroller: Central unit for processing and control.

Sensors: Used for detecting vehicle density at intersections.
Web Interface: For remote monitoring and control.

WiFi Connectivity: For communication and remote access.
Objectives Optimize traffic flow by dynamically adjusting traffic light timings.

Reduce waiting time and fuel consumption.

Enable remote monitoring and control via a web interface.

# Libraries Used
WiFi.h: Handles WiFi connectivity.

WebServer.h: Manages web server functionalities.

ESPmDNS.h: Enables mDNS functionality.

ArduinoJson.h: Facilitates JSON parsing and generation.

Ticker.h: Provides timed callbacks.

# Network Configuration

const char* ssid = "OnePlus";

const char* password = "719622@Aa";

mDNS Configuration: esp32.local

# Traffic Light States
RED: Vehicles must stop.

YELLOW: Vehicles should prepare to stop.

GREEN: Vehicles can proceed.

# Key Variables
Current Post: Intersection currently being controlled.

Vehicle Counts: Number of vehicles waiting at each 
intersection.

Timers: Durations for each traffic light state.

Light Status: Current state of each traffic light.

Paused: Indicates if the system is paused.

Control Mode: Current mode of operation (time-based or density-based).

# Setup and Initialization
```
void setup() {

  Serial.begin(115200);

  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {

    delay(1000);

  }
  if (!MDNS.begin("esp32")) return;

  server.on("/", handleRoot);

  server.on("/pause", handlePause);

  server.on("/resume", handleResume);

  server.on("/density", handleDensity);

  server.on("/time", handleTime);

  server.on("/update", handleUpdate);

  server.on("/updateVehicleCount", 

handleUpdateVehicleCount);

  server.on("/events", handleEvents);

  server.begin();

  greenTicker.attach_ms(greenDuration, switchToNextPost);

} 
```
# Implementation Procedure

## Set Up Hardware:
Connect the ESP32 to your computer via USB.

Set up the Arduino IDE with ESP32 board support.

Write and Upload Code:

Write the code for traffic light control, web server, and real-time updates.

Upload the code to the ESP32 using the Arduino IDE.

Connect to WiFi:

Ensure the ESP32 connects to the specified WiFi network.
Access the web interface through the IP address or esp32.local.

Interact with Web Interface:

Use the web interface to monitor and control the traffic lights.

Adjust configurations as needed via the control menu.

Monitor and Adjust:

Monitor real-time updates.

Make adjustments to traffic light timings and vehicle counts as required.

# Additional Hardware Options
Raspberry Pi: More powerful processing capabilities.

Arduino UNO with WiFi Shield: Easier to set up for beginners.

BeagleBone Black: Robust and reliable with extensive I/O options.

# Applications

Urban Traffic Management: Optimizes traffic flow in cities.

Smart Cities: Integrates with other smart city solutions.

Emergency Response: Provides priority passage for 
emergency vehicles.

# Modifications
Vehicle Count Rate Adjustment:

Implement a slider or button in the web interface to adjust the vehicle count decrement rate.

Round Timer Element:

Design a round CSS element with transparency and hover effects to display a countdown timer.

No Post Repetition:

Modify control logic to ensure no traffic post is repeated twice in the signal sequence.

Control Menu and Performance Optimization:

Design a menu in the web interface to control variables and optimize website performance.

# Example Code for Modifications:


<div>

  <label for="decrementRate">Vehicle Count Decrement 
Rate:</label>

  <input type="range" id="decrementRate" min="100" 

max="1000" value="400" step="100" 

oninput="updateDecrementRate(this.value)">

  <span id="decrementRateValue">400 ms</span>

</div>

<style>

  .round-timer {

    border-radius: 50%;

    background: rgba(0, 0, 0, 0.5);

    color: white;

    text-align: center;

    line-height: 50px;

    width: 50px;

    height: 50px;

    transition: background 0.3s;

  }

  .round-timer:hover {

    background: rgba(0, 0, 0, 0.7);

  }

</style>
