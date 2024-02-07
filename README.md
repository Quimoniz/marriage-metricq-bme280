# BME280 into MetricQ

Getting Humidity, Temperature and Pressure into MetricQ.


## The Big Picture

![Sensor](img/bme280-to-metricq.png)

## Hardware

There's a variety of sensors for Measuring Humidity. A prerequisite for measuring `relative humidity` is information on `temperature`. There's a wide variety of sensors for this purpose, which shall be omitted for brevity purposes here.


### BME280

Bosch's sensortec series provides us with the [BME280 sensor](https://www.bosch-sensortec.com/products/environmental-sensors/humidity-sensors-bme280/). It can mesaure:
- `relative humidity`
- `temperature`
- `barometric pressure`

Unless you are very capable at miniature soldering 8 pins with a distance of just 0.55 mm between the connection pads, you might want to fetch some BME280 pre-soldered on a PCB[*] from some electronics retailer.

Similar sensors: GY-21, HTU21D/SHT21 (Note: adjust the I²C address for those sensors)

Further Reading:
- [BME280 Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf)
- [BME280 Mounting Instructions](https://www.bosch-sensortec.com/media/boschsensortec/downloads/handling_soldering_mounting_instructions/bst-bme280-hs006.pdf)


[*] PCB is shorthand for Printed Circuit Board

### Raspberry Pi

Here we are using Raspberry Pi 4 with Argon One V.2 housing here. However the BME280 sensor can be connected to even a simple Raspberry Pi 1 A.

Follow some other Online tutorial on how to setup your raspberry pi including putting some debian-ish operating system on it.

### I2C Introduction

For brevity purposes we'll assume you got some BME280 sensor on a PCB providing [I²C](https://en.wikipedia.org/wiki/I%C2%B2C) on four Pins. We will not concern ourselves with SPI here, because it requires two more pins to work and I²C's frequency/Baud-rate is far far sufficient for reading a few small numbers.

Your sensor and PCB might look a little something like this:
![BME280](img/bme280-detail.png)

Do note the four pins here:
- Vin: Voltage Input (i.e. Polarity: Positive (+); 1.71 - 3.6 volt[*])
- Gnd: Ground (i.e. Polarity: Negative (-))
- SCl: Serial Clock
- SDa: Serial Data

[*] Note on the Voltage: the metallic looking 2.5 x 2.5 mm sensor by Bosch would be destroyed with a voltage higher than 3.6 V. However, this particular PCB comes with a series of Resistors and Capacitors which allow us to run 5.0 - 5.2 V (provided by the Raspberry Pi) to the PCB without problems.

### I2C wiring.

Simply run the four aforementioned Pins to the Raspberry Pi into the respective Ports. For simplicity see this table here on the Raspberry Pi pinout:

| Description    | Pin | Pin | Description    |
|----------------|-----|-----|----------------|
| 3.3 Volt       |   1 |   2 | 5 Volt         |
| **I2C1 SDA/GPIO2** |   3 |   4 | **5 Volt**         |
| **I2C1 SCL/GPIO3** |   5 |   6 | **Ground**         |
| GPIO4/GPCLK0   |   7 |   8 | GPIO14/UART TX |
| Ground         |   9 |  10 | GPIO15/UART RX |
| GPIO17         |  11 |  12 | GPIO18/PCM CLK |
| ...            | ... | ... | ...            |

(for a complete reference see [the Pinout.xyz site](https://pinout.xyz/))

I marked the Pins 3, 4, 5 and 6 which I've been using. For providing 3 Volts instead, you might choose to use Pin 1 (3.3 Volt) instead of Pin 4.

### Completed Hardware Setup

![Raspberry Pi 4 in Argon One housing with connected BME280 sensor](img/metricq-bme280_small.jpg)

(See [here for a high resolution image](img/metricq-bme280.jpg))

## Software

So, you got all the hardware ready, now you want to install the pre-requisites for running a MetricQ-Source.

Note: a **MetricQ-Source** (i.e. some sensor) creates data which can be sent to a **MetricQ-Server** to be thereafter consumed by a **MetricQ-Sink** (e.g. a database).

### Software-Pre-Requisites
apt install...
git clone....

https://github.com/metricq/metricq-source-example

### Programming
....
