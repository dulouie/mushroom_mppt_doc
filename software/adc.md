---
title: Analog-digital converter
layout: post
nav_order: 2
parent: Software implementation
---

# Analog-digital converter

An analog-to-digital converter (ADC) is a hardware component that
converts analog input signals into digital values. Usually the
conversion is done with a certain accuracy, which is specified by the
number of bits. The RP2040 is equipped with a 12-bit ADC by default, but
with MicroPython the ADC is internally converted to 16 bits.

$$
V_{digital} = V_{analog} \cdot \frac{V_{sys}}{Resolution ADC} = Value \cdot\frac{3.2V}{2^{16}}$$/label{eq1}

To convert the digital values into analog quantities such as voltage or
current, a conversion function is used. With a 16-bit conversion
function, the input voltage is converted according to the equation
([\[eq:adc\]](#eq:adc){reference-type="ref" reference="eq:adc"}), where
$Value$ is the measured input value in volts.

```python
def getfilteredADC(self):
    '''Sample and filter adc data'''
    self.filtered[0] = self.filter1.calc()
    self.filtered[1] = self.filter2.calc()
    self.filtered[2] = self.filter3.calc()
    self.filtered[3] = self.filter4.calc()
```


The *getfilteredADC()* method in Listing
[\[listing:3\]](#listing:3){reference-type="ref" reference="listing:3"}
is a function in the *MPPTController* class that is used to sample the
voltage and current data from the ADCs and smooth it through filtering.
This involves filtering the raw data from the four ADC channels. The
filtering is necessary to filter out measurement inaccuracies of the
[adc]{acronym-label="adc" acronym-form="singular+short"}. The method
first calls the calc() method of the FilterAvg object for each ADC
channel to get the filtered data. This filtered data is then written to
the filtered array of the MPPTController class, which is later used by
the calcADCData() method to calculate the voltage values.


```python
def calcADCData(self):
    '''Calcuate raw adc data to voltages and currents'''
    self.voltage[0] = round( corr[0] * self.filtered[0] * adcScaleFac
                                                        * voltDiv, rounded)
    self.voltage[1] = round( corr[2] * self.filtered[2] * adcScaleFac
                                                        * voltDiv, rounded)
    self.current[0] = round( corr[1] * ((( self.filtered[1] * adcScaleFac)
                                                - zeroCurrentHall) / 
                                                currentSensivity), rounded)
    self.current[1] = round( corr[3] * ((( self.filtered[3] * adcScaleFac)
                                                - zeroCurrentHall) /
                                                currentSensivity), rounded)
    self.power[0] = round(self.voltage[0] * self.current[0], 2)
    self.power[1] = round(self.voltage[1] * self.current[1], 2)
```


The *calcADCData()* method from Listing
[\[listing:3\]](#listing:3){reference-type="ref" reference="listing:3"}
in the *MPPTController* class is used to convert the raw ADC data into
voltage and current values. For the voltage measurement, a voltage
divider with resistors of 36 kOhm and 2.2 kOhm is used, where *voltDiv*
specifies the divider factor from equation
([\[voltageDiv1\]](#voltageDiv1){reference-type="ref"
reference="voltageDiv1"}). The factor *adcScaleFac* gives the conversion
factor from ([\[eq:adc\]](#eq:adc){reference-type="ref"
reference="eq:adc"}). The converted voltage values are multiplied with
correction factors *corr* and rounded. For the current measurement the
transfer function
[\[eq:tmcs1108trans\]](#eq:tmcs1108trans){reference-type="ref"
reference="eq:tmcs1108trans"} from the last chapter is used.

