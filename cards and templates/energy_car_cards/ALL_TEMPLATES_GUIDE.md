# Complete Template Guide - All Available Templates

## 📋 Template Index

### ✅ YOUR EXISTING TEMPLATES (15 templates)
### 🆕 NEW ADD-ON TEMPLATES (3 templates)
### 📊 TOTAL: 18 Templates Available

---

## ✅ EXISTING TEMPLATES (Already in Your Dashboard)

### 1. **setup** - Foundation Template
**Purpose**: Base template providing unavailable state handling and font settings
**Features**:
- Shows alert icon when entity unavailable
- Strikethrough text for unavailable states
- Font family normalization

**Usage**: Used as base for all other templates
```yaml
template: setup
```

---

### 2. **button_template** - Generic Customizable Button
**Purpose**: Highly flexible button with customizable colors and icons
**Features**:
- Custom icons for on/off states
- Custom background colors
- Custom text colors
- Small icon indicator (icon2)
- Label shows entity state

**Variables**:
```yaml
variables:
  icon2: mdi:custom-icon              # Small top-right icon
  icon_on: mdi:lightbulb              # Icon when ON
  icon_off: mdi:lightbulb-outline     # Icon when OFF
  state_on: 'on'                      # State considered "on"
  state_off: 'off'                    # State considered "off"
  background_color_on: var(--red)     # Background when ON
  background_color_off: var(--contrast2)  # Background when OFF
  color_on: var(--black)              # Text color when ON
  color_off: var(--contrast20)        # Text color when OFF
```

**Example**:
```yaml
- type: custom:button-card
  entity: binary_sensor.motion
  name: Motion Sensor
  template: button_template
  variables:
    icon_on: mdi:motion-sensor
    icon_off: mdi:motion-sensor-off
    background_color_on: var(--yellow)
    state_on: 'on'
```

---

### 3. **navigation_button** - Navigation with Arrow
**Purpose**: Button that navigates to another view
**Features**:
- Same as button_template but with navigation action
- Arrow icon (mdi:arrow-right-bold) in top-right
- Tap navigates to path

**Variables**: Same as button_template PLUS:
```yaml
variables:
  navigation_path: /lovelace/sala  # Where to navigate
```

**Example**:
```yaml
- type: custom:button-card
  entity: light.sala
  name: Ir para Sala
  template: navigation_button
  variables:
    navigation_path: /lovelace/sala
```

---

### 4. **switch_template** - Switch/Toggle Control
**Purpose**: Toggle switches, plugs, or any on/off entity
**Features**:
- Tap to toggle
- Shows entity state as text
- Custom color variable
- Default purple when ON

**Variables**:
```yaml
variables:
  icon_on: mdi:toggle-switch
  icon_off: mdi:toggle-switch-off
  color: var(--purple)  # Change ON color
```

**Example**:
```yaml
- type: custom:button-card
  entity: switch.heater
  name: Aquecedor
  template: switch_template
  variables:
    color: var(--red)  # Red when on
```

---

### 5. **climate_card** - Climate Control (Advanced)
**Purpose**: Full climate control with temp adjustment
**Features**:
- Shows current temp + humidity
- Window sensor integration
- +/- temp controls
- Color changes by mode (auto=green, heat=red)
- Large format (194px height)

**Variables**:
```yaml
variables:
  sensor: binary_sensor.window  # Window/door sensor
```

**Example**:
```yaml
- type: custom:button-card
  entity: climate.ac_sala
  name: AC Sala
  template: climate_card
  variables:
    sensor: binary_sensor.sala_window
```

---

### 6. **light_rgb** - RGB Light with Slider
**Purpose**: RGB lights with color and brightness control
**Features**:
- Shows RGB color as background
- Brightness slider
- Brightness percentage display
- Requires custom:my-slider-v2

**Example**:
```yaml
- type: custom:button-card
  entity: light.rgb_strip
  name: LED RGB
  template: light_rgb
```

---

### 7. **light_switch** - Simple Light Toggle
**Purpose**: Basic light on/off
**Features**:
- Yellow when ON
- Shows ON/OFF state text
- Icon in circle badge
- Simple and fast

**Variables**:
```yaml
variables:
  icon_on: mdi:lightbulb
  icon_off: mdi:lightbulb-outline
  color: var(--yellow)  # Change ON color
```

**Example**:
```yaml
- type: custom:button-card
  entity: light.desk
  name: Secretária
  template: light_switch
```

---

### 8. **mobile_media_player** - Fixed Bottom Media Player
**Purpose**: Mobile media player bar (fixed at bottom)
**Features**:
- Shows album art
- Artist + title
- Play/pause button
- Progress bar animation
- Fixed position (bottom of screen)

**Example**:
```yaml
- type: custom:button-card
  entity: media_player.spotify
  template: mobile_media_player
```

---

### 9. **person_card_big** - Large Person Card
**Purpose**: Person tracking with sensors
**Features**:
- Large entity picture
- Home/away status
- Green border when home
  - Grayscale when away
- 3 sensor chips (battery, steps, direction)

**Variables**:
```yaml
variables:
  sensor1: sensor.phone_battery
  sensor2: sensor.phone_steps
  sensor3: sensor.direction
```

**Example**:
```yaml
- type: custom:button-card
  entity: person.rui
  name: Rui
  template: person_card_big
  variables:
    sensor1: sensor.rui_battery
    sensor2: sensor.rui_steps
    sensor3: sensor.rui_direction
```

---

### 10. **person_card_small** - Small Person Card
**Purpose**: Compact person tracking
**Features**:
- Small entity picture
- Home/away badge
- 1 sensor chip (usually battery)

**Variables**:
```yaml
variables:
  sensor: sensor.battery_level
```

