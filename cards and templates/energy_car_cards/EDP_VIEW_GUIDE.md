# 📊 EDP Energia View - Modern Dashboard Guide

## ✨ What's New

Your EDP Energia view has been completely modernized with:

- ✅ **Button-card design** - All sensors now use custom button cards
- ✅ **Dynamic color coding** - Cards change color based on power consumption
- ✅ **Modern layout** - Header → Overview → Chart → Monitors → Monthly Summary
- ✅ **Responsive grid** - Auto-adjusts for mobile and desktop
- ✅ **24px border-radius** - Matches your design system
- ✅ **Portuguese labels** - All text in Portuguese

---

## 🎨 Layout Structure

### 1. **Header Section**
- Large title: "EDP Energia"
- Subtitle: "Monitorização e análise de consumos"

### 2. **Overview Cards** (Quick Status)
- **Potência Atual** (2 columns wide) - Large gradient card with power status
  - 🔴 Red: > 5000W (Very High)
  - 🟡 Yellow: > 2000W (High)
  - 🔵 Blue: > 500W (Normal)
  - 🟢 Green: < 500W (Low)
- **Período Atual** - Day/Night indicator (yellow/blue)
- **Tarifa** - Current tariff type
- **Dias no Ciclo** - Days in billing cycle

### 3. **Today's Consumption**
- ☀️ **Consumo Dia** - Day period (yellow card)
- 🌙 **Consumo Noite** - Night period (blue card)
- 💰 **Custo Hoje** - Today's cost (2 columns wide)

### 4. **15-Day Consumption Chart**
- Full-width ApexCharts card
- Stacked bar chart (Day vs Night)
- Shows last 15 days
- Data labels with kWh values

### 5. **Power Monitors** (8 Individual Devices)
All cards have dynamic color coding:

**Heater Suite** (Aquecedor Suite)
- 🔴 Red: > 1500W
- 🟡 Yellow: > 500W
- 🔵 Blue: > 10W
- ⚫ Gray: < 10W (Off)

**Server NAS** (Servidor NAS)
- 🔴 Red: > 200W
- 🟡 Yellow: > 100W
- 🔵 Blue: > 10W
- ⚫ Gray: < 10W (Off)

**Unifi Network** (Unifi Rede)
- 🔴 Red: > 100W
- 🟡 Yellow: > 50W
- 🔵 Blue: > 10W
- ⚫ Gray: < 10W (Off)

**Office** (Escritório)
- 🔴 Red: > 300W
- 🟡 Yellow: > 150W
- 🔵 Blue: > 10W
- ⚫ Gray: < 10W (Off)

**Oven & Stove** (Forno & Placa)
- 🔴 Red: > 3000W
- 🟡 Yellow: > 1000W
- 🔵 Blue: > 10W
- ⚫ Gray: < 10W (Off)

**Tesla Charger** (Carregador Tesla)
- 🟢 Green: > 5000W (Fast charging)
- 🔵 Blue: > 1000W (Normal charging)
- 🟡 Yellow: > 10W (Slow/idle)
- ⚫ Gray: < 10W (Off)

**Living Room & Kitchen** (Sala & Cozinha)
- 🔴 Red: > 2000W
- 🟡 Yellow: > 500W
- 🔵 Blue: > 10W
- ⚫ Gray: < 10W (Off)

**Heat Pump** (Bomba de Calor)
- 🔴 Red: > 2000W
- 🟡 Yellow: > 800W
- 🔵 Blue: > 10W
- ⚫ Gray: < 10W (Off)

### 6. **Monthly Cycle Summary**
- ☀️ **Total Dia (Ciclo)** - Monthly day consumption (yellow)
- 🌙 **Total Noite (Ciclo)** - Monthly night consumption (blue)
- **Total do Ciclo** - Monthly total (2 columns wide)
- 💰 **Custo Total do Ciclo** - Monthly cost (purple, 2 columns wide)
- **Markdown Info Card** - Detailed cycle information

### 7. **Tariff Configuration**
- Entities card with all EDP configuration inputs
- Prices, IVA rates, contracted power, etc.

---

## 🎯 Color Coding System

### Power Cards (Consumption Level)
```
🔴 Red    = Very High / Critical
🟡 Yellow = High / Warning
🔵 Blue   = Normal / Active
🟢 Green  = Low / Efficient (or Tesla charging)
⚫ Gray   = Off / Standby (< 10W)
```

### Period Cards
```
🟡 Yellow = Day Period (☀️)
🔵 Blue   = Night Period (🌙)
```

### Cost Cards
```
🟣 Purple = Financial information
```

---

## 📐 Grid Layout

The view uses a responsive grid:
- **Desktop**: Auto-fills columns (typically 4-6 cards per row)
- **Mobile**: Adapts to single column or 2 columns
- **Gap**: 12px spacing between cards
- **Padding**: 12px around edges

### Column Spanning
- **Regular cards**: 1 column
- **Wide cards**: 2 columns (Potência Atual, costs, totals)
- **Full width**: All columns (Headers, chart, markdown, entities)

