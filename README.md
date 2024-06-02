# linuxlaptopstat2mqtt

This is a docker container that sends various system stats via MQTT to a broker. The intended recipient is Home Assistant's MQTT integration.

## Building the container

```bash
docker build . -t linuxlaptopstat2mqtt
```

## Running the container

If you are planning to use this with Home Assistant, setup the MQTT addon beforehand: https://www.home-assistant.io/integrations/mqtt/

```bash
  docker run -d \
  --name=linuxlaptopstat2mqtt \
  -e MQTT_BROKER_HOST=yourmqtthost \
  -e MQTT_BROKER_PORT=1883 \
  -e MQTT_BROKER_USERNAME=yourmqttusername \
  -e MQTT_BROKER_PASSWORD=yourmqttpassword \
  -e DEVICE_NAME=laptop \
  --restart unless-stopped \
  linuxlaptopstats2mqtt
```

## Adding the sensors to Home Assistant

TODO: implement service discovery. Currently this has to be done as follows:

Add the following to your `configuration.yaml` configuration file (replace `laptop` in the `state_topic` definitions with whatever you gave as `DEVICE_NAME`)

```bash
mqtt:
  sensor:
    - name: "Battery Percentage"
      state_topic: "homeassistant/sensor/laptop_battery/state"
      unique_id: "laptop_battery"
      icon: mdi:battery
      unit_of_measurement: "%"
      device:
        identifiers:
          - laptop
        manufacturer: "HP"
        model: "Pavillion-X360"
        name: "Jash Laptop"
    - name: "Battery Plugged"
      state_topic: "homeassistant/sensor/laptop_battery_status/state"
      unique_id: "laptop_battery_plugged"
      icon: mdi:battery-sync-outline
      device:
        identifiers:
          - laptop
        manufacturer: "HP"
        model: "Pavillion-X360"
        name: "Jash Laptop"
    - name: "CPU Percentage"
      state_topic: "homeassistant/sensor/laptop_cpu_percent/state"
      unique_id: "laptop_cpu_percent"
      icon: mdi:cpu-64-bit
      unit_of_measurement: "%"
      device:
        identifiers:
          - laptop
        manufacturer: "HP"
        model: "Pavillion-X360"
        name: "Jash Laptop"
    - name: "Total Storage"
      state_topic: "homeassistant/sensor/laptop_storage_total/state"
      unique_id: "laptop_storage_total"
      icon: mdi:harddisk
      unit_of_measurement: Gb
      device:
        identifiers:
          - laptop
        manufacturer: "HP"
        model: "Pavillion-X360"
        name: "Jash Laptop"
    - name: "Used Storage"
      state_topic: "homeassistant/sensor/laptop_storage_used/state"
      unique_id: "laptop_storage_used"
      icon: mdi:harddisk-remove
      unit_of_measurement: Gb
      device:
        identifiers:
          - laptop
        manufacturer: "HP"
        model: "Pavillion-X360"
        name: "Jash Laptop"
    - name: "Free Storage"
      state_topic: "homeassistant/sensor/laptop_storage_free/state"
      unique_id: "laptop_storage_free"
      icon: mdi:harddisk-plus
      unit_of_measurement: Gb
      device:
        identifiers:
          - laptop
        manufacturer: "HP"
        model: "Pavillion-X360"
        name: "Jash Laptop"
```
