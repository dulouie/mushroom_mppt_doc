---
title: VI-Scanner
layout: post
nav_order: 1
parent: Maximum Power Point Tracking Algorithms
---

### VI-Scanner

For the second algorithm to be tested in this work, the shadow
management of modern MPP trackers is to be implemented. Thereby
the IU-characteristic of the solar module is scanned quickly in an
interval of several minutes and it is checked at which point the maximum
power can be drawn. This operating point is then set for the next
interval. 

The code in Listing
[\[listing:7\]](#listing:7){reference-type="ref" reference="listing:7"}
uses two loops to find the maximum power point of the
PV-module. It
increments the duty cycle of the device from 0% to 70% and measures the
voltage, current, and power of the device. When the voltage $U_{pv}$ on
the solar module drops below $12V$, the recording is stopped. The reason
for this is that the gate driver cannot drive the
mosfet anymore
because the operating voltage is too low. The measured values are stored
in a list and the maximum power point is determined based on the
collected data. Finally, the duty cycle is set to the value of the
maximum power point and the program waits 60 seconds before starting
over. The waiting time can be configured as required to keep the module
optimizer at this point for longer.

```python
power_curve =[]
while(True):
    for duty in range(70):
        device.setDutyCycle(duty)
        time.sleep_ms(20)
        device.getfilteredADC()
        device.calcADCData()
        time.sleep_ms(20)
        power_curve.append(device.power[0])
        device.printOut()
        if device.voltage[0] < 12:
            print('Abbruch ', device.voltage[0])
            break
    power_max = max(power_curve)
    duty_max = power_curve.index(power_max)
    power_curve.clear()
    device.setDutyCycle(duty_max)
    time.sleep_ms(100)
    device.getfilteredADC()
    device.calcADCData()
    time.sleep(60)
```
