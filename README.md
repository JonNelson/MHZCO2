
[![Arduino CI](https://github.com/RobTillaart/MHZCO2/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
[![Arduino-lint](https://github.com/RobTillaart/MHZCO2/actions/workflows/arduino-lint.yml/badge.svg)](https://github.com/RobTillaart/MHZCO2/actions/workflows/arduino-lint.yml)
[![JSON check](https://github.com/RobTillaart/MHZCO2/actions/workflows/jsoncheck.yml/badge.svg)](https://github.com/RobTillaart/MHZCO2/actions/workflows/jsoncheck.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobTillaart/MHZCO2/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/RobTillaart/MHZCO2.svg?maxAge=3600)](https://github.com/RobTillaart/MHZCO2/releases)


# MHZCO2

Arduino Library for MHZ series CO2 sensors.


## Description

The MHZCO2 is an experimental library for the MHZ19B CO2 sensor with a Serial (RS232-TTL) interface and compatibles.

The library offers a base class and derived classes to prepare for specific functionality.
The base class is based upon the MHZ19B specification. This might change in the future as compatibles might differ on detail.

Reference: user manual MHZ129B 2019-04-25 version 1.4 


#### Compatibles

This list is not verified although these devices should be compatible based upon datasheet.

|  type      | precision  |  notes  |
|:-----------|:----------:|:--------|
|  MHZ1311A  | 50ppm + 5% | energy saving version
|  MHZ19     | 50ppm + 5% | 
|  MHZ19B    | 50ppm + 3% | test device
|  MHZ19C    | 50ppm + 5% | 
|  MHZ19D    | 50ppm + 5% | 
|  MHZ19E    | 50ppm + 5% |
|  MTP40F    |            |

Note: The calibration of the MHZ1311A is different than MHZ19x series

If there are compatible devices missing in this list, please let me know.

#### Links

- https://emariete.com/en/sensor-co2-mh-z19b/
- https://emariete.com/en/sensor-co2-low-consumption-mh-z1311a-winsen/
- https://revspace.nl/MHZ19


## Connection

- check datasheet of your sensor.


## Interface

#### Constructor

- **MHZCO2()** base class constructor.
- **MHZ19()** constructor. Also 19B,C,D,E
- **MTP40F()** constructor.
- **void begin(Stream \* str)** set the Serial port to use, e.g Serial1.
- **uint32_t uptime()** returns milliseconds since 'instantiation'.


#### Range

- **void setPPM(uint16_t PPM)** PPM = 2000, 5000, 10000
- **uint16_t getPPM()** returns (cached) PPM value


#### Measure

- **int measure()** workhorse, send command to read the sensor.
- **uint32_t lastMeasurement()** timestamp in millis of last measurement
- **int getCO2()** returns CO2 PPM last measurement.
- **int getTemperature()** returns temperature last measurement.
- **int getAccuracy()** returns accuracy last measurement.
- **int getMinCO2()** returns minCO2 last measurement.

The latter two might not be supported by all MH sensors.

#### Calibration

**WARNING:** use with care, read the datasheet as these commands may disrupt your sensor.

- **void calibrateZero()** Only use when sensor is at least 30 minutes in **400** PPM environment.
- **void calibrateSpan(uint16_t span)** Only use when sensor is at least 30 minutes in **2000** PPM environment.
- **void calibrateAuto(bool mode = true)**


## Future

#### Must
- improve documentation
- buy hardware MHZ19B / MHZ19C
- test with hardware
- verify checksum
- verify timeout

#### Should 
- plotter example
- check 3000 PPM

#### Could
- extend unit tests
- add type info for derived classes?
- save RAM? possible?

#### Won't

