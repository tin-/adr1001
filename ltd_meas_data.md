# Long-term drift measurement
---

Total number of devices evaluated in long-term drift test:

* EVAL board with ADR1001KHZ manufactured with date code 46 week 2023, Module #A configured for 10V output
* EVAL board with ADR1001KHZ manufactured with date code 46 week 2023, Module #B configured for 6.6V output
* References with LTZ1000ACH#PBF production device - 1 units
* Fluke 732A 10V standards are key long-term reference - 2 units
* xDevs.com QVR device with four LTZ1000ACH averaged with passive resistor network - 1 unit
* Fluke 732C commercial standard - 1 unit (6 month test for transfer)

![Long-term drift measurement setup](https://xdevs.com/doc/xDevs.com/QVRA/ltd_setup_chart_bk.png)

## Manufacturer specifications

Accurate determination of long-term stability and drift rate of a solid-state Zener reference is complex subject, specially with stability levels below 50 &micro;V/V. Stability depends on design of the chip, application circuit components selection and performance, PCB layout design, shielding, environmental contributors and method of measurement. All components involved in the design contribute to final output voltage differently. With careful design and validation many of the negative effects can be measured and corrected, but some residual drift will be inherently develop over the long time scales. 

![Long-term drift spec](https://github.com/tin-/adr1000/blob/main/img/ltd_spec.png?raw=true)

Manufacturer long-term stability specifications can be used as a starting point to determine expected performance of the IC. For high performance ovenized Zener references such parameter is often included in [datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/adr1001.pdf) as "long-term drift" or "long-term stability". ADR1001 &Delta;VREF_LTD is specified for 3.5 mA Base-Zener current and oven temperature +70 &deg;C. In datasheet for ADR1001 we are provided with three relative numbers:

* Drift over first 200 hours : typically 3 &micro;V/V
* Drift over 1000 hours : typically 5 &micro;V/V
* Drift over 2000 hours : typically 5 &micro;V/V

There is no maximum drift specification and charts in datasheet for long-term drift for both 6.6 V and 5 V outputs are for sample set of 32 chips. Specification of the long-term stability this way departs from more common drift rate representation using &Sqrt;(kHours), such as LTZ1000's specification 2 &Sqrt;(kHours). Representation &Sqrt;(kHours) have own limitations as actual Zeners reach small but linear drift rate over few years time, unlike larger theoretical reduction of drift rate over time.

Ideally, measuring the long-term drift of the DUT's output voltage would require a significantly more stable reference so that a direct comparison could be done. Both ADR1001 and older ADR1000/LTZ1000 are the best chips that are commercially available capable to maintain stability better than 1 &micro;V/V, so better reference requirement implies direct comparison to Josephson Voltage Standard over a long duration of time. Such standard was not available for the duration of this study, so instead bank of well aged constantly-powered Zener standards was utilized. Bank was calibrated multiple times on the Josehpson Voltage Standard to accurately determine long-term drift.

DC Voltage standard stability verification to levels below a few &micro;V/V and complicated analysis of results is not an easy challenge. Different solutions and approaches were tested in practice by xDevs.com members since 2016. One of very good solutions was acquisition of the specialized low thermal scanner, such as [Dataproof 160 or 320](https://xdevs.com/fix/dp160a) and measuring each DC Voltage reference output individually by some high-end long scale multimeter, such as Keysight 3458A or Datron 1281. But this method is prone to errors and would depend on noise and temperature stability of DMM. Gain errors can be cancelled out by using calibrated DC standard with known drift as a reference, but other issues remain in this method.

Better approach is to perform the comparison of voltage differential in series opposition between two different DC standards. This significantly reduced requirements for DVM performance and even lower-end 6&frac12;-digit instruments such as [HP 34401A](https://xdevs.com/fix/hp34401a) used in lowest 100mV range can be used now to obtain sub-ppm uncertainty. But best instrument for this task is often sensitive nanovoltmeter which can easily resolve even fractions of microvolt between loosely matched 10 V outputs of various standards. 1 &micro;V of 10V equals 0.1 ppm resolution, and nanovoltmeter like Keithley 2182A or [Keysight 34420A](https://xdevs.com/fix/hp34420a) have own noise floor around 0.03 &micro;V. Given internal Zener reference noise in commercial DC standards at level around ~1 &micro;V such comparison method is well suited for detecting even minute changes in output voltage EMF with best uncertainty. This procedure is also [covered with diagrams in detail here](https://xdevs.com/article/792x_cal/#Zenercal)

This method is also what Fluke recommends performing calibration of their own 732B/C standards. In fact, even in Josephson Voltage standard system such as [NIST SRI 6000](https://www.nist.gov/sri/standard-reference-instruments/sri-6000-series-programmable-josephson-voltage-standard-pjvs) or [Supracon](http://www.supracon.com/files/online/NormaleSpannungsnormal/AC_QuantumVoltmeter_cooler.pdf) the calibration of unknown source or DC standard is done in very same manner. JVS array +10 V output configured as quantum-accurate noiseless level and connected in opposite to the compared Zener, with commercial nanovoltmeter like HP 34420A measuring difference in nanovolts. This provides a direct link to intrinsic realization of the voltage, limited only by quality of the scanner/switching system, parasitic EMFs and nanovoltmeter detector short-term noise. Any gain and linearity errors of the nanovoltmeter can be easily calibrated and cancelled out with programmable JVS array output as well.

Based on similar setup and 2182A nanovoltmeter + DP160A scanner instrumentation following results were obtained. Tests were performed on both 6.6V Zener output voltage and with scaled 10V output voltages.

## Future work

The study of long-term drift leaves some questions open, such as how oven set point temperature and Zener current affect long-term drift, and require larger sample set to gain more confidence in results. In theory, higher current and higher temperature would cause drift rate to accelerate as well, but it's not so simple in the real world application. Experimental verification of these claims would be very useful and will be done at a later date. These initial results exhibit rather noticeable initial drift of new ADR1001 Zener IC and highlight importance of careful procedures and possible need of selection to obtain desired long term stability better than 1 &micro;V/V per year.

## Other notable references

* [Forum page about other ADR1001-based references](https://www.eevblog.com/forum/metrology/adr1001-ovenized-voltage-reference-system/) - branadic and Andreas also demonstrated long-term drift by ADR1001 with similar behavior, despite completely different instrumentation approach.
