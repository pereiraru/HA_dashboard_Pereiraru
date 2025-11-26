# Energy & Car Cards Collection

Individual button-card components for Energy monitoring and Tesla car control.

## 📁 Folder Contents

### ⚡ Energy Cards (9 cards)

**Current Status:**
- `energy_current_power.yaml` - Live power consumption with color coding (red >5kW, yellow >2kW)
- `energy_period.yaml` - Current tariff period (Day/Night) with sun/moon icon

**Today's Consumption:**
- `energy_today_total.yaml` - Total consumption today
- `energy_today_day.yaml` - Day period consumption (yellow background)
- `energy_today_night.yaml` - Night period consumption (blue background)
- `energy_cost_today.yaml` - Today's cost in euros

**Monthly Consumption:**
- `energy_monthly_total.yaml` - Total monthly consumption (billing cycle)
- `energy_monthly_cost.yaml` - Monthly cost in euros

**Charts:**
- `energy_chart_15days.yaml` - ApexCharts 15-day history (Day vs Night stacked bars)

### 🚗 Tesla Car Cards (14 cards)

**Battery & Charging:**
- `car_battery_large.yaml` - Large gradient battery display with range (spans 4 columns, 2 rows)
- `car_charging_status.yaml` - Charging state (green when charging)
- `car_charger_power.yaml` - Charger power in kW
- `car_time_to_full.yaml` - Time to full charge
- `car_charge_limit.yaml` - Charge limit percentage (tap for more-info)

**Vehicle Info:**
- `car_odometer.yaml` - Mileage/kilometers
- `car_range.yaml` - Battery range in km
- `car_temp_inside.yaml` - Interior temperature
- `car_temp_outside.yaml` - Exterior temperature

**Climate & Controls:**
- `car_climate.yaml` - AC control (tap for more-info)
- `car_charge_switch.yaml` - Start/stop charging switch
- `car_charge_port.yaml` - Charge port door cover
- `car_lock.yaml` - Door lock status and control
- `car_wake_button.yaml` - Wake up Tesla button (purple)

---

## 🎨 Design Features

All cards use the **button-card template system** from your main dashboard:

- **Templates used**: `info_card`, `switch_card`, `cover_card`, `base_card`, `room_header`
- **24px border-radius** - Rounded corners matching your theme
- **Dynamic colors**:
  - Yellow - Lights/Day tariff
  - Blue - Night tariff/Cooling
  - Green - Charging/Active
  - Red - High consumption/Heat
  - Purple - Special actions
- **Responsive grid** - Cards span 2 columns by default (battery_large spans 4)

---

## 📖 How to Use These Cards

### Option 1: Copy Individual Cards to Dashboard

1. Open Home Assistant dashboard in edit mode
2. Add new card → Manual card
3. Copy contents of desired `.yaml` file
4. Paste and save

### Option 2: Build a Complete Page

Create an Energy page combining multiple cards:

```yaml
- title: Energia
  path: energia
  icon: mdi:lightning-bolt
  type: custom:grid-layout
  layout:
    grid-template-columns: repeat(auto-fill, minmax(min(100%, 160px), 1fr))
    grid-template-rows: auto
    grid-gap: 12px
    padding: 12px
  cards:
    # Page header
    - type: custom:button-card
      name: Energia
      label: Monitorização EDP e consumos
      template: room_header
      view_layout:
        grid-column: 1 / -1

    # Add individual cards here
    # Copy from energy_current_power.yaml
    # Copy from energy_period.yaml
    # etc.
```

### Option 3: Include in Existing Lovelace

For YAML dashboards, use `!include`:

```yaml
# In your main dashboard file
cards:
  - !include energy_car_cards/energy_current_power.yaml
  - !include energy_car_cards/energy_period.yaml
  - !include energy_car_cards/car_battery_large.yaml
```

---

## 🔧 Customization

### Change Colors

Edit the `styles` section in any card:

```yaml
styles:
  card:
    - background: var(--your-color)  # Change color
    # Available colors: --yellow, --blue, --green, --red, --purple
```

### Adjust Grid Span

```yaml
view_layout:
  grid-column: span 2  # Change number (1-4)
  grid-row: span 2     # For taller cards
```

### Change Icons

```yaml
icon: mdi:your-icon-name  # Browse icons at materialdesignicons.com
```

### Modify Text/Labels

```yaml
name: Your Custom Name
label: Your custom subtitle
```

---

## 📋 Required Templates

These cards require the templates defined in your `dashboard_novo.yaml`:

- `base_card` - Foundation
- `info_card` - Status display
- `switch_card` - Switches/toggles
- `cover_card` - Covers/doors
- `room_header` - Section headers

