# 🎨 Template Integration - Visual Guide

## 📊 Current State: Your Dashboard Templates

```
┌─────────────────────────────────────────────────┐
│  YOUR EXISTING BUTTON_CARD_TEMPLATES (15)       │
│  ✅ Already in your dashboard                   │
└─────────────────────────────────────────────────┘

🔧 Foundation
  └─ setup (base template for unavailable states)

🎛️ Generic Controls
  ├─ button_template (customizable button)
  ├─ navigation_button (navigation with arrow)
  └─ switch_template (toggle switches)

💡 Lights
  ├─ light_switch (simple on/off)
  └─ light_rgb (RGB with brightness slider)

🌡️ Climate
  └─ climate_card (temp control with +/- buttons)

📊 Sensors (3 sizes)
  ├─ sensor_big (129px - large status displays)
  ├─ sensor_medium (56px - with icon)
  └─ sensor_small (56px - text only)

🏠 Rooms & People
  ├─ room_card (room overview with temp/slider)
  ├─ person_card_big (large person tracking)
  └─ person_card_small (compact person)

🔐 Security & Media
  ├─ security_card (alarm control)
  └─ mobile_media_player (fixed bottom player)
```

---

## ➕ What You Need to Add (3 New Templates)

```
┌─────────────────────────────────────────────────┐
│  NEW TEMPLATES FROM ADDON_TEMPLATES.yaml        │
│  ⭐ Add these to your dashboard                 │
└─────────────────────────────────────────────────┘

🪟 Covers
  └─ cover_card (blinds/shutters control)
     • Blue when OPEN
     • Gray when CLOSED
     • Arrow indicator (up/down)
     • 75px height

📑 Headers
  └─ room_header (page section titles)
     • Large title (28px)
     • Subtitle (14px)
     • No background
     • Not clickable

ℹ️ Info Display
  └─ info_card (simple sensor display)
     • Icon on left (40px)
     • Large state value (24px)
     • 75px height
     • Simpler than sensor_medium
```

---

## 🔄 Integration Process

### Step 1: Locate Your Templates Section

Find this in your dashboard YAML:

```yaml
button_card_templates:

  setup:
    # ... your existing setup template

  button_template:
    # ... your existing button_template

  # ... 13 more existing templates ...
```

### Step 2: Add 3 New Templates

Open `ADDON_TEMPLATES.yaml` and copy the 3 new templates:

```yaml
button_card_templates:

  # ============================================
  # YOUR EXISTING 15 TEMPLATES (keep as-is)
  # ============================================

  setup:
    # ... existing

  button_template:
    # ... existing

  # ... rest of your 15 templates ...

  # ============================================
  # ADD THESE 3 NEW TEMPLATES BELOW
  # ============================================

  cover_card:
    template: base_card
    icon: |
      [[[
        if (entity.state == "open") return "mdi:window-shutter-open";
        else if (entity.state == "closed") return "mdi:window-shutter";
        else return "mdi:window-shutter-alert";
      ]]]
    # ... (copy full template from ADDON_TEMPLATES.yaml)

  room_header:
    tap_action:
      action: none
    # ... (copy full template from ADDON_TEMPLATES.yaml)

  info_card:
    tap_action:
      action: more-info
    # ... (copy full template from ADDON_TEMPLATES.yaml)
```

---

## 📦 Complete Template Map (After Integration)

```
┌───────────────────────────────────────────────────────────┐
│  COMPLETE BUTTON_CARD_TEMPLATES (18 TOTAL)                │
│  ✅ Your 15 existing + ⭐ 3 new                            │
└───────────────────────────────────────────────────────────┘

🔧 Foundation (1)
  └─ setup

🎛️ Generic Controls (3)
  ├─ button_template
  ├─ navigation_button
  └─ switch_template

💡 Lights (2)
  ├─ light_switch
  └─ light_rgb

🌡️ Climate (1)
  └─ climate_card

🪟 Covers (1) ⭐ NEW
  └─ cover_card

📊 Sensors & Info (4)
  ├─ sensor_big
  ├─ sensor_medium
  ├─ sensor_small
  └─ info_card ⭐ NEW

🏠 Rooms & Headers (2)
  ├─ room_card
  └─ room_header ⭐ NEW

👤 People (2)
  ├─ person_card_big
  └─ person_card_small

🔐 Security & Media (2)
  ├─ security_card
  └─ mobile_media_player

────────────────────────────────────────────────────────────
Total: 18 templates available for all your cards
```

---

## 🎯 How Cards Use Templates

### Energy Cards Use These Templates:

```
energy_current_power.yaml    → info_card ⭐ NEW
energy_period.yaml           → info_card ⭐ NEW
energy_today_total.yaml      → info_card ⭐ NEW
energy_today_day.yaml        → info_card ⭐ NEW
energy_today_night.yaml      → info_card ⭐ NEW
energy_cost_today.yaml       → info_card ⭐ NEW
energy_monthly_total.yaml    → info_card ⭐ NEW
energy_monthly_cost.yaml     → info_card ⭐ NEW
energy_chart_15days.yaml     → (no template - pure ApexChart)
```

