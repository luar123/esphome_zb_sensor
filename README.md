# ESP32-H2 Zigbee

## Zigbee based temperature/humidity sensor

ESPHome Zigbee sensor connected to [AHT10 Temperature+Humidity Sensor](https://next.esphome.io/components/sensor/aht10).

### Build ESPHome Zigbee sensor

* We will build [ZB_sensor.yaml](ZB_sensor.yaml) file.
* Check [Getting Started with the ESPHome Command Line](https://esphome.io/guides/getting_started_command_line.html) tutorial to setup your dev environment.

**Steps**
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