---

### 11. **room_card** - Room Summary Card
**Purpose**: Room overview with temp & brightness slider
**Features**:
- Shows temperature + humidity
- Window sensor integration
- Brightness slider when light ON
- Navigation on tap
- 130px height (155px when ON with slider)

**Variables**:
```yaml
variables:
  icon: mdi:sofa-outline       # Room icon
  sensor: binary_sensor.window # Window sensor
  state: temperature/humidity display template
```

**Example**:
```yaml
- type: custom:button-card
  entity: light.sala
  name: Sala
  template: room_card
  variables:
    icon: mdi:sofa
    sensor: binary_sensor.sala_window
```

---

### 12. **security_card** - Alarm Panel Control
**Purpose**: Alarm control with mode selector
**Features**:
- Shows alarm state
- Tile with arm/disarm modes
- Blink animation when triggered
- Red background when triggered

**Example**:
```yaml
- type: custom:button-card
  entity: alarm_control_panel.home
  name: Alarme
  template: security_card
```

---

### 13. **sensor_big** - Large Sensor Display
**Purpose**: Big status sensors (connection, system status)
**Features**:
- Large label display (26px font)
- Icon in circle badge (top-right)
- Custom state displays
- 129px height

**Variables**:
```yaml
variables:
  icon_on: mdi:router-wireless
  icon_off: mdi:router-wireless-off
  state_on: 'on'
  state_off: 'off'
  background_color_on: var(--green)
  background_color_off: var(--red)
  color_on: var(--black)
  color_off: var(--black)
  state: HTML template for display
```

**Example**:
```yaml
- type: custom:button-card
  entity: binary_sensor.internet
  name: Internet
  template: sensor_big
  variables:
    icon_on: mdi:wifi
    icon_off: mdi:wifi-off
```

---

### 14. **sensor_medium** - Medium Sensor with Icon
**Purpose**: Numeric sensors (power, energy, etc.)
**Features**:
- Icon in circle (left side)
- Value with unit (customizable)
- 56px height
- Compact and efficient

**Variables**:
```yaml
variables:
  state: |  # Custom display template
    [[[
      var st = states[entity.entity_id].state;
      var uni = ' kWh';  # Change unit
      return `${parseFloat(st).toFixed(1)}<span style="font-size:0.5em;opacity:0.7">${uni}</span>`;
    ]]]
```

**Example**:
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

---

### 15. **sensor_small** - Small Sensor (No Icon)
**Purpose**: Minimal sensor display
**Features**:
- No icon (text only)
- Value with unit
- 56px height
- Most compact option

**Variables**: Same as sensor_medium

**Example**:
```yaml
- type: custom:button-card
  entity: sensor.power
  name: Potência
  template: sensor_small
```

---

## 🆕 NEW ADD-ON TEMPLATES (Add These!)

### 16. **cover_card** - Cover/Shutter Control
**Purpose**: Control blinds, shutters, curtains
**Features**:
- Blue when OPEN
- Gray when CLOSED
- Arrow indicator (up/down)
- Tap to toggle
- 75px height

**No Variables** - Just use directly

**Example**:
```yaml
- type: custom:button-card
  entity: cover.sala_estores
  name: Estores Sala
  template: cover_card
```

---

### 17. **room_header** - Page Header/Section Title
**Purpose**: Section dividers and page titles
**Features**:
- Large title (28px)
- Subtitle/label (14px)
- No background
- Not clickable

**No Variables** - Use name & label directly

**Example**:
```yaml
- type: custom:button-card
  name: Energia
  label: Monitorização de consumos
  template: room_header
```

---

### 18. **info_card** - Simple Info/Status Display
**Purpose**: Show sensor values with icon
**Features**:
- Large state value (24px)
- Icon on left (40px)
- Simple and clean
- 75px height
- SIMPLER alternative to sensor_medium

**No Variables** - Just entity, name, icon

**Example**:
```yaml
- type: custom:button-card
  entity: sensor.battery_level
  name: Bateria
  icon: mdi:battery
  template: info_card
  state_display: |
    [[[
      return entity.state + '%';
    ]]]
```

---

## 🎨 How to Customize Any Card

### Change Colors
```yaml
variables:
  color: var(--blue)  # For switch_template
  background_color_on: var(--purple)  # For button_template
```

### Change Icons
```yaml
icon: mdi:your-icon
variables:
  icon_on: mdi:icon-when-on
  icon_off: mdi:icon-when-off
```

### Custom State Display
```yaml
state_display: |
  [[[
    if (entity.state == "on") return "Ligado";
    else return "Desligado";
  ]]]
```

### Custom Label
```yaml
label: |
  [[[
    return entity.attributes.temperature + "°C";
  ]]]
```

---

## 🚀 Quick Reference by Use Case

**Lights**: `light_switch`, `light_rgb`
**Switches**: `switch_template`
**Climate**: `climate_card`
**Covers**: `cover_card` ⭐ NEW
**Sensors**: `sensor_big`, `sensor_medium`, `sensor_small`, `info_card` ⭐ NEW
**Navigation**: `navigation_button`
**Headers**: `room_header` ⭐ NEW
**Rooms**: `room_card`
**People**: `person_card_big`, `person_card_small`
**Security**: `security_card`
**Media**: `mobile_media_player`
**Custom**: `button_template`

---

## 📦 Required Custom Cards

- **custom:button-card** (ALL templates)
- **custom:my-slider-v2** (light_rgb, room_card)
- **custom:mushroom-chips-card** (person cards)

---

**Total Templates**: 18
**New Add-Ons**: 3 (cover_card, room_header, info_card)
**Ready to use**: Copy ADDON_TEMPLATES.yaml into your dashboard!
