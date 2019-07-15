# ha-emfitqs

### Emfit QS Sleep Tracker Component for Home Assistant.

This component provides sensors polled directly from Emfit QS Sleep Tracker devices. Useful for automations based on bed presence and sleep detection (via heart rate bpm levels)

**NOTE:** This component has only been tested with Emfit QS firmware version 120.2.2.1.

![Sensor Card](https://i.imgur.com/rlsxNTC.jpg)

## Supported Features
* Bed Presence binary sensor
* Time in Bed (seconds)
* Heart Rate BPM sensor
* Breath Rate sensor
* Activity Level sensor

**IMPORTANT:** Your Emfit QS device must be accessible by Home Assistant on your local area network.

## Installation

Copy the `ha-emfitqs` directory into your `/config/custom_components` directory.

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
      - breath_rate
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
| breath_rate | `sensor` | Breath rate (BPM) |
| activity_level | `sensor` | Activity level |
| seconds_in_bed | `sensor` | Number of seconds in bed |


**NOTE:** In Home Assistant, the component sensor names include the device serial number, for example `binary_sensor.emfitqs_012345_bed_presence` and `sensor.emfitqs_012345_heart_rate` where "012345" is the device serial. This allows you to add multiple entries in your config file.
