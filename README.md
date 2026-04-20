# Analog Devices ADR1001 zener performance study 2023-2026

Data repository for Analog Devices ADR1001-based xDevs.com module voltage standards performance, collected by [xDevs.com lab](https://xdevs.com/).

![Photo](https://xdevs.com/doc/Analog_Devices/ADR1001/adr1k1_ppms_1.jpg)

Current Status
--------------
* Drift data collection/analysis : [926 days done, monitoring in progress](ltd_meas_data.md)
* Mid-term 3000 hours drift evaluation: done
* Hysteresis test: done
* Short-term noise evaluation: done
* Tempco evaluation: done
* PSRR evaluation: planned 2026
* Additional evaluation of integrated onchip resistors/amplifiers: TBD 2026

Introduction
------------

This repository contains the data collected on in-house coming soon voltage reference modules assembled with [Analog Devices ADR1001AEZ]([https://xdevs.com/article/adr1000order/](https://xdevs.com/pow/adr1k1_pow/)) buried zener IC. Consistent with my primary use cases for these devices in DC voltage metrology projects, these modules designed with focus on lower integration cost and good stability below 10 ppm/year. 

Data in this repository was collected and analyzed within scope of the presentation of scientific article at [2026 Conference on Precision Electromagnetic Measurements (CPEM)](https://cpem2026.com) in Madrid, Spain.

Issues and caveats
------------------

1. Thermal coefficient and humidity coefficient contributors are not removed from the long-term drift data.

2. Temperature coefficient measurements were done based on long-scale DMM setup with larger uncertainties, compared to long-term drift array setup.

3. Only three boards with older ADR1001 chips were used in initial study. More to come later.
