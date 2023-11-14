---
title: "Raspberry Pi Performance Issues"
date: "2023-11-05T13:00:00.284Z"
template: "post"
draft: true
slug: "/posts/raspberry-pi-crashed"
category: "Issues"
tags:
  - "Issues"
  - "Laravel"
  - "RaspberryPi"
description: ""
socialImage: ""
---

## Raspberry Pi Performance Issues

Installing both a LAMP (Linux, Apache, MySQL, PHP) stack and a MERN (MongoDB, Express.js, React, Node.js) stack for another project, turned out to be too much for my Rasberry Pi 4.

Monitoring CPU and memory usage quickly revealed that I was pushing my hardware to the limit. Lesson one: Know your Pi's capabilities and plan accordingly.

Due too all the crashes the SD Card that was serving as my main memory had become corrupted.  SD cards are not 2023-05-11---Raspberry-Pi-Crashed copyinvincible; treat them with care, and always have backups at the ready.

As I hadn't started any substantial work on my project. I made the decision to reformat the SD card and flash a new operating system onto it
