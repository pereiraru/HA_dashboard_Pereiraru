# 🏠 Home Assistant Dashboard - Pereiraru

A modern, beautiful Home Assistant dashboard featuring energy monitoring, Tesla car controls, and custom button-card templates.

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.11+-blue.svg)
![Button Card](https://img.shields.io/badge/button--card-required-orange.svg)
![Language](https://img.shields.io/badge/language-Portuguese-green.svg)

---

## 📋 Overview

This repository contains a comprehensive collection of Lovelace dashboard cards and templates for Home Assistant, featuring:

- ⚡ **Energy Monitoring** - Real-time power consumption, EDP tariff tracking, cost analysis
- 🚗 **Tesla Car Control** - Battery monitoring, charging controls, climate, locks
- 🎨 **18 Button-Card Templates** - Reusable, customizable templates for all card types
- 📱 **Responsive Design** - Mobile and desktop optimized with grid layout
- 🇵🇹 **Portuguese Labels** - All cards use Portuguese language

---

## ✨ Features

### ⚡ Energy Monitoring Cards (9 cards)
- Real-time power consumption with color-coded alerts
- Day/Night tariff period indicator
- Daily consumption tracking (separate day/night periods)
- Cost analysis (daily and monthly)
- 15-day consumption chart (ApexCharts)

### 🚗 Tesla Car Control Cards (14 cards)
- Large gradient battery display with range
- Charging status and controls (start/stop/limit)
- Climate control integration
- Door locks and charge port
- Interior/exterior temperature
- Odometer and range tracking
- Wake button

### 🎨 Button-Card Templates (18 templates)
**Foundation & Generic:**
- `setup` - Base template with unavailable state handling
- `button_template` - Highly customizable generic button
- `navigation_button` - Navigation with arrow indicator
- `switch_template` - Toggle switches and plugs

**Lights & Climate:**
- `light_switch` - Simple light on/off
- `light_rgb` - RGB lights with brightness slider
- `climate_card` - Advanced climate control with +/- temp

**Covers & Controls:**
- `cover_card` - Blinds, shutters, curtains control
- `room_card` - Room overview with temp & brightness

**Sensors & Display:**
- `sensor_big` - Large status displays (129px)
- `sensor_medium` - Medium with icon (56px)
- `sensor_small` - Compact text only (56px)
- `info_card` - Simple sensor display (75px)

**People & Security:**
- `person_card_big` - Large person tracking with sensors
- `person_card_small` - Compact person tracking
- `security_card` - Alarm control panel

**Headers & Media:**
- `room_header` - Page section titles
- `mobile_media_player` - Fixed bottom media bar

---

## 🎨 Design System

### Theme
- **Border Radius**: 24px rounded corners
- **Color Scheme**: Dark theme with contrast levels
- **Dynamic Colors**:
  - 🟡 Yellow - Lights ON, Day tariff
  - 🔵 Blue - Night tariff, Cooling, Covers OPEN
  - 🟢 Green - Charging, Active states
  - 🔴 Red - High power, Heat, Alerts
  - 🟣 Purple - Special actions

### Layout
- **Responsive Grid** - Auto-adjusts for screen size
- **Grid Gap**: 12px spacing
- **Standard Card**: 75px height (2 column span)
- **Large Cards**: 120-194px height (4 column span available)

---

## 📦 Installation

### Prerequisites

**Required HACS Custom Cards:**
- [button-card](https://github.com/custom-cards/button-card)
- [apexcharts-card](https://github.com/RomRider/apexcharts-card)
- [layout-card](https://github.com/thomasloven/lovelace-layout-card)

**Optional (for advanced features):**
- [my-slider-v2](https://github.com/AnthonMS/my-cards) - For RGB lights
- [mushroom-chips-card](https://github.com/piitaya/lovelace-mushroom) - For person cards

### Installation Steps

#### 1. Install Custom Cards via HACS

```
HACS → Frontend → Search for:
- Button Card
- ApexCharts Card
- Layout Card
```

#### 2. Add Templates to Your Dashboard

Open your dashboard in YAML mode and add the templates from `cards and templates/energy_car_cards/ADDON_TEMPLATES.yaml`:

```yaml
button_card_templates:
  # Copy all 18 templates here
  # Or copy just the 3 new ones if you already have the base 15
```

#### 3. Add Individual Cards

Copy card files from `cards and templates/energy_car_cards/` to your dashboard:

**Option A - Direct Copy:**
```yaml
cards:
  # Paste YAML content from individual card files
```

**Option B - Using !include (if using YAML mode):**
```yaml
cards:
  - !include energy_car_cards/energy_current_power.yaml
  - !include energy_car_cards/car_battery_large.yaml
```

---

## 📂 Repository Structure

```
HA_dashboard_Pereiraru/
├── .gitignore
├── README.md
├── CLAUDE.md                          # Project documentation
│
└── cards and templates/
    └── energy_car_cards/              # Main card collection
        │
        ├── Energy Cards (9 files)
        │   ├── energy_current_power.yaml
        │   ├── energy_period.yaml
        │   ├── energy_today_total.yaml
        │   ├── energy_today_day.yaml
        │   ├── energy_today_night.yaml
        │   ├── energy_cost_today.yaml
        │   ├── energy_monthly_total.yaml
        │   ├── energy_monthly_cost.yaml
        │   └── energy_chart_15days.yaml
        │
        ├── Tesla Car Cards (14 files)
        │   ├── car_battery_large.yaml
        │   ├── car_charging_status.yaml
        │   ├── car_charger_power.yaml
        │   ├── car_time_to_full.yaml
        │   ├── car_charge_limit.yaml
        │   ├── car_odometer.yaml
        │   ├── car_range.yaml
        │   ├── car_temp_inside.yaml
        │   ├── car_temp_outside.yaml
        │   ├── car_climate.yaml
        │   ├── car_charge_switch.yaml
        │   ├── car_charge_port.yaml
        │   ├── car_lock.yaml
        │   └── car_wake_button.yaml
        │
        ├── Templates
        │   ├── ADDON_TEMPLATES.yaml         # 3 new templates to add
        │   └── button_card_templates.yaml   # All 18 templates (standalone)
        │
        ├── EDP Energia Views (3 versions)
        │   ├── edp_energia_view.yaml              # Full version
        │   ├── edp_energia_view_compact.yaml      # Compact version
        │   └── edp_energia_view_ultra_compact.yaml # Ultra compact (70% less scrolling)
        │
        └── Documentation (10 guides)
            ├── README.md                          # Complete usage guide
            ├── ALL_TEMPLATES_GUIDE.md             # All 18 templates documented
            ├── TEMPLATE_USAGE_GUIDE.md            # How to use variables in cards ⭐ NEW
            ├── TEMPLATE_REFERENCE_TABLE.md        # Quick reference table ⭐ NEW
            ├── IMPLEMENTATION_SUMMARY.md          # Implementation overview
            ├── TEMPLATE_INTEGRATION_VISUAL.md     # Visual integration guide
            ├── TEMPLATE_COMPARISON.md             # Template compatibility
            ├── TEMPLATES_INSTALL.md               # Installation guide
            ├── TEMPLATES_TO_ADD_NOW.yaml          # 3 templates quick add ⭐ NEW
            ├── EDP_VIEW_GUIDE.md                  # EDP view documentation ⭐ NEW
            ├── INDEX.md                           # Quick card index
            └── QUICK_START.md                     # Fast setup guide
```

---

## 🚀 Quick Start

### 📊 EDP Energia View (Ready-to-Use!)

We've created **3 versions** of a complete EDP energy monitoring view:

1. **Full Version** (`edp_energia_view.yaml`)
   - Complete energy dashboard
   - All features and documentation
   - ~100 cards with detailed layout

2. **Compact Version** (`edp_energia_view_compact.yaml`)
   - 40% less scrolling
   - Tighter spacing and smaller cards
   - Perfect for desktop

3. **Ultra Compact** (`edp_energia_view_ultra_compact.yaml`) ⭐ **RECOMMENDED**
   - 70% less scrolling
   - Icon-only power monitors
   - Everything fits in ~2 screen heights
   - Best for mobile and desktop

**Features:**
- ⚡ Real-time power monitoring with color coding
- 📊 15-day consumption chart
- 💰 Cost tracking (daily & monthly)
- 🔌 8 individual device monitors
- 🌙 Day/Night tariff tracking

**To use:** Copy any version to your dashboard's raw YAML editor.

See `EDP_VIEW_GUIDE.md` for complete documentation.

---

### Create Energy Page

```yaml
- title: Energia
  path: energia
  icon: mdi:lightning-bolt
  type: custom:grid-layout
  layout:
    grid-template-columns: repeat(auto-fill, minmax(min(100%, 160px), 1fr))
    grid-gap: 12px
    padding: 12px
  cards:
    # Header
    - type: custom:button-card
      name: Energia
      label: Monitorização EDP e consumos
      template: room_header
      view_layout:
        grid-column: 1 / -1

    # Add energy cards here
    # Copy from energy_*.yaml files
```

### Create Tesla Car Page

```yaml
- title: Tesla
  path: car
  icon: mdi:car-electric
  type: custom:grid-layout
  layout:
    grid-template-columns: repeat(auto-fill, minmax(min(100%, 160px), 1fr))
    grid-gap: 12px
    padding: 12px
  cards:
    # Header
    - type: custom:button-card
      name: Tesla Model Y
      label: 🔋 Ze das Pilhas
      template: room_header
      view_layout:
        grid-column: 1 / -1

    # Add Tesla cards here
    # Copy from car_*.yaml files
```

---

## 🎯 Customization

All cards support extensive customization. See `ALL_TEMPLATES_GUIDE.md` for complete details.

### Change Colors
```yaml
styles:
  card:
    - background: var(--purple)  # Custom color
```

### Change Icons
```yaml
icon: mdi:your-custom-icon
variables:
  icon_on: mdi:custom-on-icon
  icon_off: mdi:custom-off-icon
```

### Custom State Display
```yaml
state_display: |
  [[[
    return entity.state + ' custom text';
  ]]]
```

---

## 📊 Entity Requirements

### Energy Monitoring Entities
These sensors are expected by the energy cards:
- `sensor.w_shelly_todos_juntos` - Current power (W)
- `sensor.edp_periodo_atual` - Current tariff period
- `sensor.edp_dia_total_kwh_consumidos` - Total daily kWh
- `sensor.edp_daily_kwh` - Day period consumption
- `sensor.edp_nightly_kwh` - Night period consumption
- `sensor.edp_valor_diario_euros` - Daily cost (€)
- `sensor.mensal_kwh_total` - Monthly total
- `sensor.edp_valor_mensal_euros` - Monthly cost

### Tesla Car Entities
These sensors are expected by the Tesla cards:
- `sensor.ze_das_pilhas_battery_level` - Battery %
- `sensor.ze_das_pilhas_charging` - Charging status
- `sensor.ze_das_pilhas_charger_power` - Charger power
- `button.ze_das_pilhas_wake` - Wake button
- Plus climate, lock, cover entities

**Note:** Update entity IDs in card files to match your system.

---

## 📚 Documentation

Comprehensive documentation is available in the `cards and templates/energy_car_cards/` folder:

### 🎯 Getting Started
- **QUICK_START.md** - Fast setup guide for beginners
- **README.md** - Complete usage instructions
- **INDEX.md** - Quick card reference by category

### 📖 Template Guides
- **TEMPLATE_USAGE_GUIDE.md** ⭐ **NEW** - Shows exactly where and how to use variables in cards
- **TEMPLATE_REFERENCE_TABLE.md** ⭐ **NEW** - Quick reference table for all 18 templates
- **ALL_TEMPLATES_GUIDE.md** - Complete documentation of all templates
- **TEMPLATES_TO_ADD_NOW.yaml** ⭐ **NEW** - Quick copy/paste for 3 new templates

### 🔧 Implementation Guides
- **IMPLEMENTATION_SUMMARY.md** - What was created and next steps
- **TEMPLATE_INTEGRATION_VISUAL.md** - Visual integration guide
- **TEMPLATE_COMPARISON.md** - Template compatibility analysis
- **TEMPLATES_INSTALL.md** - Step-by-step installation

### 📊 View Documentation
- **EDP_VIEW_GUIDE.md** ⭐ **NEW** - Complete EDP Energia view documentation
  - Color coding system
  - Power thresholds for each device
  - Customization options
  - Mobile vs Desktop layouts

---

## 🛠️ Technology Stack

- **Home Assistant**: 2025.11.3+
- **Custom Cards**: button-card, apexcharts-card, layout-card
- **Language**: Portuguese (PT)
- **Theme**: Dark with contrast colors
- **Configuration**: YAML

---

## 📸 Screenshots

<!-- Add screenshots here -->
_Screenshots coming soon..._

**Planned:**
- Energy monitoring page
- Tesla car control page
- Individual card examples

---

## 🤝 Contributing

Contributions are welcome! If you have improvements or new cards:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙏 Credits

- **Button Card** - [custom-cards/button-card](https://github.com/custom-cards/button-card)
- **ApexCharts Card** - [RomRider/apexcharts-card](https://github.com/RomRider/apexcharts-card)
- **Home Assistant Community** - For inspiration and support

---

## 💡 Support

If you find this helpful:
- ⭐ Star this repository
- 🐛 Report issues via GitHub Issues
- 💬 Share your customizations!

---

**Created by**: Rui Pereira
**Last Updated**: 2025-11-26
**Home Assistant Version**: 2025.11.3+
**Language**: Portuguese (PT-PT)
