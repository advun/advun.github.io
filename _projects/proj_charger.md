---
layout: project
title: "Anti-Overcharge Power Brick"
photo: /public/images/tbd.jpg
date: 2025-05-05
excerpt: "A smart charging block for any device"
---

## Overview

In ECE2799: Electrical and Computer Engineering Design, we were broken up into three person groups and given the task to design and build a product that could save consumers money within 6 weeks.  I was in charge of electrical design.

Our product was a charger that could automatically detect the power levels of charging batteries connected to it, and shut off charge to full batteries, preventing overcharge and damage to batteries. While some devices like smartphones have overcharge protection, most do not, including almost every commercial laptop.  Even the devices that do have overcharge protection are not perfect, as many times phones are noticablly warm to the touch after a night plugged in.  This overcharging leads to repeated battery damage that reduces the time consumers get out of their batteries, forcing the purchase of replacement batteries or new devices altogether.

It won top product out of 20 total teams in the class, as judged by several engineers and product managers invited by our professors.  

## Design
To accommodate all devices, we added four ports to the brick: 2 USB-C and 2 USB-A ports.  All of these are connected to USB Power Delivery (PD) controllers, which allow for various voltages to be output from each port depending on the device plugged into the port, after a handshake is performed with the device.  The USB-C ports are capable of outputting up to 60W, enough to charge most modern laptops, and all four ports can charge at full power at the same time, ensuring a consumer could charge all of their devices at once.  

Each port, save for one always on USB-A port, tracks current flow.  By observing the rate of change in current flow into the charging battery, an approximation can be made to the fullness of the battery, regardless of the size.  When the derivative of the current flow dropped to the level we found experimentally to be around 80%, the reccomended max charge of a battery, we shut off power to that port, and the corresponding port LED turned off. 

### Schematic
<iframe src="{{ '/public/files/smartchargschem.pdf' | relative_url }}" width="100%" height="800px" style="border: none; border-radius: 6px;">
  This browser doesn't support embedded PDFs.
  <a href="{{ '/public/files/smartchargschem.pdf' | relative_url }}">Download the PDF instead.</a>
</iframe>


## Final Presentation
<iframe src="{{ '/public/files/2799pres.pdf' | relative_url }}" width="100%" height="800px" style="border: none; border-radius: 6px;">
  This browser doesn't support embedded PDFs.
  <a href="{{ '/public/files/2799pres.pdf' | relative_url }}">Download the PDF instead.</a>
</iframe>