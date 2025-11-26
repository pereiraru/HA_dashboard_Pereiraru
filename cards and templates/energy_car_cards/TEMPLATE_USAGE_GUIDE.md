# 📊 Button-Card Templates - Usage Guide with Real Examples

## How to Use Templates in Your Cards

This guide shows you **exactly where and how** to add variables in your card YAML.

---

## Template 1: **setup**

### Functionalities:
- Base template with unavailable state handling
- Font normalization
- Used as parent for other templates

### Variables:
None (used as foundation only)

### Example Card:
```yaml
- type: custom:button-card
  entity: sensor.temperature
  name: Temperature
  template: setup
```

---

## Template 2: **button_template**

### Functionalities:
- Highly customizable button
- Custom icons for ON/OFF states
- Custom background colors
- Custom text colors
- Small indicator icon (icon2)

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `icon2` | Small icon in top-right corner | In `variables:` section |
| `icon_on` | Icon when state is ON | In `variables:` section |
| `icon_off` | Icon when state is OFF | In `variables:` section |
| `state_on` | What value is considered "on" | In `variables:` section |
| `state_off` | What value is considered "off" | In `variables:` section |
| `background_color_on` | Background color when ON | In `variables:` section |
| `background_color_off` | Background color when OFF | In `variables:` section |
| `color_on` | Text color when ON | In `variables:` section |
| `color_off` | Text color when OFF | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: binary_sensor.motion_sensor
  name: Motion Sensor
  template: button_template
  variables:
    icon2: mdi:battery-50                    # Top-right indicator
    icon_on: mdi:motion-sensor               # Icon when detecting motion
    icon_off: mdi:motion-sensor-off          # Icon when no motion
    state_on: 'on'                           # What state means "on"
    state_off: 'off'                         # What state means "off"
    background_color_on: var(--yellow)       # Yellow background when motion detected
    background_color_off: var(--contrast2)   # Gray background when no motion
    color_on: var(--black)                   # Black text when ON
    color_off: var(--contrast20)             # Light text when OFF
```

**What each variable does in this example:**
- `icon2: mdi:battery-50` → Shows battery icon in top-right
- `icon_on: mdi:motion-sensor` → Shows filled sensor icon when motion detected
- `icon_off: mdi:motion-sensor-off` → Shows empty sensor icon when no motion
- `background_color_on: var(--yellow)` → Card turns yellow when motion detected
- `background_color_off: var(--contrast2)` → Card is gray when no motion

---

## Template 3: **navigation_button**

### Functionalities:
- Navigate to another view
- Arrow icon in top-right
- Inherits all from button_template

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `navigation_path` | View to navigate to | In `variables:` section |
| Plus all from button_template | | |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: light.sala
  name: Ir para Sala
  template: navigation_button
  variables:
    navigation_path: /lovelace/sala          # Navigates to sala view when tapped
    icon_on: mdi:sofa                        # Shows sofa icon when lights are ON
    icon_off: mdi:sofa-outline               # Shows outline sofa when lights OFF
    background_color_on: var(--green)        # Green background when lights ON
    background_color_off: var(--contrast2)   # Gray background when lights OFF
```

**What each variable does:**
- `navigation_path: /lovelace/sala` → Clicking card takes you to the "sala" dashboard page
- `icon_on: mdi:sofa` → Shows filled sofa icon when sala lights are on
- `background_color_on: var(--green)` → Card is green when lights are on

---

## Template 4: **switch_template**

### Functionalities:
- Toggle switches on/off
- Tap to toggle
- Shows state as text

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `icon_on` | Icon when switch is ON | In `variables:` section |
| `icon_off` | Icon when switch is OFF | In `variables:` section |
| `color` | Background color when ON | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: switch.heater
  name: Aquecedor
  template: switch_template
  variables:
    icon_on: mdi:radiator                    # Radiator icon when heater is ON
    icon_off: mdi:radiator-off               # Radiator-off icon when heater is OFF
    color: var(--red)                        # Red background when heater is ON (instead of default purple)
```

**What each variable does:**
- `color: var(--red)` → Card turns red when switch is ON (default is purple)
- `icon_on: mdi:radiator` → Shows radiator icon when heater is running

---

## Template 5: **climate_card**

### Functionalities:
- Climate/AC control
- Temperature adjustment (+/- buttons)
- Shows current temp and humidity
- Window sensor integration
- Color changes by mode

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `sensor` | Window/door sensor entity | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: climate.ac_sala
  name: AC Sala
  template: climate_card
  variables:
    sensor: binary_sensor.sala_window        # Shows if window is open/closed
```

**What the variable does:**
- `sensor: binary_sensor.sala_window` → Displays window status on the card
- If window is open, card shows warning indicator

---

## Template 6: **light_rgb**

### Functionalities:
- RGB light control
- Shows current color as background
- Brightness slider
- Brightness percentage display

### Variables & Where to Add Them:

None (automatically uses light entity attributes)

### Example Card Code:
```yaml
- type: custom:button-card
  entity: light.led_strip
  name: LED RGB Sala
  template: light_rgb
```

