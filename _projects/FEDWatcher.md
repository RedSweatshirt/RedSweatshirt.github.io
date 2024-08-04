---
layout: page
title: FEDWatcher, A Raspberry Pi Interface for FED3 Devices
description: Research at MIT Choi Labs
img: assets/img/FEDWatcher/fedwatcher_logo.png
importance: 3
category: work
---

<center>
    <div class="row justify-content-sm-center">
        <div class="col-sm-4 mt-3 mt-md-0">
            {% include figure.liquid path="assets/img/FEDWatcher/fedwatcher_logo.png" title="FEDWatcher logo" class="img-fluid rounded z-depth-1" %}
        </div>
    </div>
</center>
<div class="caption">
    The FEDWatcher Logo
</div>

As a developer with a passion for both coding and design, I was excited to take on a project that would challenge my skills and offer a unique opportunity to contribute to the world of open-source software. The FEDWatcher project not only delivered on that promise but also allowed me to create something innovative for the scientific community.

#### The FEDWatcher Project

<div class="container">
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.liquid path="assets/img/FEDWatcher/fedwatcher-top.jpg" title="FEDWatcher top" class="img-fluid rounded z-depth-1" %}
        </div>
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.liquid path="assets/img/FEDWatcher/fedwatcher-side.jpg" title="FEDWatcher side" class="img-fluid rounded z-depth-1" %}
        </div>
    </div>
</div>
<div class="caption">
    Two photos of the PCB design for FEDWatcher installed on a Raspberry Pi
</div>

FEDWatcher is a software solution that connects up to four FED3 feeder devices to a single Raspberry Pi 4. Using a Raspberry Pi as the central hub, the software communicates with the FED3 devices through software serial from the BNC port of the FED3 device to a headphone jack port connected to the UART channels on the Pi.

Originally, the FED3 mouse feeder had to be removed from the mouse's cage to collect the information, potentially interfering with the experiment. This was an inconvenient and time-consuming process, as it required researchers to manually retrieve data from the feeder. Additionally, the microcontroller inside the feeder had only a single port left available, which was a standard digital wire.

FEDWatcher was designed to address these limitations by using the remaining port on the microcontroller to communicate with the feeder without needing to remove it from the cage. This allows researchers to remotely monitor the feeder, reducing the chances of disrupting ongoing experiments. FEDWatcher uses a workaround in software serial to transmit data reliably, making it a valuable tool for scientific research involving FED3 feeders.

The [Github repository](https://github.com/matiasandina/FEDWatcher) for FEDWatcher contains the following:

1. Python code using standard Raspberry Pi software and Python packages.
2. The modified software serial library used on the FED3 devices (softwareSerial).
3. Files for printing the PCB, used as a Raspberry Pi HAT for easier interfacing with the Raspberry Pi 4 pinout.
4. Python code for the FEDWatcher GUI, enabling users to create projects and trigger FEDWatcher easily.

<div class="container">
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.liquid path="assets/img/FEDWatcher/circuit_drawing.png" title="FEDWatcher circuit diagram" class="img-fluid rounded z-depth-1" %}
        </div>
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.liquid path="assets/img/FEDWatcher/gui.png" title="FEDWatcher GUI" class="img-fluid rounded z-depth-1" %}
        </div>
    </div>
</div>
<div class="caption">
    First Image: Circuit diagram for the Raspberry Pi UART interfaces. Second Image: The FEDWatcher GUI
</div>

#### My Role

As a developer on the FEDWatcher team, my primary responsibilities included adapting the open-source FED3 mouse feeder systems for remote monitoring capabilities, engineering new hardware to interface the offline mouse feeder using a Raspberry Pi for internet connectivity, and developing software for the Raspberry Pi to monitor the mouse feeders and transmit data and alerts autonomously.

During the development process, I focused on creating efficient, easy-to-understand Python code that would work seamlessly with Raspberry Pi software and Python packages. This involved setting up the Raspberry Pi OS, enabling hardware UARTs, and installing the FEDWatcher software within a virtual environment. Additionally, I worked on finding an optimal hardware connection between the microcontroller on the FED3 feeder and a Raspberry Pi. I settled on a SoftwareSerial connection, due to the constraints of the design of the FED3, which left only a digital pin to work with.

While my colleagues designed the FEDWatcher GUI, I worked closely with them to ensure that the components would be compatible and create a user-friendly experience for researchers and developers. The FEDWatcher HAT was designed by another collaborator on the open-source project.

#### The Result

The result of our collaborative work on the FEDWatcher project is a versatile, user-friendly, and cost-effective solution for connecting FED3 devices to a Raspberry Pi. With this software and HAT design, users can now easily interface with FED3 devices, enabling new possibilities in scientific research and experimentation.

The FEDWatcher project has been an incredible opportunity to put my skills in software development and hardware engineering to the test, while working alongside a talented team of colleagues. I'm proud to have played a part in its creation and am excited to see how the FEDWatcher will be utilized by the scientific community in the future.

If you're interested in learning more about the FEDWatcher project or would like to contribute, please visit the [GitHub repository](https://github.com/matiasandina/FEDWatcher) and join the ongoing conversation. Let's continue to push the boundaries of what's possible in the world of open-source software and scientific research.