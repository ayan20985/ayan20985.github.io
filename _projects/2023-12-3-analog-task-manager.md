---
title: "Analog Gauge-Based Task Manager"
layout: page
image:
  thumbnail: /assets/projects/analog.png
tagg:
  #- "this project has been completed, #35835b"
  - "this project is in-progress, #D37070"
  - "this project's documentation is up to date, #35835b"
  #- "this project's documentation is almost complete, #eb9234"
---
Let's make a Analog task manager inspired that allows us to display the CPU core loads, CPU core temperatures, CPU power consumption, GPU load, GPU temperature, GPU power consumption, and memory usage.

<div class="content-container" data-bg-image="/assets/images/chevron2.png">
    This project is available as a Github Repository <a href="https://github.com/420Ayan420/analog-task-manager">here</a>.
</div>

<div class="content-container" data-bg-image="/assets/images/chevron2.png">
    Suggestions? Want to discuss a certain aspect of my work? Please contact me at ayanali20985@gmail.com, use the direct email link in the bottom of the menu on the left, or create a Github pull request.
</div>

{% raw %}
# Version v0.0
This project is in inspired by <a href="https://www.youtube.com/watch?v=4J-DTbZlJ5I">this</a>.

To complete this project we have to do the following:
1.  Software
    1.  Create a script to read all relevant readings from from WMI (windows management instrumentation)
    2.  Parse and process this data into a useful voltage value
    3.  Send this processed data to an Arduino so that it can be used to control analog gauges. Also add basic code to add color changing lights.
2.  Hardware
    1. Take this data and send it properly to the relevant gauge using the digital PWM pins on the Arduino Mega2560.
    2. Use digital I/O pins to control the RGB lights for each gauge so that it can be red/yellow/green for the status of the gauge.
    3. Add in 2 toggle switches for ON/OFF for the reading on the gauge and the backlight on the gauge.
    4. Add a variable resistor dimmer switch for each gauge backlight.
3.  Nice-to-haves
    1. Nice casing that is curved and matches the curve of your eyes just like a curved monitor does.
    2. Make it sit low so it does not cover a large portion of desk space.
    3. Make it modular so additional gauge clusters can be added without having to change the frame. Use magnets and contact connectors such as 4-pin headphone jacks to connect for power and data.
    4. Perhaps make a program/software that can easily adapt to each system and allow the user to program what each gauge does.
    5. Add a small LCD on the gauge to allow user to change the name of the purpose of each gauge easily and without fuss.

First, let us prove the feasibility of such a project through a proof of concept.

Let's first create script to take data from the WMI and print it out to console. I'm going to keep it simple and just use python as we do not need that much power. Be very careful with the installation of the clr library as we should use:
```bash
pip install pythonnet
pip install pyserial
```
```python
import clr  #IMPORTANT! pip install pythonnet, NOT pip install clr
import serial
import time

c = Computer()
c.CPUEnabled = True
c.GPUEnabled = True
c.Open()

while True:
    c.Hardware[1].Update()  # Update the hardware info
    for sensor in c.Hardware[1].Sensors:
        if sensor.SensorType == SensorType.Temperature and sensor.Value is not None:
            temperature = sensor.Value
            print("GPU Temp is:", temperature)
            ser.write(f"{temperature}\n".encode())
```
Nice! Okay now lets update this code so that it sends it across to the Arduino on COM4 and baudrate 9600.
```python
import clr  #IMPORTANT! pip install pythonnet, NOT pip install clr
import serial
import time

clr.AddReference('OpenHardwareMonitorLib')
from OpenHardwareMonitor.Hardware import Computer, SensorType

ser = serial.Serial('COM4', 9600, timeout=1)

c = Computer()
c.CPUEnabled = True
c.GPUEnabled = True
c.Open()

while True:
    c.Hardware[1].Update()  # Update the hardware info
    for sensor in c.Hardware[1].Sensors:
        if sensor.SensorType == SensorType.Temperature and sensor.Value is not None:
            temperature = sensor.Value
            print("GPU Temp is:", temperature)
            ser.write(f"{temperature}\n".encode())
```
Okay now lets write some simple code to take this GPU temp reading and turn on the onboard LED if it exceeds 51°C.
```
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  if (Serial.available() > 0) {
    float gpuTemperature = Serial.parseFloat();
    if (gpuTemperature > 51.0) {
      digitalWrite(LED_BUILTIN, HIGH);
    } else {
      digitalWrite(LED_BUILTIN, LOW);
    }
  }
}
```
See the following video for a demonstration of this code, the top LED lights up when the temperature exceed 51°C.
<iframe width="100%" height=500px src="https://www.youtube.com/embed/XGVtSRLHYPk" frameborder="0" allowfullscreen style="border-radius: 10px;"></iframe>