**No variables needed** - automatically shows the RGB color from the light entity

---

## Template 7: **light_switch**

### Functionalities:
- Simple light on/off
- Yellow when ON (default)
- Shows ON/OFF text

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `icon_on` | Icon when light is ON | In `variables:` section |
| `icon_off` | Icon when light is OFF | In `variables:` section |
| `color` | Background color when ON | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: light.desk
  name: Secretária
  template: light_switch
  variables:
    icon_on: mdi:desk-lamp                   # Desk lamp icon when ON
    icon_off: mdi:desk-lamp-outline          # Desk lamp outline when OFF
    color: var(--blue)                       # Blue background when ON (instead of yellow)
```

**What each variable does:**
- `color: var(--blue)` → Light card turns blue when ON (default is yellow)
- `icon_on: mdi:desk-lamp` → Shows desk lamp icon when light is on

---

## Template 8: **person_card_big**

### Functionalities:
- Large person tracking
- Entity picture
- Home/away status
- 3 sensor chips (battery, steps, direction)
- Green border when home, grayscale when away

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `sensor1` | First sensor entity (usually battery) | In `variables:` section |
| `sensor2` | Second sensor entity (usually steps) | In `variables:` section |
| `sensor3` | Third sensor entity (usually direction) | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: person.rui
  name: Rui
  template: person_card_big
  variables:
    sensor1: sensor.rui_phone_battery        # Shows battery percentage
    sensor2: sensor.rui_steps_today          # Shows daily steps
    sensor3: sensor.rui_direction            # Shows direction/location
```

**What each variable does:**
- `sensor1: sensor.rui_phone_battery` → Displays "85%" (battery level) in first chip
- `sensor2: sensor.rui_steps_today` → Displays "5,234" (steps) in second chip
- `sensor3: sensor.rui_direction` → Displays "Norte" (direction) in third chip

---

## Template 9: **person_card_small**

### Functionalities:
- Compact person tracking
- Small entity picture
- Home/away badge
- 1 sensor chip

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `sensor` | Sensor entity to display | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: person.maria
  name: Maria
  template: person_card_small
  variables:
    sensor: sensor.maria_phone_battery       # Shows battery level below picture
```

**What the variable does:**
- `sensor: sensor.maria_phone_battery` → Shows "72%" battery indicator

---

## Template 10: **room_card**

### Functionalities:
- Room overview
- Temperature and humidity display
- Window sensor integration
- Brightness slider when light ON
- Navigation to room

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `icon` | Room icon | In `variables:` section |
| `sensor` | Window/door sensor | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: light.sala
  name: Sala
  template: room_card
  variables:
    icon: mdi:sofa                           # Shows sofa icon for living room
    sensor: binary_sensor.sala_window        # Shows if window is open
```

**What each variable does:**
- `icon: mdi:sofa` → Displays sofa icon representing living room
- `sensor: binary_sensor.sala_window` → Shows window icon if window is open

---

## Template 11: **sensor_big**

### Functionalities:
- Large sensor display (129px height)
- Icon in circle badge
- Custom state displays
- Dynamic colors

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `icon_on` | Icon when state is ON | In `variables:` section |
| `icon_off` | Icon when state is OFF | In `variables:` section |
| `state_on` | State considered "on" | In `variables:` section |
| `state_off` | State considered "off" | In `variables:` section |
| `background_color_on` | Background when ON | In `variables:` section |
| `background_color_off` | Background when OFF | In `variables:` section |
| `color_on` | Text color when ON | In `variables:` section |
| `color_off` | Text color when OFF | In `variables:` section |
| `state` | Custom HTML display template | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: binary_sensor.internet
  name: Internet
  template: sensor_big
  variables:
    icon_on: mdi:wifi                        # WiFi icon when connected
    icon_off: mdi:wifi-off                   # WiFi-off icon when disconnected
    state_on: 'on'                           # "on" means connected
    state_off: 'off'                         # "off" means disconnected
    background_color_on: var(--green)        # Green when connected
    background_color_off: var(--red)         # Red when disconnected
    color_on: var(--black)                   # Black text when connected
    color_off: var(--white)                  # White text when disconnected
    state: |                                 # Custom display text
      [[[
        if (entity.state == 'on')
          return '<b>Conectado</b><br>100 Mbps';
        else
          return '<b>Desconectado</b><br>Sem internet';
      ]]]
```

**What each variable does:**
- `background_color_on: var(--green)` → Card is green when internet is working
- `background_color_off: var(--red)` → Card is red when internet is down
- `state: |...` → Shows custom text like "Conectado<br>100 Mbps"

---

## Template 12: **sensor_medium**

### Functionalities:
- Medium sensor (56px height)
- Icon in circle (left side)
- Numeric value with unit
- Compact display

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `state` | Custom display with unit | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: sensor.energy_today
  name: Energia Hoje
  icon: mdi:lightning-bolt
  template: sensor_medium
  variables:
    state: |                                 # Custom display format
      [[[
        var value = parseFloat(entity.state);
        var unit = ' kWh';
        return value.toFixed(2) + '<span style="font-size:0.5em;opacity:0.7">' + unit + '</span>';
      ]]]
```

