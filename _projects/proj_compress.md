---
layout: project
title: "Trace Data Compressor"
photo: /public/images/compress.png
date: 2026-05-01
excerpt: "Compresses bus trace data for efficient on-chip storage"
---

## Overview
In January 2026, as part of the GoatHacks hackathon, I designed an FPGA trace compressor to allow users to collect 
more trace data at once.  If one is observing even 100 traces at 500 MHz, over 50 gigabits of data per second are being created, well above what many FPGAs are capable of offputting.  Thus, trace data is stored in on-board memory, to be read off in the future. This memory is quite limited, to the point which it makes sense to use FPGA resources to compress this trace data to fit longer periods of observation.  Luckily, most trace data is fairly predictable, allowing for a quite simple compression algorithm to do a great deal of work.  

Both designs use run length and delta encoding to take advantage of the predictable behavior of many busses. Long stretches of time where values remain the same or change at the same rate can be compressed quite easily, with minimal hardware, and decompressed without loss.

## Links
[Design 1](https://github.com/advun/goathacksCompressor) won Best Rookie Hack at GoatHacks 2026, and the much improved [Design 2](https://github.com/advun/ttCompressor) was taped out on the [TTsky26b](https://tinytapeout.com/chips/ttsky26b/) shuttle in May 2026, and awaits testing.  It can be viewed through TinyTapeout's viewer [here](https://advun.github.io/ttCompressor/).

