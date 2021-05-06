# Hello BMP280

This example demonstrates how to read temperature data from the BMP280 temperature sensor board.
We will use [I2C](https://en.wikipedia.org/wiki/I%C2%B2C) protocol to connect a sensor board to our Nerves target device (e.g., Raspbery Pi).

## Nerves target

The explanation below assumes a [Raspberry Pi Zero W](https://www.raspberrypi.org/products/raspberry-pi-zero-w/) as a target device but other [Nerves targets](https://hexdocs.pm/nerves/targets.html) should work as well.

[![](https://www.raspberrypi.org/homepage-9df4b/static/7ee0b4ceafeccddd8aef917cc818990d/ae23f/9371b539-77d4-47f1-b89b-aa65b23c9833_RPI%2BZERO%2BW%2BANGLE%2B2%2BREFRESH_.jpg)](https://www.raspberrypi.org/products/raspberry-pi-zero-w/)

## Sensor board

The [Bosch BMP280 sensor](https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/) itself is so tiny that it might be difficult to handle but some electronics components manufactureres mount it on a [breakout board](https://en.wikipedia.org/wiki/Printed_circuit_board) for our convenience, which is what we look for. Do [Google search by "BMP280 breakout board"](https://www.google.com/search?q=bmp280+breakout+board) and you will find something like [Adafruit BMP280 Sensor board](https://www.adafruit.com/product/2651).

[![](https://cdn-shop.adafruit.com/970x728/2651-07.jpg)](https://www.adafruit.com/product/2651)


You can alternatively use [BME280](https://www.bosch-sensortec.com/products/environmental-sensors/humidity-sensors-bme280/) or [BME680](https://www.bosch-sensortec.com/products/environmental-sensors/gas-sensors-bme680/) since the [elixir-sensors/bmp280](https://github.com/elixir-sensors/bmp280) library supports them.

## Wiring

Roughly speaking, there are typically two ways to hook up a sensor to our Nerves target.

### A: Pin header

If you already have a [soldering iron](https://en.wikipedia.org/wiki/Soldering_iron) and enjoy using it, this is the go-to option. Even if you have not already, soldering can be fun. This option only requires a [pin header](https://en.wikipedia.org/wiki/Pin_header) and 4 [jumper wires](https://en.wikipedia.org/wiki/Jump_wire)

[![](https://cdn-learn.adafruit.com/assets/assets/000/026/855/large1024/sensors_2651_kit_ORIG.jpg?1438369482)](https://learn.adafruit.com/adafruit-bmp280-barometric-pressure-plus-temperature-sensor-breakout/assembly)

[![](https://cdn-shop.adafruit.com/970x728/1950-02.jpg)](https://www.adafruit.com/product/1950)

[I2C](https://en.wikipedia.org/wiki/I%C2%B2C) protocol uses 4 pins. It is confusing but different products may name the  pins differently.

| Target (I2C controller) | Sensor (I2C peripheral) | Description                       |
| ----------------------- | ----------------------- | --------------------------------- |
| 3.3V                    | Vin                     | power                             |
| GND                     | GND                     | common ground for power and logic |
| I2C SDA (GPIO 2)        | SDA                     | I2C data                          |
| I2C SCL (GPIO 3)        | SCL                     | I2C clock                         |

[![](https://camo.githubusercontent.com/0b6abcc834c63e6843846a3d04ea29618d91b160509745783aeea257d9f2b036/68747470733a2f2f70696e6f75742e78797a2f7265736f75726365732f7261737062657272792d70692d70696e6f75742e706e67)](https://pinout.xyz/pinout/)

### B: Qwiic Connect System etc

Taking advantage of [Qwiic Connect System](https://www.sparkfun.com/qwiic) or similar system, we can remove the need for the soldering. One tradeoff is that we need to get an extra board like [Qwiic HAT for Raspberry Pi](https://www.adafruit.com/product/4688) and special wires.

[![](https://cdn-shop.adafruit.com/970x728/4688-00.jpg)](https://www.adafruit.com/product/4688)

[![](https://cdn-shop.adafruit.com/970x728/4399-00.jpg)](https://www.adafruit.com/product/4399)

## How to use this repository

Please see the main [Nerves installation
docs](https://hexdocs.pm/nerves/installation.html) if you haven't used Nerves
before.

### Go to the `hello_bmp280` directory

```shell
cd hello_bmp280
```

### Set up your build environment

Specify the [Nerves target hardware](https://hexdocs.pm/nerves/targets.html).

```shell
export MIX_TARGET=rpi0
```

Specify the WiFi name and password in order to hard-code WiFi credentials in the firmware.

```shell
export WIFI_SSID=your_wifi_name
export WIFI_PSK=your_wifi_password
```

If you do not have WiFi available, you can alternatively connect the target board to your host machine (e.g., your laptop) using a USB cable.

**Install dependencies**

```shell
mix deps.get
```

**build firmware**

```shell
mix firmware
```

**burn firmware to an [SD card](https://en.wikipedia.org/wiki/SD_card)**

```shell
mix firmware.burn
```

**Insert the SD card into your target board and power up**

**Wait for the target board to finish booting**

**SSH into the target board**

```shell
ssh nerves.local
```

Once you shell into your target board, you can play around with the [elixir-sensors/bmp280](https://github.com/elixir-sensors/bmp280) library.

![](https://user-images.githubusercontent.com/7563926/117234457-0bb4f980-adf3-11eb-8b2d-f3fa7afc71d2.png)

## Learn more

- Official docs: https://hexdocs.pm/nerves/getting-started.html
- Official website: https://nerves-project.org/
- Forum: https://elixirforum.com/c/nerves-forum
- Discussion Slack elixir-lang #nerves ([Invite](https://elixir-slackin.herokuapp.com/))
- Source: https://github.com/nerves-project/nerves