**What the variable does:**
- `state: |...` → Formats display as "12.45 kWh" with small "kWh" unit
- Without this variable, it would just show "12.45" with no unit

---

## Template 13: **sensor_small**

### Functionalities:
- Small sensor (56px height)
- Text only (no icon)
- Custom unit display
- Most compact option

### Variables & Where to Add Them:

| Variable | What It Does | Where to Add |
|----------|--------------|--------------|
| `state` | Custom display with unit | In `variables:` section |

### Example Card Code:
```yaml
- type: custom:button-card
  entity: sensor.power
  name: Potência
  template: sensor_small
  variables:
    state: |                                 # Custom format
      [[[
        return Math.round(entity.state) + ' W';
      ]]]
```

**What the variable does:**
- `state: |...` → Displays "1523 W" instead of just "1523"

---

## Template 14: **cover_card**

### Functionalities:
- Control blinds/shutters/curtains
- Blue when OPEN
- Gray when CLOSED
- Arrow indicator (up/down)
- Tap to toggle

### Variables & Where to Add Them:

None (automatically uses cover entity states)

### Example Card Code:
```yaml
- type: custom:button-card
  entity: cover.sala_estores
  name: Estores Sala
  template: cover_card
```

**No variables needed** - automatically handles open/closed states

---

## Template 15: **room_header**

### Functionalities:
- Page section header
- Large title (28px)
- Subtitle (14px)
- No background
- Not clickable

### Variables & Where to Add Them:

None (just use `name` and `label` directly)

### Example Card Code:
```yaml
- type: custom:button-card
  name: Energia                              # Large title text
  label: Monitorização e análise de consumos # Smaller subtitle text
  template: room_header
  view_layout:
    grid-column: 1 / -1                      # Spans full width
```

**What name and label do:**
- `name: Energia` → Shows "Energia" in large 28px font
- `label: Monitorização...` → Shows subtitle in small 14px font below

---

## Template 16: **info_card**

### Functionalities:
- Simple info display (75px height)
- Icon on left (40px)
- Large state value (24px)
- Clean and simple

### Variables & Where to Add Them:

None (just use entity, name, icon directly)

### Example Card Code:
```yaml
- type: custom:button-card
  entity: sensor.battery_level
  name: Bateria                              # Name shown on card
  icon: mdi:battery                          # Icon shown on left
  template: info_card
  state_display: |                           # Custom state format (optional)
    [[[
      return entity.state + '%';
    ]]]
```

**What each part does:**
- `name: Bateria` → Shows "Bateria" label
- `icon: mdi:battery` → Shows battery icon on left
- `state_display: |...` → Formats value as "85%" instead of "85"

---

## Template 17: **security_card**

### Functionalities:
- Alarm control panel
- Arm/disarm modes
- Shows alarm state
- Blink animation when triggered
- Red background when triggered

### Variables & Where to Add Them:

None (automatically uses alarm entity states)

### Example Card Code:
```yaml
- type: custom:button-card
  entity: alarm_control_panel.home
  name: Alarme Casa
  template: security_card
```

**No variables needed** - automatically handles all alarm states

---

## Template 18: **mobile_media_player**

### Functionalities:
- Fixed-bottom media player bar
- Album art
- Artist + title
- Play/pause button
- Progress bar animation

### Variables & Where to Add Them:

None (automatically uses media player attributes)

### Example Card Code:
```yaml
- type: custom:button-card
  entity: media_player.spotify
  template: mobile_media_player
```

**No variables needed** - automatically shows currently playing media

---

## 🎯 Quick Summary: Where Variables Go

**ALL variables go in the `variables:` section like this:**

```yaml
- type: custom:button-card
  entity: your.entity
  name: Your Name
  icon: mdi:your-icon           # Optional: override template icon
  template: template_name       # Which template to use
  variables:                    # ← Variables section starts here
    variable1: value1           # ← Your custom variables
    variable2: value2
    variable3: |                # ← Multi-line variables use |
      [[[
        return 'custom code';
      ]]]
  styles:                       # Optional: override template styles
    card:
      - background: var(--red)
  view_layout:                  # Optional: grid positioning
    grid-column: span 2
```

---

## 💡 Common Patterns

### Pattern 1: Simple Variable (Text/Icon)
```yaml
variables:
  color: var(--red)
  icon_on: mdi:lightbulb
```

### Pattern 2: Multi-line Variable (Code)
```yaml
variables:
  state: |
    [[[
      return entity.state + ' units';
    ]]]
```

### Pattern 3: Multiple Variables Together
```yaml
variables:
  icon_on: mdi:motion-sensor
  icon_off: mdi:motion-sensor-off
  background_color_on: var(--yellow)
  background_color_off: var(--contrast2)
```

---

**Created**: 2025-11-26
**Purpose**: Show exactly where and how to use template variables in card YAML
