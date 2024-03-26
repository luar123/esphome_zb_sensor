esp32-h2 based temperatur/huminity sensor.

Build:
* esphome run ZB_sensor (will fail)
* copy [idf_component.yml](idf_component.yml) to .esphome/build/zb-sensor/src/
* copy CONFIG_ZB_ENABLED=y, CONFIG_ZB_RADIO_NATIVE=y, CONFIG_ZB_ZED=y, and ZB_ED_ROLE=y from sdkconfig.zb_sensor.esphomeinternal to sdkconfig.zb-sensor (in .esphome/build/zb-sensor/)
* esphome run ZB_sensor

Notes:
* There is a bug in [ESPHome 2024.3.0](https://esphome.io/changelog/2024.3.0.html). Deactivate the logger to make it build.
