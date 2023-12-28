# swiss-stationboard

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/custom-components/hacs)

Custom lovelace card for Home Assistant Lovelace UI.
Swiss public transport stationboard. Shows connections from one or multiple stations.

![Stationboard "Schüpfen"](https://github.com/Narekushia/lovelace-swiss-stationboard/blob/main/img/stationboard-1.png?raw=true "Stationboard Schüpfen")

## Installation

### Requirement

_Requires https://github.com/neuhausf/swiss-public-transport-mod to be installed first._

### HACS Installation

- Go to HACS
- Add a custom repo: https://github.com/Narekushia/lovelace-swiss-stationboard
- Install the lovelace card

## Configuration

Add a new custom card to your Dashboard:

```YAML
type: custom:swiss-stationboard
name: Abfahrt
hide_title: true
category: B|^ICE$|S
platform_name: Gl.
entity:
  - sensor.schupfen
line_color:
  - name: S31
    background_color: "#ada431"
    color: "#fff"
```

### Card settings

| Name | Type | Default | Description |
| ---- | :---: | :---: | ----------- |
| `departure_offset` | number | `0` | An optional number of X minutes. If greater than zero minutes, it hides all next departures within those minutes.  Note that the filtering is on the frontend only - so this could lead to an empty stationboard if the sensor doesn't provide enough journeys (`limit` setting of the [stationboard-sensor](https://github.com/neuhausf/swiss-public-transport-mod)) |
| `departure_countdown` | number | `15` | An optional number of minutes. All departures within this time window will have a countdown displayed onscreen. |
| `show_seconds` | boolean | `false` | If true, will show seconds in addition to minutes within the countdown. |
| `entity` ***(required)*** | | | which entity (from *swiss-public-transport-mod*) to use as the data source. |
| `hide_title` | boolean | `false` | Hides the title if true. |
| `category` | string | | Regular expression to filter by categories (S-train, Bus, ICE, ...).  i.e. to include multiple categories use the OR operator: `category: B|^ICE$|S` |
| `show_last_changed` | boolean | `false` | If true, shows the last time that the underlying data changed. |
| `minutes_label` | string | `min` or `mins` | The string denoting minutes in the ETA field.  Note the whitespace before the word — if your chosen string does not have whitespace, the string will be stuck to the number. |
| `seconds_label` | string | `″` | The string denoting seconds in the ETA field. Note the whitespace before the word — if your chosen string does not have whitespace, the string will be stuck to the number. |
| `line_color` | list |  | Optional css styling for specific lines (for example, S-Bahn color lines) |

## Privacy

This integration uses:

- https://github.com/agners/swiss-public-transport-card
- the changes made in the pull request by @agners: https://github.com/home-assistant/core/pull/30715
- and some own code to adapt the visualization.