### Tesla Car Cards Use These Templates:

```
car_battery_large.yaml       → base_card ✅ existing
car_charging_status.yaml     → info_card ⭐ NEW
car_charger_power.yaml       → info_card ⭐ NEW
car_time_to_full.yaml        → info_card ⭐ NEW
car_charge_limit.yaml        → info_card ⭐ NEW
car_odometer.yaml            → info_card ⭐ NEW
car_range.yaml               → info_card ⭐ NEW
car_temp_inside.yaml         → info_card ⭐ NEW
car_temp_outside.yaml        → info_card ⭐ NEW
car_climate.yaml             → climate_card ✅ existing
car_charge_switch.yaml       → switch_card ✅ existing
car_charge_port.yaml         → cover_card ⭐ NEW
car_lock.yaml                → cover_card ⭐ NEW
car_wake_button.yaml         → base_card ✅ existing
```

**Summary**:
- ✅ **Existing templates**: base_card, climate_card, switch_card (you already have)
- ⭐ **NEW templates required**: info_card, cover_card (need to add)

---

## 🚦 Template Dependencies

```
All Templates
    ↓
    └─→ base_card (or setup)
         ↓
         ├─→ light_switch
         ├─→ switch_template
         ├─→ cover_card ⭐ NEW
         ├─→ info_card ⭐ NEW
         └─→ climate_card
```

**Note**: Most templates inherit from `base_card` or `setup`, which provides:
- Border-radius: 24px
- Box-shadow: none
- Haptic feedback
- Standard padding & sizing

---

## 📝 Template Size Reference

```
┌─────────────────────────────────────────────────┐
│  Template Height Comparison                     │
└─────────────────────────────────────────────────┘

sensor_small         ▓▓▓▓▓▓  56px
sensor_medium        ▓▓▓▓▓▓  56px
info_card ⭐         ▓▓▓▓▓▓▓ 75px
light_switch         ▓▓▓▓▓▓▓ 75px
switch_template      ▓▓▓▓▓▓▓ 75px
cover_card ⭐        ▓▓▓▓▓▓▓ 75px
room_card            ▓▓▓▓▓▓▓▓▓▓ 130px (155px when ON)
sensor_big           ▓▓▓▓▓▓▓▓▓▓▓ 129px
climate_card         ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ 194px
car_battery_large    ▓▓▓▓▓▓▓▓▓▓▓▓ 120px (4 cols wide)
room_header          Auto height (no background)
```

---

## 🎨 Template Color Schemes

```yaml
# Your Theme Variables (used by all templates)

Background Colors:
  --contrast1   # Very dark gray
  --contrast2   # Dark gray (default OFF state)
  --contrast4   # Medium-dark gray
  --contrast10  # Medium gray
  --contrast16  # Light gray
  --contrast20  # Very light gray (default text)

Accent Colors:
  --yellow      # Lights ON, Day tariff
  --blue        # Night tariff, Cooling, Covers OPEN
  --green       # Charging, Active, Success
  --red         # High power, Heat, Alerts
  --purple      # Special actions (wake button)
  --black       # Text on colored backgrounds
```

### How Templates Use Colors:

```
light_switch      → yellow (ON), contrast2 (OFF)
switch_template   → green (ON), contrast2 (OFF)
cover_card ⭐     → blue (OPEN), contrast2 (CLOSED)
climate_card      → green (auto), red (heat), blue (cool)
info_card ⭐      → contrast2 (default, customizable)
```

---

## 🔧 Customization Compatibility

All templates support these customizations:

### Color Override
```yaml
template: info_card
styles:
  card:
    - background: var(--purple)  # Override default
```

### Icon Override
```yaml
template: cover_card
icon: mdi:your-custom-icon  # Override default icon
```

### State Display Override
```yaml
template: info_card
state_display: |
  [[[
    return entity.state + ' custom suffix';
  ]]]
```

### Grid Layout Override
```yaml
template: info_card
view_layout:
  grid-column: span 3  # Make wider
  grid-row: span 2     # Make taller
```

---

## 📚 Documentation Cross-Reference

**For complete template details**: See `ALL_TEMPLATES_GUIDE.md`
**For integration steps**: See `TEMPLATES_INSTALL.md`
**For card examples**: See `README.md`
**For quick reference**: See `INDEX.md`
**For fast setup**: See `QUICK_START.md`

---

## ✅ Integration Checklist

Before adding cards, ensure:

- [ ] Added 3 new templates to your dashboard (from ADDON_TEMPLATES.yaml)
- [ ] Verified existing templates still work
- [ ] Checked theme variables exist (--yellow, --blue, etc.)
- [ ] Installed required custom cards:
  - [ ] button-card
  - [ ] apexcharts-card
  - [ ] grid-layout
- [ ] Verified entity IDs match your system
- [ ] Tested one card before adding all

---

**Visual Summary**:
```
15 existing templates + 3 new templates = 18 total templates
     ✅                    ⭐                    🎯

Your dashboard templates + ADDON_TEMPLATES.yaml = Complete system
                                                  ↓
                                    Ready to use 23 energy/car cards!
```
