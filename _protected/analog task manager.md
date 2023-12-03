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
```powershell
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
Okay now lets write some simple code to take this GPU temp reading and turn on the onboard LED if it exceed 51°C.
```C++
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
We have now proven it is possible to do this using the this pipeline. The structure of our software is as follows:
```
analog task manager
├── OpenHardwareMonitorLib.dll      # available through their source code.
├── OpenHardwareMonitorLib.sys      # auto-produced
└── ProgramMain v0.0.py             # feasibility analysis
```

---
title: "Analog Gauge-Based Task Manager"
layout: page
image:
  thumbnail: /assets/projects/analog.png
---
Let's make a Analog task manager inspired that allows us to display the CPU core loads, CPU core temperatures, CPU power consumption, GPU load, GPU temperature, GPU power consumption, and memory usage.

<style>
    .pdf-container {
    width: 100%;
    height: 100vh;
    border-radius: 20px; /* Adjust the value for the desired roundness */
    overflow: hidden; /* This hides any overflow outside the rounded container */
    position: relative;
    }

    .pdf-object {
    width: 100%;
    height: 100%;
    }

    .pdf-fallback {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #283741;
    border-radius: 20px;
    }

    .content-container-blue {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-color: #283741; /* Add a background color */
    }

    .content-container {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-size: cover;
    background-repeat: no-repeat;
    background-attachment: fixed; /* Optional, for a fixed background */
    }

    .dropdown-content {
        display: none;
        overflow: hidden;
    }
    
    /* Adjusted styles for dropdown-header */
    .dropdown-header {
        display: flex;
        align-items: center;
        cursor: pointer;
        padding-left: 10px;
    }

    .dropdown-header:hover {
        color: #D37070;
    }

    .dropdown-icon {
        font-size: 56px;
        transition: transform 0.3s;
        margin-right: 25px;
    }

    .rotate-icon {
        transform: rotate(-180deg);
    }

    .dropdown-content {
        display: none;
        overflow: hidden;
        margin-top: 10px;
    }

    .content-container a {
    color: #D37070; /* Change the color of hyperlinks */
    text-decoration: underline; /* Add underline to hyperlinks */
    }
</style>

<div class="content-container" data-bg-image="/assets/images/chevron2.png">
    This project is available as a Github Repository <a href="https://github.com/420Ayan420/analog-task-manager">here</a>.
</div>

<div class="content-container" data-bg-image="/assets/images/chevron2.png">
    Suggestions? Want to discuss a certain aspect of my work? Please contact me at ayanali20985@gmail.com, use the direct email link in the bottom of the menu on the left, or create a Github pull request.
</div>

