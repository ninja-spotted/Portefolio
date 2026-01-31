---
title:  "Android TV Box to Linux server"
parent: Blog
permalink: "/blog/android-tv-box-to-linux-server"
layout: default
date:   2026-01-31
last_modified_date: 2026-01-31
---

# Android TV Box to Linux appliance

## Introduction and why bother

There is a high chance that the person reading this has bought in the past one of those cheap android boxes to transform a television into a "smart" television, making it possible to watch more than cable channels. After the initial excitement, it might have gotten retired for being too cumbersome to use, low power or simply unsupported by every app after a while. What if you could save it from being E-waste?

## Credits & inspiration

The idea to look for my dusty android box came after watching the video [Linux on a TV Box - Raspberry Pi Alternative?](https://www.youtube.com/watch?v=b1UIIlYLM4I) from [TheSillyWorkshop](https://www.youtube.com/@TheSillyWorkshop) a few months ago. This seemed like something right up my alley, since I hate having devices that me or my family bought to be used once and forgotten.

With this in mind, I looked around for my TV Box, noted the model name and went online finding out if anyone had already had installed an alternative OS to the thing. That's when I found the [Turning an Amlogic S912 Android TV Box Into a Linux Appliance](https://sigmdel.ca/michel/ha/aml912/linux_on_aml912_en.html) blog post from [sigmdel.ca/michel](sigmdel.ca/michel), which was really useful during this whole experience. I would recomend to everyone to have a look at the blog since there are topics like networking, microcontroller reviews or other linux boxes.

## The box itself

My former Android box is the **Beelink GT 1**, adquired around 2017. The thing never had much use, outside of a few streaming sessions and it was quickly forgotten. It came with an IR transmitter controller and a 10 Watts (5V, 2A) rated power brick, with a barrel connector to the box. As for internal specifications:

|  Beelink GT1     | Specifications             |
|      :---        |      :---:                 |
| OS               | Android 6                  |
| CPU              | Amlogic S912               |
| GPU              | Mali-T820                  |
| RAM              | 2 GB                       |
| Storage (eMMC)   | 16 GB                      |
| Storage (microSD)| 512 GB Max.                |
| Ethernet         | Gigabit LAN                |
| Wireless         | Wi-Fi AC and BT4.0         |
| Video out        | HDMI 2.0                   |
| USB              | 2 x USB 2.0                |
| Power            | 10 Watts (5V, 2A)          |




### Internals

### Power draw

## Operating systems

### "Out-of-the-box" experience

### Libreelec

### Armbian

#### USB booting

#### Installing to internal storage

