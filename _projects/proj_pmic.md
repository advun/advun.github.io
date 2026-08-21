---
layout: project
title: "CRIMSON Power Management IC"
photo: /public/images/crimson.png
date: 2026-05-15
excerpt: "A fully self contained power management ASIC for edge devices"
---
<style>
figure {
    text-align: center;
    margin: 2rem auto;
}

figure img {
    display: block;
    margin: 0 auto;
}
</style>

## Overview
CRIMSON, the Conversion and Regulation Integrated Management SolutiON is a Power Management Integrated Circuit (PMIC) with on-chip programmability, monitoring and control, developed over the course of a year as a Major Qualifying Project to fulfill final degree requirements at WPI. The PMIC uses various power management methods with external powering such as a Micro-Solar Cell Manager and Linear Battery Charger in combination with a Boost Converter. For the rest of the chip, the LDO, BGR and Bias Network provide internal power. To monitor, the chip measures current and temperature with
an 8-bit SAR ADC filtered by an active Sallen Key LPF and sampled by a 32kHz RTC. These readings are read by an FSM to determine whether the PMIC is operating within safe constraints. The FSM additionally controls the power on and off sequences, as well as controling our output low dropout regulator, ensuring stable, controllable power to sink devices. To encode each programmable section, a SPI Chain has been implemented to send Serial Data from an FPGA.

This ASIC design has been manufactured by TSMC in June 2026 using the TSMC 180nm CMOS 3v3/1v8, 1P6M process, and is awaiting testing.

<body>
    <figure>
        <img src="{{ '/public/images/pmicoverview.png' | relative_url }}" alt="PMIC Wiring Diagram">
        <figcaption>Full CRIMSON Wiring and Architecture Diagram</figcaption>
    </figure>
</body>


### Digital Control
I was in charge of the Digital Control blocks, consisting of the Finite State Machine (FSM), the Power on Reset Pulse Generator (POR-PG), and the ADC Controller.  The Finite State Machine controlls power up and down sequences, as well as safety checks and user input responces, the ADC Controller provides clocking and data flow control for the ADC, and the POR-PG resets the digital logic on power reaching 3.3V and on brownout.

#### Finite State Machine
The FSM has a large range of interactions with the chip, controlling block enables, timer controls, and power sourcing.  It determines these primarly through ADC readings of power and temperature, though also has several latches and control lines provided to the user to allow the chip to temporarily cease power supply, change operation to use outside provided power, and output ADC information.  The general operation can be seen below, and the full truth tables can be found in the report.

<body>
    <figure>
        <img src="{{ '/public/images/pmicstate.png' | relative_url }}" alt="State Machine">
        <figcaption>State Machine Flowchart</figcaption>
    </figure>
</body>


#### ADC Controller
The 8 bit SAR-ADC used to monitor analog signals on the chip needed several control signals: a start bit to begin reading every 9 cycles, a done bit determining if the read was completed, and a 3 bit control line to switch between which ADC channel was being read from, all of which was provided by the controller.  The controller also held the comparators, seen below, that were used to set upper and lower bounds for each channel through reading from the SPI chain (to allow later changes).  If the current ADC reading was between the upper and lower bounds, adcgood became high, being passed to the FSM along with the start and done signals.

<body>
    <figure>
        <img src="{{ '/public/images/watchdog.png' | relative_url }}" alt="ADC Watchdog" style="width:70%">
        <figcaption>ADC Comparators</figcaption>
    </figure>
</body>

#### POR-PG
The POR-PG is a modified version of one created by Suat Ay, the advisor of this project, in <cite><a href="https://www.worldscientific.com/doi/abs/10.1142/S0218126610006876">A COMPACT CMOS POWER-ON-RESET PULSE GENERATOR DESIGN WITH LOW-POWER AND WIDE OPERATION RANGE</a> </cite>.  It provides a reset pulse after a delay from the power rails reaching 3.3V, ensuring that all digital logic on the chip is properly reset.  Additionally, it provides a reset pulse upon "brownout", which in this configuration meant power dropping below 2.2V, which would put logic high levels dangerously close to logic low.

<body>
    <figure>
        <img src="{{ '/public/images/porpg.png' | relative_url }}" alt="PORPG" style="width:70%">
        <figcaption>POR-PG Design</figcaption>
    </figure>
</body>

Below is the POR-PG in operation.  As Voltage 1 (V5 on the above diagram) reaches the threshold of 2V, the reset pulse is created by the XOR gate, until the delayed Voltage 2 (V4 above) reaches 2V as well, ending the reset pulse.  Later, the power drops, and again a reset pulse is created.

<body>
    <figure>
        <img src="{{ '/public/images/porpgresponce.png' | relative_url }}" alt="PORPG Responce" style="width:70%">
        <figcaption>POR-PG Responce</figcaption>
    </figure>
</body>


## Paper

<iframe src="{{ '/public/files/CRIMSON_MQP_Report_REAL.pdf' | relative_url }}" width="100%" height="800px" style="border: none; border-radius: 6px;">
  This browser doesn't support embedded PDFs.
  <a href="{{ '/public/files/CRIMSON_MQP_Report_REAL.pdf' | relative_url }}">Download the PDF instead.</a>
</iframe>