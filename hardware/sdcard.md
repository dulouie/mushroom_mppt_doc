---
title: SD card reader
layout: post
nav_order: 10
parent: Hardware implementation
---

# SD card reader

As part of a project that is exposed to various environmental
conditions, it is often necessary to store data over time to analyze the
performance of the solar module and other system components. A common
method to store data is to put it on an SD card. The RP2040
microcontroller provides an easy way to store data on an SD card since
it has a built-in [spi]{acronym-label="spi"
acronym-form="singular+short"}. In this section, we will look at setting
up the SPI connection between the RP2040 and the SD card.
[spi]{acronym-label="spi" acronym-form="singular+short"} is a serial
communication protocol used to connect between microcontrollers and
peripherals such as sensors, memory chips, displays, wireless modules,
and many others. SPI allows fast and reliable transfer of data between
devices over short distances and can be used in many applications due to
its ease of implementation and low cost. A *SD Card Breakout Board* is
used, this can be directly connected to the [spi]{acronym-label="spi"
acronym-form="singular+short"} bus according to figure
[\[fig:sdcard\]](#fig:sdcard){reference-type="ref"
reference="fig:sdcard"} and is the compatible with supply voltage of
$3.2V$.

![image](import/sdcard.pdf){width="0.5\\linewidth"} []{#fig:sdcard
label="fig:sdcard"}
