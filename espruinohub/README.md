# About

This is an unofficial [EspruinoHub](https://github.com/espruino/EspruinoHub) addon to Hass.io

# Configuration

To conserve CPU time, you can limit the number of monitored bluetooth devices by explicitly listing them in the configuration options:

```json
{
  "known_devices": {
    "12:34:b6:50:5f:11": "dev",
    "d1:44:1e322:4b:e3": "dev2"
  },
  "only_known_devices": true,
  "http_port": 1888
}
```
