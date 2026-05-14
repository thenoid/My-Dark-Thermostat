# My "Dark Thermostat" Config

My custom multi-card configuration using Dark Thermostat card for my Nest Thermostat.

![image](https://user-images.githubusercontent.com/49846893/202269236-fb192ab6-2408-492f-ad70-48f9a14e6023.png)

![image](https://user-images.githubusercontent.com/49846893/202269558-de8d2062-2676-4dad-8a66-4575ff07a4b2.png)

## Modern low-dependency option

This branch adds a modernized option for people who want the same basic thermostat/schedule workflow with fewer custom frontend dependencies.

Use these files:

- `modern_lovelace_raw_config.yaml`
- `modern_sensors.yaml`
- `MODERNIZATION.md`

The modern dashboard only requires:

- [custom:scheduler-card](https://github.com/nielsfaber/scheduler-card)
- [HACS Scheduler Component](https://github.com/nielsfaber/scheduler-component)

Everything else uses built-in Home Assistant dashboard cards.

Replace this entity with your thermostat:

```yaml
climate.living_room
```

For example:

```yaml
climate.nest_3rd
```

## Original dashboard

The original dashboard is still available in `lovelace_raw_config.yaml`.

Additional components required by the original dashboard:

- [browser-mod](https://github.com/thomasloven/hass-browser_mod)
- [card-mod](https://github.com/thomasloven/lovelace-card-mod)
- [custom:button-card](https://github.com/custom-cards/button-card)
- [custom:popup-card](https://github.com/thomasloven/lovelace-popup-card)
- [custom:scheduler-card](https://github.com/nielsfaber/scheduler-card)
- [custom:thermostat-dark-card](https://github.com/ciotlosm/lovelace-thermostat-dark-card)
- [custom:vertical-stack-in-card](https://github.com/ofekashery/vertical-stack-in-card)
- [HACS Scheduler Component](https://github.com/nielsfaber/scheduler-component)

Thermostat: `climate.living_room` from the Nest integration.

Custom sensors used by the original dashboard:

- `nest_eco_high`
- `nest_eco_low`
- `nest_eco_temp`
- `nest_heating_runtime`
- `nest_humidity`
- `nest_hvac_action`
- `nest_preset_mode`
- `nest_room_hvac_mode`
- `nest_setpoint`
- `nest_temperature`
- `sensor.nest_time_to_temp_message`
- `sensor.outside_weather_temperature`

Copy the code from `lovelace_raw_config.yaml` and add it as a new view in your `ui.lovelace.yaml` or your Lovelace dashboard raw configuration.

## Template sensors

`sensors.yaml` is formatted for the template integration using modern configuration variables.

See [Modern Configuration Variables](https://www.home-assistant.io/integrations/template/#configuration-variables/).

Sample `configuration.yaml` entry:

```yaml
template:
  - sensor:
      - name: "Nest Heating Runtime"
        unique_id: nest_heat_runtime
        unit_of_measurement: "seconds"
        state: "{{ state_attr('climate.living_room', 'elapsed_seconds') | float(0) }}"
```

To use legacy format templating, more extensive changes are required for variable names and formatting.

See [Legacy Configuration Variables](https://www.home-assistant.io/integrations/template/#configuration-variables/).