---

## 🔧 Customization Options

### Change Power Thresholds

Edit the card's `styles` section:

```yaml
- background: |
    [[[
      var power = parseFloat(entity.state);
      if (power > YOUR_RED_VALUE) return "var(--red)";
      else if (power > YOUR_YELLOW_VALUE) return "var(--yellow)";
      else if (power > YOUR_BLUE_VALUE) return "var(--blue)";
      else return "var(--contrast2)";
    ]]]
```

### Change Icons

```yaml
icon: mdi:your-custom-icon
```

### Change Card Size

```yaml
view_layout:
  grid-column: span 2  # Make card 2 columns wide
```

### Add New Power Monitor

Copy any existing power monitor card and update:
1. `entity:` - Your sensor entity ID
2. `name:` - Display name
3. `icon:` - MDI icon
4. Power thresholds in the `styles` section

---

## 📊 Required Templates

This view uses these templates (make sure they're in your dashboard):

1. ✅ **room_header** - For section titles
2. ✅ **info_card** - For most sensor displays
3. ✅ **ApexCharts card** - For the consumption chart

---

## 📱 Mobile vs Desktop

**Desktop View:**
- 4-6 cards per row
- Full-width chart
- Comfortable spacing

**Mobile View:**
- 2 cards per row (or 1 for wide cards)
- Scrollable
- Touch-optimized

---

## 🚀 Installation

### Option 1: Copy Entire View

1. Open your dashboard in **Edit mode**
2. Click **⋮ menu** → **Raw configuration editor**
3. Add a new view section
4. Copy the entire content from `edp_energia_view.yaml`
5. Paste into your dashboard
6. **Save**

### Option 2: Manual Card-by-Card

1. Create a new view:
   - Title: "EDP Energia"
   - Path: "edp"
   - Icon: "mdi:flash"
   - Type: "custom:grid-layout"
2. Add cards one by one from the file

---

## ⚠️ Important Notes

### Entity IDs
Make sure these entities exist in your system:
- `sensor.w_shelly_todos_juntos`
- `sensor.edp_periodo_atual`
- `sensor.um_diario_daily`
- `sensor.um_diario_nightly`
- `sensor.edp_valor_diario_euros`
- All power monitor sensors (8 total)
- All monthly sensors
- All config input_numbers

### Dependencies
Required custom cards:
- ✅ **button-card** (all button cards)
- ✅ **apexcharts-card** (consumption chart)
- ✅ **layout-card** (grid layout)
- ⚠️ **card-mod** (optional, for markdown styling)

### Theme Variables
Required theme variables:
- `--red`, `--yellow`, `--blue`, `--green`, `--purple`
- `--black`
- `--contrast2`, `--contrast16`, `--contrast20`

---

## 🎨 Visual Examples

### Power Card States

**High Power (Red):**
```
┌─────────────────────┐
│ 🔥 Forno & Placa    │ RED BACKGROUND
│                     │
│ 3500 W              │ BLACK TEXT
└─────────────────────┘
```

**Medium Power (Yellow):**
```
┌─────────────────────┐
│ ⚡ Servidor NAS     │ YELLOW BACKGROUND
│                     │
│ 150 W               │ BLACK TEXT
└─────────────────────┘
```

**Low Power (Blue):**
```
┌─────────────────────┐
│ 💻 Escritório       │ BLUE BACKGROUND
│                     │
│ 50 W                │ BLACK TEXT
└─────────────────────┘
```

**Off (Gray):**
```
┌─────────────────────┐
│ 🔌 Unifi Rede       │ GRAY BACKGROUND
│                     │
│ 0 W                 │ LIGHT TEXT
└─────────────────────┘
```

---

## 📈 Comparison: Old vs New

### Old View (Sections)
- ❌ Mixed card types (gauge, glance, entities, sensor)
- ❌ Inconsistent styling
- ❌ Static colors
- ❌ Line graphs for all sensors
- ❌ Sections layout (limited flexibility)

### New View (Grid Layout)
- ✅ Unified button-card design
- ✅ Consistent 24px border-radius
- ✅ Dynamic color coding (8 color states)
- ✅ Modern gradient cards
- ✅ Responsive grid layout
- ✅ Better visual hierarchy
- ✅ Touch-optimized for mobile

---

## 🎯 Tips

1. **Quick Status**: Top cards give you instant overview
2. **Device Monitoring**: Color-coded cards show what's consuming power
3. **Cost Tracking**: Today and monthly costs clearly displayed
4. **Trend Analysis**: 15-day chart shows consumption patterns
5. **Cycle Management**: Full billing cycle information at bottom

---

**File**: `edp_energia_view.yaml`
**Created**: 2025-11-26
**Design System**: 24px border-radius, Portuguese labels, Dark theme
**Layout**: Responsive grid with 12px gaps
**Total Cards**: ~30 cards (1 header + 4 overview + 3 today + 1 chart + 8 monitors + section headers + monthly + config)
