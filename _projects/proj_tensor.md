---
layout: project
title: "Tensor Coprocessor for Croc SoC"
photo: /public/images/tensor.png
date: 2025-12-10
excerpt: "Efficient matrix multiplication for edge device inference"
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
This is a Tensor Core, developed as a co-processer for the [Croc SoC](https://github.com/pulp-platform/croc) developed by ETH Zurich and the University of Bologna, designed to compute matrix multiplication as quickly as possible. It consists of 4 processing elements performing 8 MAC operations in parallel every cycle on INT8 outputting in INT32, allowing for 640,000,000 operations per second at 80 MHz. For reference: GPT-2 Small needs an average of 248 million ops per token, so we can generate 2.58 tokens per second.  This hardware allows for a 9.58x speedup over calculation in software.  Our size was constrained by both needing to tape out with other projects on the same chip and by strict memory fetching limits, but we have made the design to be easily expandable.  The chip was taped out during May 2026, and has yet to be recieved back from the fabrication lab.  The GitHub link can be found [here](https://github.com/advun/Croc-Tensor-Core/).

At the center of the Tensor core is a systolic array, made of Processing Elements (PEs), which can be seen below.  Each processing element takes the data from above and the data from the left, multiplies and accumulates in one cycle, then passes the data down and to the right.  This provides major memory savings over more traditional calculation, as each value in the matrix only needs to be fetched a single time, unlike traditional CPUs and GPUs which must repeatedly fetch the same value for each multiplication it is needed for.

<body>
    <figure>
        <img src="{{ '/public/images/pe.png' | relative_url }}" alt="Processing Element" style="width:70%">
    </figure>
</body>

Below is a visualization of how data moves through a systolic array, where a 2x2 systolic array is calculating multiple 2x2 matrix multiplications (A * B, C * D, etc).

<body>
    <figure>
        <img src="{{ '/public/images/Systolic.gif' | relative_url }}" alt="Systolic Function" style="width:70%">
    </figure>
</body>

For matrix multiplication larger then 2x2 matrices, we use a tiling system, where a matrix of any size is broken into 2x2 "tiles".  As seen below, if one breaks two 4x4 matrixes A and B into 2x2 blocks, one can perform matrix multiplication normally upon them.  So, if A x B = C, the 2x2 matrix C11 is equal to A11 * B11 + A12 * B21.  Through this tiling, matrixes of any size can be calculated.

<body>
    <figure>
        <img src="{{ '/public/images/tiling.png' | relative_url }}" alt="Tiling" style="width:50%">
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

#### Data Fetching/Storing
As Croc's data fetching pipeline is limited to just 32 bits every clock cycle, major additions had to be made for the system to function.  The state machine \