Make sure these templates are loaded in your dashboard!

---

## 🚀 Quick Start - Energy Page Example

```yaml
cards:
  # Header
  - type: custom:button-card
    name: Energia
    template: room_header
    view_layout:
      grid-column: 1 / -1

  # Current status row
  - !include energy_car_cards/energy_current_power.yaml
  - !include energy_car_cards/energy_period.yaml

  # Today's consumption
  - !include energy_car_cards/energy_today_total.yaml
  - !include energy_car_cards/energy_today_day.yaml
  - !include energy_car_cards/energy_today_night.yaml
  - !include energy_car_cards/energy_cost_today.yaml

  # Chart
  - !include energy_car_cards/energy_chart_15days.yaml
```

---

## 🚙 Quick Start - Car Page Example

```yaml
cards:
  # Header
  - type: custom:button-card
    name: Tesla Model Y
    label: 🔋 Ze das Pilhas
    template: room_header
    view_layout:
      grid-column: 1 / -1

  # Large battery display (takes 4 columns, 2 rows)
  - !include energy_car_cards/car_battery_large.yaml

  # Status row
  - !include energy_car_cards/car_charging_status.yaml
  - !include energy_car_cards/car_charger_power.yaml

  # Info row
  - !include energy_car_cards/car_odometer.yaml
  - !include energy_car_cards/car_range.yaml
  - !include energy_car_cards/car_temp_inside.yaml
  - !include energy_car_cards/car_temp_outside.yaml

  # Controls
  - !include energy_car_cards/car_charge_switch.yaml
  - !include energy_car_cards/car_climate.yaml
  - !include energy_car_cards/car_lock.yaml
  - !include energy_car_cards/car_wake_button.yaml
```

---

## 🔍 Entity Reference

### Energy Entities Used
- `sensor.w_shelly_todos_juntos` - Current power (W)
- `sensor.edp_periodo_atual` - Current period (daily/nightly)
- `sensor.edp_dia_total_kwh_consumidos` - Total today (kWh)
- `sensor.edp_daily_kwh` - Day consumption (kWh)
- `sensor.edp_nightly_kwh` - Night consumption (kWh)
- `sensor.edp_valor_diario_euros` - Daily cost (€)
- `sensor.mensal_kwh_total` - Monthly total (kWh)
- `sensor.edp_valor_mensal_euros` - Monthly cost (€)
- `sensor.um_diario_daily` - Daily meter (for chart)
- `sensor.um_diario_nightly` - Nightly meter (for chart)

### Tesla Entities Used
- `sensor.ze_das_pilhas_battery_level` - Battery %
- `sensor.ze_das_pilhas_battery_range` - Range (km)
- `sensor.ze_das_pilhas_charging` - Charging status
- `sensor.ze_das_pilhas_charger_power` - Charger power (kW)
- `sensor.ze_das_pilhas_time_to_full_charge` - Time to full
- `number.ze_das_pilhas_charge_limit` - Charge limit %
- `sensor.ze_das_pilhas_odometer` - Odometer
- `sensor.ze_das_pilhas_inside_temperature` - Inside temp
- `sensor.ze_das_pilhas_outside_temperature` - Outside temp
- `climate.ze_das_pilhas_climate` - AC control
- `switch.ze_das_pilhas_charge` - Charge on/off
- `cover.ze_das_pilhas_charge_port_door` - Charge port
- `lock.ze_das_pilhas` - Door lock
- `button.ze_das_pilhas_wake` - Wake button

---

## 🎯 Tips & Best Practices

1. **Test individually first** - Add one card at a time to verify entities exist
2. **Check entity IDs** - Use Developer Tools → States to verify your entity names
3. **Mobile vs Desktop** - Grid layout automatically adjusts for screen size
4. **Color customization** - Modify gradient colors in `car_battery_large.yaml` for your preference
5. **ApexCharts** - Requires HACS custom card `apexcharts-card`

---

## 🐛 Troubleshooting

### Card shows "Entity not found"
- Check entity ID in Developer Tools → States
- Verify entity name matches exactly (case-sensitive)

### Colors not working
- Ensure theme variables are defined (`--yellow`, `--blue`, etc.)
- Check theme is active in your dashboard

### Templates not found
- Make sure `dashboard_novo.yaml` templates are loaded
- Check `button_card_templates` section exists

### Chart not displaying
- Install `apexcharts-card` via HACS
- Clear browser cache
- Check browser console for errors

---

**Created**: 2025-11-26
**Dashboard**: Portuguese labels, dark theme, rounded design
**Compatible with**: Home Assistant 2025.11.3+
