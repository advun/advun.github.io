---
layout: project
title: "Tensor Coprocessor for Croc SoC"
photo: /public/images/tensor.png
date: 2025-12-10
excerpt: "Efficient matrix multiplication for edge device inference"
---

## Overview

### Design

#### Systolic Array

#### Data Fetching/Storing

### Operation

4 Processing Elements which perform 2 operations a second at 20 MHz provide 160 million operations a second.  To produce 1 token on GPT-2 Medium, around 808 million operations need to occur.  Thus, our co-processor can produce a token every 5.05 seconds.  Not too bad for a extremely memory limited device.
