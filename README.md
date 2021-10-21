
# SPI Host Driver Example for ESP32-S3-USB-OTG (including S2)

Original code of example: https://github.com/espressif/esp-idf/tree/master/examples/peripherals/spi_master/lcd

## How to Use Example

### Hardware Required

* Hardware: https://www.espressif.com/en/products/devkits - ESP32-S3-USB-OTG with SPI LCD
* Driver: ST7789VW
* Example of driver: https://github.com/espressif/esp-iot-solution/blob/master/components/display/screen/controller_driver/st7789/st7789.c

Connection :

### Build and Flash

Run:

```
idf.py set-target esps2
idf.py build flash monitor
```

(To exit the serial monitor, type ``Ctrl-]``.)


See the [Getting Started Guide](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html) for full steps to configure and use ESP-IDF to build projects.

## Example Output

The board does not have support for reading values from SPI, so it's not possible to detect display ID from SPI.

On ESP-WROVER-KIT there will be:

```
kconfig: force CONFIG_LCD_TYPE_ST7789V.
LCD ST7789V initialization.
```

At the meantime `ESP32` will be displayed on the connected LCD screen.


## Changes from original example

Following changes were made to original LCD example:
```
#elif defined CONFIG_IDF_TARGET_ESP32S2
#define LCD_HOST    SPI2_HOST

#define PIN_NUM_MOSI 7
#define PIN_NUM_CLK  6
#define PIN_NUM_CS   5

#define PIN_NUM_DC   4
#define PIN_NUM_RST  8
#define PIN_NUM_BCKL 9
```

The important trick is to invert backlight value from original code to 1:

```
gpio_set_level(PIN_NUM_BCKL, 1);
```

