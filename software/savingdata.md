---
title: Saving data
layout: post
nav_order: 5
parent: Software implementation
---

# Saving data

SPI is a protocol used to communicate with SD cards. The code in Listing
[\[listing:7\]](#listing:7){reference-type="ref" reference="listing:7"}
initializes an SPI object with the correct parameters and uses the chip
select pin (pin 1) to select the SD card. The initialization is done so
that the microcontroller can write to and read from the SD card.


```python
cs = machine.Pin(1, machine.Pin.OUT)
spi = machine.SPI(0,
                  baudrate=1000000,
                  polarity=0,
                  phase=0,
                  bits=8,
                  firstbit=machine.SPI.MSB,
                  sck=machine.Pin(2),
                  mosi=machine.Pin(3),
                  miso=machine.Pin(4))
sd = sdcard.SDCard(spi, cs)
vfs = uos.VfsFat(sd)
uos.mount(vfs, "/sd")
```

The actual writing of the data to the SD card is done in Listing
[\[listing:8\]](#listing:8){reference-type="ref" reference="listing:8"},
here the file header is set first so that the correct variables can be
assigned to the data later. The code uses a loop to vary the duty cycle
of the device and measure the performance depending on it.

The duty cycle is increased incrementally from 0% to 70%. After each increase in
duty cycle, the voltage, current, and power of the device are measured
and written to a file. The *file.flush()* command ensures that the data
is written to the file immediately and does not just remain in the
buffer memory. The process continues indefinitely until the program is
terminated.

```python
file = open('/sd/iu-data.txt', 'w')
file.write('duty' + ';' + 'voltage[0]' + ';' 
                        + 'current[0]' + ';' 
                        + 'power[0]' + '\n')
while(True):
    for duty in range(70):
        device.setDutyCycle(duty)
        time.sleep_ms(50)
        device.getfilteredADC()
        device.calcADCData()
        time.sleep_ms(50)
        file.write(str(duty) + ';' + 
                   str(device.voltage[0]) + ';' + 
                   str(device.current[0]) + ';' +
                   str(device.power[0]) + ';' +
                   '\n')
        file.flush()
```