---
title: "Project BrickBoy"
category: "Engineering"
description: "An in-progress project aiming to convert the LEGO Gameboy set into a fully playable handheld emulator, with the secondary goal of creating a high quality 3D-printed handheld emulator."
images:
  - /images/brickboy1.jpg
  - /images/brickboy2.jpg
  - /images/brickboy3.jpg
highlight: false
layout: project
---

*Project Brickboy* looks to create a fully functioning handheld emulator that fits within the official LEGO Gameboy model. Using the same hardware, a second design will be made as a more comfortable and easy to manufacture alternative to the Lego version. Many existing emulators use SPI protocol to drive the screen, which results in sluggish response rates and a poor end user experience. This design uses RGB DPI protocol to fix this issue, but due to the high number of GPIO pins that must be used to run this connection, an external microcontroller (in this case a Seeeduino XIAO RP2040) is connected through USB to send the control inputs back to the main Raspberry Pi.
