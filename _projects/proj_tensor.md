---
layout: project
title: "Tensor Coprocessor for Croc SoC"
photo: /public/images/tensor.png
date: 2025-12-10
excerpt: "Efficient matrix multiplication for edge device inference"
---

## Overview
This is a Tensor Core, developed as a co-processer for the [Croc SoC](https://github.com/pulp-platform/croc) developed by ETH Zurich and the University of Bologna, designed to compute matrix multiplication as quickly as possible. It consists of 4 processing elements performing 8 MAC operations in parallel every cycle on INT8 outputting in INT32, allowing for 640,000,000 operations per second at 80 MHz. For reference: GPT-2 Small needs an average of 248 million ops per token, so we can generate 2.58 tokens per second.  This hardware allows for a 9.58x speedup over calculation in software.  Our size was constrained by both needing to tape out with other projects on the same chip and by strict memory fetching limits, but we have made the design to be easily expandable.  The chip was taped out during May 2026, and has yet to be recieved back from the fabrication lab.

At the center of the Tensor core is a systolic array, made of Processing Elements (PEs), which can be seen below.  Each processing element takes the data from above and the data from the left, multiplies and accumulates in one cycle, then passes the data down and to the right.  This provides major memory savings over more traditional calculation, as each value in the matrix only needs to be fetched a single time, unlike traditional CPUs and GPUs which must repeatedly fetch the same value for each multiplication it is needed for.

<body>
    <figure>
        <img src="{{ '/public/images/pe.png' | relative_url }}" alt="Processing Element" style="width:70%">
    </figure>
</body>

Below is a visualization of how data moves through a systolic array, where a 2x2 systolic array is calculating multiple 2x2 matrix multiplications (A * B, C * D, etc).  After a start up period where each processing element is filling with data, every clock cycle 

<body>
    <figure>
        <img src="{{ '/public/images/Systolic.gif' | relative_url }}" alt="Systolic Function" style="width:70%">
    </figure>
</body>

### Design
<body>
    <figure>
        <img src="{{ '/public/images/matrixmult.png' | relative_url }}" alt="Tiling" style="width:70%">
        <figcaption>Tensor Core Architecture</figcaption>
    </figure>
</body>

#### State Machine
<body>
    <figure>
        <img src="{{ '/public/images/tiling.png' | relative_url }}" alt="Tiling" style="width:70%">
    </figure>
</body>

#### Data Fetching/Storing
As Croc's data fetching pipeline is limited to just 32 bits every clock cycle, major additions had to be made for the system to function.  The state machine \

### Operation

4 Processing Elements which perform 2 operations a second at 20 MHz provide 160 million operations a second.  To produce 1 token on GPT-2 Medium, around 808 million operations need to occur.  Thus, our co-processor can produce a token every 5.05 seconds.  Not too bad for a extremely memory limited device.