We have now proven it is possible to do this using the this pipeline. The structure of our software is as follows:
```
analog task manager
├── OpenHardwareMonitorLib.dll      # available through their source code.
├── OpenHardwareMonitorLib.sys      # auto-produced
├── sketch v0.0.ino                 # arduino sketch 
└── ProgramMain v0.0.py             # feasibility analysis
```

# Version v0.1
```py
import clr #IMPORTANT! pip install pythonnet, NOT pip install clr
import time 

clr.AddReference('OpenHardwareMonitorLib')

from OpenHardwareMonitor.Hardware import Computer, HardwareType, SensorType

c = Computer()
c.CPUEnabled = True  # Enable CPU Info
c.GPUEnabled = True  # Enable GPU Info (optional)
c.Open()

print("CPU Core Temperatures and Loads")
print("--------------------------------")

while True:
    for hardware_item in c.Hardware:
        if hardware_item.HardwareType == HardwareType.CPU:
            hardware_item.Update()
            temperatures = []
            loads = []

            for sensor in hardware_item.Sensors:
                if sensor.SensorType == SensorType.Temperature:
                    temperatures.append(sensor.Value)
                elif sensor.SensorType == SensorType.Load:
                    loads.append(sensor.Value)

            # Print in a tabular format
            for i in range(len(temperatures)):
                temp_str = f"{temperatures[i]:.1f}°C" if temperatures[i] is not None else "N/A"
                load_str = f"{loads[i]:.1f}%" if loads[i] is not None else "N/A"
                print(f"Core {i+1}: Temp = {temp_str}, Load = {load_str}")
            print("-" * 40)

            break  # Assuming only one CPU, break after processing it

    time.sleep(5)  # Wait for 5 seconds before the next update
```
```py
import clr  # the pythonnet module.
import serial  # for serial communication
import time  # for sleeping

clr.AddReference('OpenHardwareMonitorLib')

from OpenHardwareMonitor.Hardware import Computer, HardwareType, SensorType

# Set up serial communication with the Arduino
ser = serial.Serial('COM4', 9600, timeout=1)

c = Computer()
c.CPUEnabled = True  # Enable CPU Info
c.GPUEnabled = True  # Enable GPU Info (optional)
c.Open()

print("CPU Core Temperatures and Loads")
print("--------------------------------")

while True:
    for hardware_item in c.Hardware:
        if hardware_item.HardwareType == HardwareType.CPU:
            hardware_item.Update()
            temperatures = []
            loads = []

            for sensor in hardware_item.Sensors:
                if sensor.SensorType == SensorType.Temperature:
                    temperatures.append(sensor.Value)
                elif sensor.SensorType == SensorType.Load:
                    loads.append(sensor.Value)

            # Print and send the temperatures to the Arduino
            for i in range(len(temperatures)):
                temp_str = f"{temperatures[i]:.1f}°C" if temperatures[i] is not None else "N/A"
                load_str = f"{loads[i]:.1f}%" if loads[i] is not None else "N/A"
                print(f"Core {i+1}: Temp = {temp_str}, Load = {load_str}")

                # Send temperature reading to the Arduino
                if temperatures[i] is not None:
                    ser.write(f"{temperatures[i]:.1f}\n".encode())

            print("-" * 40)

            break  # Assuming only one CPU, break after processing it

    time.sleep(5)  # Wait for 5 seconds before the next update
```
{% endraw %}
