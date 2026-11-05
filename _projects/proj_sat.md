---
layout: project
title: "SDC GOAT-1 Satellite"
photo: /public/images/goat1.jpg
date: 2025-12-01
excerpt: "WPI's first satellite, a PocketQube"
---

## Overview

The GOAT-1 Satellite, developed by WPI's Spacecraft Development Club (SDC), is WPI's first satellite, developed to begin a flight history and to develop and test power and control systems that can be scaled for future larger missions.  The satellite fits within the PocketQube standards, with sides of 5cm and a mass of no more then 250 grams.  I was the Support Systems Lead from 2024 to 2026, in charge of main control board development, which operates the camera, control the power board, and transmits images from space to the ground.

<body>
    <figure>
        <img src="{{ '/public/images/goat2.jpg' | relative_url }}" alt="GOAT1 Full Prototype">
        <figcaption>Full testing prototype assembled, with glass installed</figcaption>
    </figure>
</body>

Other then our main systems, we were testing two novel satellite features: a switchable glass sunshade for the camera, and using PCBs as structural components.  In larger satellites, there are systems to stabilize and maneuver the satellite while in orbit.  With small satellites like ours, there is simply not enough weight for these systems, so the satellites tumble through space, leading to the satellite's camera pointing directly at the sun repeatedly.  This leads to camera failures long before the satellite de-orbits.  Our solution is testing a piece of switchable glass as a sunshade, along with software to figure out how the satellite is tumbling, to protect the camera from the sun.  The glass uses no moving parts, only an applied electric charge, can be switched on and off thousands of times, and is very light.  A paper written on this solution was submitted to the American Institute of Aeronautics and Astronautics (AIAA).

The other test we performed is on the structural stability of PCBs in a vacuum, which has not been done in extended tests before.  We completed several Earth based tests to analyze degassing and structural stability, as well as several sensors on the satellite to gather data over the several years the satellite will orbit the Earth.

