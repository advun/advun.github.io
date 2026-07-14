---
layout: project
title: "LED Array Business Card"
photo: /public/images/card1draw.png
date: 2024-9-15
excerpt: "An LED array card small enough to fit in your wallet and (nearly) cheap enough to give away"
---
<hr style="border: none; border-top: 4px solid rgba(0,0,0,0.5); margin: 2rem 0;">

## Why Business Cards?

As I learned more about electronics in my undergraduate degree, I came across [this](https://www.instructables.com/PCB-Business-Card-With-NFC/) NFC business card by loboat and [this](https://www.youtube.com/watch?v=zHVrY_xLM3c) wonderful stylophone business card made by the great [mitxela](https://mitxela.com/).  Wanting to make my own PCB card with a bit more flair, I set out to make a card that 

1. Cheap
2. Actually Card Sized
3. Stood out

As such, I landed on making a card with a small LED array, for displaying animations and text.

## Design Details
PCBs are, unfortunatly, thicker then paper.  Even the thinnest PCBs I could source (0.06 inches) are about twice as thick as a credit card.  However, this thickness allowed me to use CR2016 coin cell batteries (0.058 inches thick) as my power source, slotting into a hole cut into the side of the card.  To keep thickness down, my switch too was chosen to be as thin as possible, fitting onto the side of the card in a slot like the battery.  

## Electrical Design
The LEDs are a 5x5 Charlieplexed array, in which each column of LEDs shares an anode, and each row of LEDs shares an cathode, allowing for just 6 lines from the ATTINY1606 to control all 25 LEDs, as well as just 6 LEDs.  Through persistance of vision, each LED can be flickered quickly enough to trick the eye into seeing them as constantly on.  

### Schematic
<iframe src="{{ '/public/files/charlieplexed_led_schematic.pdf' | relative_url }}" width="100%" height="800px" style="border: none; border-radius: 6px;">
  This browser doesn't support embedded PDFs.
  <a href="{{ '/public/files/charlieplexed_led_schematic.pdf' | relative_url }}">Download the PDF instead.</a>
</iframe>
