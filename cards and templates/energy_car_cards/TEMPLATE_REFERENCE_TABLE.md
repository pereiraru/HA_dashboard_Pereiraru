# 📊 Button-Card Templates - Complete Reference Table

## All 18 Templates Available

---

| Template Name | Functionalities | Variables (Customizable in Card) | Examples of Customization |
|--------------|-----------------|----------------------------------|---------------------------|
| **setup** | Base template with unavailable state handling, font normalization | None (used as parent template) | Used as foundation for other templates |
| **button_template** | Highly customizable button with custom icons, colors, and states | `icon2` - Top-right indicator icon<br>`icon_on` - Icon when ON<br>`icon_off` - Icon when OFF<br>`state_on` - State considered "on"<br>`state_off` - State considered "off"<br>`background_color_on` - Background when ON<br>`background_color_off` - Background when OFF<br>`color_on` - Text color when ON<br>`color_off` - Text color when OFF | ```yaml<br>variables:<br>  icon_on: mdi:lightbulb<br>  icon_off: mdi:lightbulb-outline<br>  background_color_on: var(--red)<br>  background_color_off: var(--contrast2)<br>``` |
| **navigation_button** | Navigation button with arrow indicator, inherits from button_template | All from button_template PLUS:<br>`navigation_path` - Where to navigate | ```yaml<br>variables:<br>  navigation_path: /lovelace/sala<br>  icon_on: mdi:sofa<br>  background_color_on: var(--blue)<br>``` |
| **switch_template** | Toggle switches with on/off states | `icon_on` - Icon when ON<br>`icon_off` - Icon when OFF<br>`color` - Color when ON (default: purple) | ```yaml<br>variables:<br>  icon_on: mdi:toggle-switch<br>  icon_off: mdi:toggle-switch-off<br>  color: var(--red)<br>``` |
| **climate_card** | Climate control with temp adjustment, humidity, and window sensor | `sensor` - Window/door sensor entity | ```yaml<br>variables:<br>  sensor: binary_sensor.sala_window<br>``` |
| **light_rgb** | RGB lights with color display and brightness slider | None (uses entity attributes automatically) | ```yaml<br>entity: light.rgb_strip<br>name: LED Strip<br>template: light_rgb<br>``` |
| **light_switch** | Simple light on/off toggle | `icon_on` - Icon when ON<br>`icon_off` - Icon when OFF<br>`color` - Color when ON (default: yellow) | ```yaml<br>variables:<br>  icon_on: mdi:lightbulb<br>  icon_off: mdi:lightbulb-outline<br>  color: var(--yellow)<br>``` |
| **mobile_media_player** | Fixed-bottom media player bar with album art, controls, and progress | None (uses entity attributes) | ```yaml<br>entity: media_player.spotify<br>template: mobile_media_player<br>``` |
| **person_card_big** | Large person tracking card with entity picture, home/away status, 3 sensor chips | `sensor1` - First sensor (e.g., battery)<br>`sensor2` - Second sensor (e.g., steps)<br>`sensor3` - Third sensor (e.g., direction) | ```yaml<br>variables:<br>  sensor1: sensor.rui_battery<br>  sensor2: sensor.rui_steps<br>  sensor3: sensor.rui_direction<br>``` |
| **person_card_small** | Compact person tracking with entity picture, home/away badge, 1 sensor | `sensor` - Sensor to display (usually battery) | ```yaml<br>variables:<br>  sensor: sensor.phone_battery<br>``` |
| **room_card** | Room overview with temp/humidity, window sensor, brightness slider when ON | `icon` - Room icon<br>`sensor` - Window sensor<br>`state` - Custom state display template | ```yaml<br>variables:<br>  icon: mdi:sofa<br>  sensor: binary_sensor.sala_window<br>``` |
| **security_card** | Alarm control panel with arm/disarm modes, blink animation when triggered | None (uses alarm entity states) | ```yaml<br>entity: alarm_control_panel.home<br>name: Alarme<br>template: security_card<br>``` |
| **sensor_big** | Large sensor display (129px height) with custom state, icon badge, dynamic colors | `icon_on` - Icon when ON<br>`icon_off` - Icon when OFF<br>`state_on` - State considered "on"<br>`state_off` - State considered "off"<br>`background_color_on` - Background when ON<br>`background_color_off` - Background when OFF<br>`color_on` - Text color when ON<br>`color_off` - Text color when OFF<br>`state` - HTML template for custom display | ```yaml<br>variables:<br>  icon_on: mdi:wifi<br>  icon_off: mdi:wifi-off<br>  background_color_on: var(--green)<br>  background_color_off: var(--red)<br>  state: <Custom HTML><br>``` |
| **sensor_medium** | Medium sensor (56px) with icon circle, numeric value with custom unit | `state` - Custom display template with unit | ```yaml<br>variables:<br>  state: \|<br>    [[[<br>      var st = states[entity.entity_id].state;<br>      var uni = ' kWh';<br>      return `${parseFloat(st).toFixed(1)}<span style="font-size:0.5em;opacity:0.7">${uni}</span>`;<br>    ]]]<br>``` |
| **sensor_small** | Small sensor (56px) text-only, no icon, custom unit display | `state` - Custom display template with unit | ```yaml<br>variables:<br>  state: \|<br>    [[[<br>      return parseFloat(entity.state).toFixed(2) + ' kWh';<br>    ]]]<br>``` |
| **cover_card** | Cover/shutter control with toggle, blue when open, gray when closed, arrow indicator | None (uses cover entity states) | ```yaml<br>entity: cover.sala_estores<br>name: Estores Sala<br>template: cover_card<br>``` |
| **room_header** | Page/section header with large title and subtitle, no background, not clickable | None (just use name & label directly) | ```yaml<br>name: Energia<br>label: Monitorização de consumos<br>template: room_header<br>view_layout:<br>  grid-column: 1 / -1<br>``` |
| **info_card** | Simple info/status display (75px) with icon and large state value | None (just entity, name, icon) | ```yaml<br>entity: sensor.battery<br>name: Bateria<br>icon: mdi:battery<br>template: info_card<br>state_display: \|<br>  [[[<br>    return entity.state + '%';<br>  ]]]<br>``` |