<div class="content-container-blue">
    <div class="dropdown-header">
        <span class="dropdown-icon">&#9660;</span> <!-- Down-arrow icon -->
            Analog Task Manager v0.0
    </div>
    <div class="dropdown-header" class="dropdown-content">
        This project is in inspired by <a href="https://www.youtube.com/watch?v=4J-DTbZlJ5I">this</a>.

    <p>To complete this project we have to do the following:</p>
    <ol>
    <li>Software<ol>
    <li>Create a script to read all relevant readings from from WMI (windows management instrumentation)</li>
    <li>Parse and process this data into a useful voltage value</li>
    <li>Send this processed data to an Arduino so that it can be used to control analog gauges. Also add basic code to add color changing lights.</li>
    </ol>
    </li>
    <li>Hardware<ol>
    <li>Take this data and send it properly to the relevant gauge using the digital PWM pins on the Arduino Mega2560.</li>
    <li>Use digital I/O pins to control the RGB lights for each gauge so that it can be red/yellow/green for the status of the gauge.</li>
    <li>Add in 2 toggle switches for ON/OFF for the reading on the gauge and the backlight on the gauge.</li>
    <li>Add a variable resistor dimmer switch for each gauge backlight.</li>
    </ol>
    </li>
    <li>Nice-to-haves<ol>
    <li>Nice casing that is curved and matches the curve of your eyes just like a curved monitor does.</li>
    <li>Make it sit low so it does not cover a large portion of desk space.</li>
    <li>Make it modular so additional gauge clusters can be added without having to change the frame. Use magnets and contact connectors such as 4-pin headphone jacks to connect for power and data.</li>
    <li>Perhaps make a program/software that can easily adapt to each system and allow the user to program what each gauge does.</li>
    <li>Add a small LCD on the gauge to allow user to change the name of the purpose of each gauge easily and without fuss.</li>
    </ol>
    </li>
    </ol>
    <p>First, let us prove the feasibility of such a project through a proof of concept.</p>
    <p>Let&#39;s first create script to take data from the WMI and print it out to console. I&#39;m going to keep it simple and just use python as we do not need that much power. Be very careful with the installation of the clr library as we should use:</p>
    <pre><code class="lang-powershell">pip <span class="hljs-keyword">install</span> pythonnet
    pip <span class="hljs-keyword">install</span> pyserial
    </code></pre>
    <pre><code class="lang-python"><span class="hljs-keyword">import</span> clr  <span class="hljs-comment">#IMPORTANT! pip install pythonnet, NOT pip install clr</span>
    <span class="hljs-keyword">import</span> serial
    <span class="hljs-keyword">import</span> time

    c = Computer()
    c.CPUEnabled = <span class="hljs-keyword">True</span>
    c.GPUEnabled = <span class="hljs-keyword">True</span>
    c.Open()

    <span class="hljs-keyword">while</span> <span class="hljs-keyword">True</span>:
        c.Hardware[<span class="hljs-number">1</span>].Update()  <span class="hljs-comment"># Update the hardware info</span>
        <span class="hljs-keyword">for</span> sensor <span class="hljs-keyword">in</span> c.Hardware[<span class="hljs-number">1</span>].Sensors:
            <span class="hljs-keyword">if</span> sensor.SensorType == SensorType.Temperature <span class="hljs-keyword">and</span> sensor.Value <span class="hljs-keyword">is</span> <span class="hljs-keyword">not</span> <span class="hljs-keyword">None</span>:
                temperature = sensor.Value
                print(<span class="hljs-string">"GPU Temp is:"</span>, temperature)
                ser.write(f<span class="hljs-string">"{temperature}\n"</span>.encode())
    </code></pre>
    <p>Nice! Okay now lets update this code so that it sends it across to the Arduino on COM4 and baudrate 9600.</p>
    <pre><code class="lang-python"><span class="hljs-keyword">import</span> clr  <span class="hljs-comment">#IMPORTANT! pip install pythonnet, NOT pip install clr</span>
    <span class="hljs-keyword">import</span> serial
    <span class="hljs-keyword">import</span> time

    clr.AddReference(<span class="hljs-string">'OpenHardwareMonitorLib'</span>)
    <span class="hljs-keyword">from</span> OpenHardwareMonitor.Hardware <span class="hljs-keyword">import</span> Computer, SensorType

    ser = serial.Serial(<span class="hljs-string">'COM4'</span>, <span class="hljs-number">9600</span>, timeout=<span class="hljs-number">1</span>)

    c = Computer()
    c.CPUEnabled = <span class="hljs-keyword">True</span>
    c.GPUEnabled = <span class="hljs-keyword">True</span>
    c.Open()

    <span class="hljs-keyword">while</span> <span class="hljs-keyword">True</span>:
        c.Hardware[<span class="hljs-number">1</span>].Update()  <span class="hljs-comment"># Update the hardware info</span>
        <span class="hljs-keyword">for</span> sensor <span class="hljs-keyword">in</span> c.Hardware[<span class="hljs-number">1</span>].Sensors:
            <span class="hljs-keyword">if</span> sensor.SensorType == SensorType.Temperature <span class="hljs-keyword">and</span> sensor.Value <span class="hljs-keyword">is</span> <span class="hljs-keyword">not</span> <span class="hljs-keyword">None</span>:
                temperature = sensor.Value
                print(<span class="hljs-string">"GPU Temp is:"</span>, temperature)
                ser.write(f<span class="hljs-string">"{temperature}\n"</span>.encode())
    </code></pre>
    <p>Okay now lets write some simple code to take this GPU temp reading and turn on the onboard LED if it exceed 51°C.</p>
    <pre><code class="lang-C++"><span class="hljs-keyword">void</span> <span class="hljs-built_in">setup</span>() {
    <span class="hljs-built_in">pinMode</span>(<span class="hljs-literal">LED_BUILTIN</span>, <span class="hljs-literal">OUTPUT</span>);
    <span class="hljs-built_in">Serial</span>.<span class="hljs-built_in">begin</span>(<span class="hljs-number">9600</span>);
    }

    <span class="hljs-keyword">void</span> <span class="hljs-built_in">loop</span>() {
    <span class="hljs-built_in">if</span> (<span class="hljs-built_in">Serial</span>.<span class="hljs-built_in">available</span>() &gt; <span class="hljs-number">0</span>) {
        <span class="hljs-keyword">float</span> gpuTemperature = <span class="hljs-built_in">Serial</span>.<span class="hljs-built_in">parseFloat</span>();
        <span class="hljs-built_in">if</span> (gpuTemperature &gt; <span class="hljs-number">51.0</span>) {
        <span class="hljs-built_in">digitalWrite</span>(<span class="hljs-literal">LED_BUILTIN</span>, <span class="hljs-literal">HIGH</span>);
        } <span class="hljs-built_in">else</span> {
        <span class="hljs-built_in">digitalWrite</span>(<span class="hljs-literal">LED_BUILTIN</span>, <span class="hljs-literal">LOW</span>);
        }
    }
    }
    </code></pre>
    <p>We have now proven it is possible to do this using the this pipeline. The structure of our software is as follows:</p>
    <pre><code>analog task manager
    ├── OpenHardwareMonitorLib.dll      # available through their source <span class="hljs-keyword">code</span>.
    ├── OpenHardwareMonitorLib.sys      # auto-produced
    └── ProgramMain v0<span class="hljs-number">.0</span>.py             # feasibility analysis
    </code></pre>
    </div>
</div>

<div class="content-container-blue">
    <div class="dropdown-header">
        <span class="dropdown-icon">&#9660;</span> <!-- Down-arrow icon -->
            Analog Task Manager v0.1
    </div>
    <div class="dropdown-header" class="dropdown-content">
        Under-progress, to be deployed within the week.
    </div>
</div>

<script>
    // Select all dropdown-header elements
    var dropdownHeaders = document.querySelectorAll(".dropdown-header");

    // Add click event listener to each dropdown-header
    dropdownHeaders.forEach(function(header) {
        header.addEventListener("click", function() {
            // Find the next sibling element which is the dropdown content
            var content = this.nextElementSibling;
            var icon = this.querySelector(".dropdown-icon");

            // Toggle display and icon rotation
            if (content.style.display === "block") {
                content.style.display = "none";
                icon.classList.remove("rotate-icon");
            } else {
                content.style.display = "block";
                icon.classList.add("rotate-icon");
            }
        });
    });

    // Get all elements with the class "content-container"
    const contentContainers = document.querySelectorAll(".content-container");

    // Loop through the elements and set their background images
    contentContainers.forEach(container => {
        const bgImage = container.getAttribute("data-bg-image");
        container.style.backgroundImage = `url(${bgImage})`;
    });
</script>
