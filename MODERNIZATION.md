# Modernization Notes

This repo originally recreated a Nest-like thermostat dashboard with several custom Lovelace cards. The new `modern_lovelace_raw_config.yaml` keeps the same basic idea but reduces the dependency stack.

## Original custom dependencies

The original dashboard required:

- `browser-mod`
- `card-mod`
- `custom:button-card`
- `custom:popup-card`
- `custom:scheduler-card`
- `custom:thermostat-dark-card`
- `custom:vertical-stack-in-card`
- `scheduler-component`

## Modern minimal stack

The modern dashboard only requires:

- `scheduler-component`
- `scheduler-card`

Everything else uses core Home Assistant dashboard cards:

- `thermostat`
- `markdown`
- `entities`
- `grid`
- `button`
- `history-graph`

## What changed

- Replaced the archived/old popup workflow with a simple inline scheduler card.
- Replaced `thermostat-dark-card` with Home Assistant's built-in thermostat card.
- Removed `button-card`, `card-mod`, `popup-card`, `browser-mod`, and `vertical-stack-in-card` from the modern dashboard path.
- Added `modern_sensors.yaml` with safer template sensors and fewer hard-coded Celsius assumptions.

## How to use

1. Install HACS `scheduler-component` and `scheduler-card`.
2. Copy `modern_sensors.yaml` into your Home Assistant configuration or package setup.
3. Copy `modern_lovelace_raw_config.yaml` into a dashboard raw configuration.
4. Replace all instances of `climate.living_room` with your thermostat entity.
5. Replace outside/humidity source sensors if needed.

For example:

```yaml
climate.living_room -> climate.nest_3rd
```

## Scheduling model

Use scheduler-card to create thermostat setpoint rules, for example:

- Monday-Friday 08:00: set heat target to 74
- Monday-Friday 21:00: set heat target to 68
- Saturday-Sunday 08:00: set heat target to 74
- Saturday-Sunday 20:00: set heat target to 68

This keeps the Nest/thermostat entity as the HVAC controller while Home Assistant owns the visible schedule UI.