---

## 📋 Common Customizations Across All Templates

### 1. Override Icon
Works on all templates:
```yaml
icon: mdi:your-custom-icon
```

### 2. Custom State Display
Works on most templates:
```yaml
state_display: |
  [[[
    if (entity.state == "on") return "Ligado";
    else return "Desligado";
  ]]]
```

### 3. Custom Label
Works on templates that support labels:
```yaml
label: |
  [[[
    return entity.attributes.temperature + "°C";
  ]]]
```

### 4. Override Colors
Works on all templates:
```yaml
styles:
  card:
    - background: var(--purple)
    - border-radius: 20px
  icon:
    - color: var(--green)
  state:
    - color: var(--yellow)
```

### 5. Grid Layout Override
Works on all templates:
```yaml
view_layout:
  grid-column: span 2  # Make card 2 columns wide
  grid-row: span 2     # Make card 2 rows tall
```

### 6. Custom Tap Action
Works on all templates (except room_header):
```yaml
tap_action:
  action: call-service
  service: light.toggle
  service_data:
    entity_id: light.sala
```

---

## 🎨 Template Categories

### Control Templates (Interactive)
- `button_template` - Generic customizable
- `navigation_button` - Navigate views
- `switch_template` - Toggle on/off
- `light_switch` - Simple light
- `light_rgb` - RGB with slider
- `climate_card` - Climate control
- `cover_card` - Blinds/shutters
- `security_card` - Alarm panel

### Display Templates (Information)
- `sensor_big` - Large status (129px)
- `sensor_medium` - Medium with icon (56px)
- `sensor_small` - Small text only (56px)
- `info_card` - Simple display (75px)
- `room_header` - Section titles

### Special Templates
- `setup` - Base for all templates
- `room_card` - Room overview with controls
- `person_card_big` - Large person tracking
- `person_card_small` - Compact person
- `mobile_media_player` - Media controls

