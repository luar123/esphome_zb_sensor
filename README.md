# ESPHome Zigbee sensor using ESP32-H2

ESPHome example of a zigbee sensor.

Note that the Zigbee part in this project is currently hardcoded and included as a custom component including a task. (Changing this to an external component with more configuration possibilities would be the next step).

## Zigbee based temperature and humidity sensor

ESPHome Zigbee sensor connected to [AHT10 Temperature+Humidity Sensor](https://next.esphome.io/components/sensor/aht10).

### Hardware Required

* One development board with ESP32-H2 SoC acting as Zigbee end-device (that you will load ESPHome with the zb-sensor config to).
  * For example the official [ESP32-H2-DevKitM-1](https://docs.espressif.com/projects/espressif-esp-dev-kits/en/latest/esp32h2/esp32-h2-devkitm-1/user_guide.html) development kit board.
* [AHT10/AHT20/AHT30 Temperature+Humidity Sensor](https://next.esphome.io/components/sensor/aht10) connected to I2C pins (SDA: 12, SCL: 22).
* A USB cable for power supply and programming.
* (Optional) A USB-C cable to get ESP32 logs from the UART USB port (UART0).

### Build ESPHome Zigbee sensor

* We will build [ZB_sensor.yaml](ZB_sensor.yaml) file.
* Check [Getting Started with the ESPHome Command Line](https://esphome.io/guides/getting_started_command_line.html) tutorial to setup your dev environment.

**Steps**
* Change the [AHTx0 variant](https://esphome.io/components/sensor/aht10.html) according to the sensor you have in [ZB_sensor.yaml](ZB_sensor.yaml)
* Build with `esphome run ZB_sensor.yaml` command will fail
* Copy [idf_component.yml](idf_component.yml) to `.esphome/build/zb-sensor/src/`
* Add the following 4 lines to the `.esphome/build/zb-sensor/sdkconfig.zb-sensor` file
```ini
CONFIG_ZB_ENABLED=y
CONFIG_ZB_RADIO_NATIVE=y
CONFIG_ZB_ZED=y
ZB_ED_ROLE=y
```
* Build with `esphome run ZB_sensor.yaml` command
* Firmware will be uploaded automatically to the ESP32-H2 board

### Notes
* There is a bug in [ESPHome 2024.3.0](https://esphome.io/changelog/2024.3.0.html). Deactivate the logger to make it build.
  * Check issue [2024.3.0 fails to compile in logger component #5612](https://github.com/esphome/issues/issues/5612).
  * This should be fixed by esphome/esphome#6323 which should be included in ESPHome 2024.3.1.
* If library versions in [idf_component.yml](idf_component.yml) are changed, copy the file to `.esphome/build/zb-sensor/src/` again and delete `.esphome/build/zb-sensor/.pioenvs`.

## External documentation and reference

Note! The official documentation and reference examples for the ESP Zigbee SDK can currently be obtained from Espressif:

 - [ESP32 Zigbee SDK Programming Guide](https://docs.espressif.com/projects/esp-zigbee-sdk/en/latest/esp32/)
   - [ESP32-H2 Application User Guide](https://docs.espressif.com/projects/esp-zigbee-sdk/en/latest/esp32h2/application.html)
   - [ESP32-C6 Application User Guide](https://docs.espressif.com/projects/esp-zigbee-sdk/en/latest/esp32c6/application.html)
- [ESP-Zigbee-SDK Github repo](https://github.com/espressif/esp-zigbee-sdk)
  - [ESP-Zigbee-SDK examples](https://github.com/espressif/esp-zigbee-sdk/tree/main/examples/)
    - [Zigbee HA Example](https://github.com/espressif/esp-zigbee-sdk/tree/main/examples/esp_zigbee_HA_sample)
      - [Zigbee HA Light Bulb example](https://github.com/espressif/esp-zigbee-sdk/tree/main/examples/esp_zigbee_HA_sample/HA_on_off_light)
      - [Zigbee HA temperature sensor example](https://github.com/espressif/esp-zigbee-sdk/tree/main/examples/esp_zigbee_HA_sample/HA_temperature_sensor)
      - [Zigbee HA thermostat example](https://github.com/espressif/esp-zigbee-sdk/tree/main/examples/esp_zigbee_HA_sample/HA_thermostat)

## How to contribute

If looking to contribute to this project then suggest follow steps in these guides + look at issues in Espressif's ESP Zigbee SDK repoository:

- https://github.com/espressif/esp-zigbee-sdk/issues
- https://github.com/firstcontributions/first-contributions/blob/master/README.md
- https://github.com/firstcontributions/first-contributions/blob/master/github-desktop-tutorial.md
