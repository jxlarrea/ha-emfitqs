# Emfit QS Sleep Tracker Component for Home Assistant

This component provides real-time data polled directly from Emfit QS Sleep Tracker devices. Useful for automations based on bed presence and sleep detection (via heart rate bpm levels).

![Sensor Card](https://i.imgur.com/vGzT1Ko.jpg)

**NOTE:** This component has only been tested with Emfit QS firmware version 120.2.2.1.


### Supported Features
* Bed Presence binary sensor
* Time in Bed (seconds)
* Heart Rate BPM sensor
* Respiratory Rate sensor
* Activity Level sensor

**IMPORTANT:** Your Emfit QS device must be accessible by Home Assistant on your local area network.


## Installation

### HACS Installation

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg?style=for-the-badge)](https://github.com/custom-components/hacs)
 This repository is part of the default HACS store. Search for the "Emfit QS Sleep Tracker" component in HACS and install it from there.

### Manual Installation

Copy the `custom_components/ha-emfitqs` directory into your `/config/custom_components` directory.



## Component Configuration

Add the following to your `configuration.yaml` file:

```yaml
emfitqs:

sensor:
  - platform: emfitqs
    host: 192.168.1.x # Replace with your Emfit QS device IP Address.
    scan_interval: 10
    resources:
      - heart_rate
      - respiratory_rate
      - activity_level
      - seconds_in_bed

binary_sensor:
  - platform: emfitqs
    host: 192.168.1.x # Replace with your Emfit QS device IP Address.
    scan_interval: 10
    monitored_conditions:
      - bed_presence
```


### Sensor Resources & Monitored Conditions

| Name  | Type | Description |
| ----- | ---- | ----------- |
| bed_presence | `binary_sensor` | Bed presence |
| heart_rate | `sensor` | Heart rate (BPM) |
| respiratory_rate | `sensor` | Respiratory rate (BPM) |
| activity_level | `sensor` | Activity level |
| seconds_in_bed | `sensor` | Number of seconds in bed |


**NOTE:** In Home Assistant, the component sensor names include the device serial number, for example `binary_sensor.emfitqs_012345_bed_presence` and `sensor.emfitqs_012345_heart_rate` where "012345" is the device serial numer. This allows you to add multiple entries in your config file.