---

## 💡 Quick Examples by Use Case

### Change Light Color When ON
```yaml
- type: custom:button-card
  entity: light.sala
  name: Luz Sala
  template: light_switch
  variables:
    color: var(--blue)  # Blue instead of default yellow
```

### Add Navigation to Room
```yaml
- type: custom:button-card
  entity: light.sala
  name: Sala
  template: navigation_button
  variables:
    navigation_path: /lovelace/sala
    icon_on: mdi:sofa
    background_color_on: var(--green)
```

### Custom Sensor with kWh Display
```yaml
- type: custom:button-card
  entity: sensor.energy_today
  name: Energia Hoje
  icon: mdi:lightning-bolt
  template: sensor_medium
  variables:
    state: |
      [[[
        return parseFloat(entity.state).toFixed(2) + ' kWh';
      ]]]
```

### Add Window Sensor to Climate Card
```yaml
- type: custom:button-card
  entity: climate.ac_sala
  name: AC Sala
  template: climate_card
  variables:
    sensor: binary_sensor.sala_window
```

### Create Page Header
```yaml
- type: custom:button-card
  name: Energia
  label: Monitorização e análise de consumos
  template: room_header
  view_layout:
    grid-column: 1 / -1
```

### Power Monitor with Dynamic Colors
```yaml
- type: custom:button-card
  entity: sensor.server_power
  name: Servidor
  icon: mdi:server
  template: info_card
  state_display: |
    [[[
      return Math.round(entity.state) + " W";
    ]]]
  styles:
    card:
      - background: |
          [[[
            var p = parseFloat(entity.state);
            if (p > 200) return "var(--red)";
            if (p > 100) return "var(--yellow)";
            if (p > 10) return "var(--blue)";
            return "var(--contrast2)";
          ]]]
```

---

## 🔧 Advanced Customization

### Combine Multiple Variables
```yaml
- type: custom:button-card
  entity: binary_sensor.motion
  name: Motion Sensor
  template: button_template
  variables:
    icon2: mdi:battery-50
    icon_on: mdi:motion-sensor
    icon_off: mdi:motion-sensor-off
    background_color_on: var(--yellow)
    background_color_off: var(--contrast2)
    color_on: var(--black)
    color_off: var(--contrast20)
    state_on: 'on'
    state_off: 'off'
```

### Override Entire Style Section
```yaml
- type: custom:button-card
  entity: sensor.temperature
  template: info_card
  styles:
    card:
      - height: 100px
      - background: linear-gradient(135deg, var(--blue) 0%, var(--purple) 100%)
    icon:
      - width: 50px
      - color: white
    state:
      - font-size: 28px
      - color: white
```

### Add Custom Fields
```yaml
- type: custom:button-card
  entity: sensor.battery
  template: info_card
  custom_fields:
    charging: |
      [[[
        if (states['binary_sensor.charging'].state == 'on')
          return '<ha-icon icon="mdi:lightning-bolt" style="color: yellow;"></ha-icon>';
      ]]]
```

---

## 📊 Variable Priority

When customizing, this is the order of priority:

1. **Direct card properties** (highest priority)
   ```yaml
   icon: mdi:custom
   ```

2. **Variables in card**
   ```yaml
   variables:
     color: var(--red)
   ```

3. **Styles override**
   ```yaml
   styles:
     card:
       - background: var(--blue)
   ```

4. **Template defaults** (lowest priority)

---

## ✅ Summary

- **Total Templates**: 18
- **Your Existing**: 15 templates
- **New Templates**: 3 (cover_card, room_header, info_card)
- **Most Customizable**: button_template, sensor_big
- **Easiest to Use**: info_card, light_switch, cover_card
- **Most Powerful**: climate_card, room_card, person_card_big

---

**Created**: 2025-11-26
**Dashboard**: Home Assistant Button-Card Templates
**Language**: Portuguese (PT-PT)
**Design**: 24px border-radius, Dark theme
