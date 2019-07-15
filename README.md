# ha-emfitqs

### Emfit QS Sleep Tracker Component for Home Assistant.

This component provides data pulled locally from Emfit QS Sleep Tracker devices. Useful for automations based on bed presence and sleep detection (via heart rate bpm levels)

**NOTE:** This components has only been tested with Emfit QS firmware version 120.2.2.1.

## Supported Features
* Bed Presence binary sensor
* Time in Bed (seconds)
* Heart Rate BPM sensor
* Breath Rate sensor
* Activity Level sensor

![Sensor Card](https://i.imgur.com/UcDtBqY.png =393x244)

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
      - hr
      - rr
      - act
      - bed

binary_sensor:
  - platform: emfitqs
    host: 192.168.1.x # Replace with your Emfit QS device IP Address.
    scan_interval: 10
    monitored_conditions:
      - pres
```

### Sensor Resources & Monitored Conditions

| Name  | Type | Description |
| ----- | ---- | ----------- |
| pres | `binary_sensor` | Bed presence |
| hr | `sensor` | Heart rate (BPM) |
| rr | `sensor` | Breath rate (BPM) |
| act | `sensor` | Activity level |
| bed | `sensor` | Number of seconds in bed |


**NOTE:** In Home Assistant, the component sensor names will append the device serial number, for example `binary_sensor.emfitqs_012345_presence` and `sensor.emfitqs_012345_heart_rate` where "012345" will be your device serial number. This allows you to add multiple entries in your config file.
