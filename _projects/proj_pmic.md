---
layout: project
title: "CRIMSON Power Management IC"
photo: /public/images/crimson.png
date: 2026-05-15
excerpt: "A fully self contained power management ASIC for edge devices"
---

## Overview
CRIMSON, the Conversion and Regulation Integrated Management SolutiON is a Power Management Integrated Circuit (PMIC) with on-chip programmability, monitoring and control, developed over the course of a year as a Major Qualifying Project to fufill final degree requirements at WPI. The PMIC uses various power management methods with external powering such as a Micro-Solar Cell Manager and Linear Battery Charger in combination with a Boost Converter. For the rest of the chip, the LDO, BGR and Bias Network provide internal power. To monitor, the chip measures current and temperature with
an 8-bit SAR ADC filtered by an active Sallen Key LPF and sampled by a 32kHz RTC. These readings are read by an FSM to determine whether the PMIC is operating within safe constraints. The FSM additionally controls the power on and off sequences, as well as controling our output low dropout regulator, ensuring stable, controllable power to sink devices. To encode each programmable section, a SPI Chain has been implemented to send Serial Data from an FPGA.

This ASIC design has been manufactured by TSMC in June 2026 using the TSMC 180nm CMOS 3v3/1v8, 1P6M process, and is awaiting testing.

## Digital Control

### ADC Controller

### State Machine

### POR-PG

## Paper

<iframe src="{{ '/public/files/CRIMSON_MQP_Report_REAL.pdf' | relative_url }}" width="100%" height="800px" style="border: none; border-radius: 6px;">
  This browser doesn't support embedded PDFs.
  <a href="{{ '/public/files/CRIMSON_MQP_Report_REAL.pdf' | relative_url }}">Download the PDF instead.</a>
</iframe>