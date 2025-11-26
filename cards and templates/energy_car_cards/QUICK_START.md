# Quick Start Guide - Energy & Car Cards

## 🎯 Goal
Get energy monitoring and Tesla car cards working in your Home Assistant dashboard in 5 minutes.

---

## ⚡ Step 1: Install Templates (2 minutes)

1. Open Home Assistant
2. Go to **Settings → Dashboards → + ADD DASHBOARD**
3. Name it: **"Energia e Carro"**
4. After creation: **⋮ menu → Edit Dashboard → ⋮ menu → Raw configuration editor**
5. **Copy ALL contents** from `button_card_templates.yaml`
6. **Paste at the very top** (before any `views:`)
7. Click **SAVE**

✅ Templates are now loaded!

---

## 📊 Step 2: Add Energy Cards (2 minutes)

Still in Raw configuration editor, scroll down to find `views:` and add:

```yaml
views:
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
        label: Monitorização EDP
        template: room_header
        view_layout:
          grid-column: 1 / -1

      # Now copy cards from:
      # - energy_current_power.yaml
      # - energy_period.yaml
      # - energy_today_total.yaml
      # etc.
```

**Copy each card's YAML content** and paste under `cards:`

---

## 🚗 Step 3: Add Car Cards (1 minute)

Add another view:

```yaml
  - title: Carro
    path: carro
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
        label: Ze das Pilhas
        template: room_header
        view_layout:
          grid-column: 1 / -1

      # Copy cards from:
      # - car_battery_large.yaml (must be first - it's big!)
      # - car_charging_status.yaml
      # - car_charger_power.yaml
      # etc.
```

---

## ✅ Step 4: Save & Test

1. Click **SAVE**
2. Navigate to your new dashboard
3. Check "Energia" tab
4. Check "Carro" tab
5. Done! 🎉

---

## 🎨 Recommended Card Order

### Energy Page (Best Layout)
1. Header (room_header)
2. Current Power + Period (2 cards in row)
3. Today Total + Today Day + Today Night + Cost (4 cards)
4. Monthly Total + Monthly Cost (2 cards)
5. 15-day Chart (full width)

### Car Page (Best Layout)
1. Header (room_header)
2. Battery Large (takes 4 columns, 2 rows - BIG!)
3. Charging Status + Charger Power (2 cards)
4. Time to Full + Charge Limit (2 cards)
5. Odometer + Range (2 cards)
6. Temp Inside + Temp Outside (2 cards)
7. Climate + Charge Switch (2 cards)
8. Charge Port + Lock (2 cards)
9. Wake Button (1 card)

---

## 🐛 Quick Troubleshooting

**"Template not found"**
→ Templates must be at TOP of file, before `views:`

**Card shows entity not found**
→ Check entity ID in Developer Tools → States

**Colors look wrong**
→ Make sure your theme defines the color variables

**ApexChart not showing**
→ Install `apexcharts-card` from HACS

---

## 📁 Files You Need

✅ `button_card_templates.yaml` - **REQUIRED** - Install first
✅ Individual card files - Copy as needed
📖 `README.md` - Detailed documentation
📖 `INDEX.md` - Quick card reference
📖 `TEMPLATES_INSTALL.md` - Detailed template installation

---

## 💡 Pro Tips

1. **Start small** - Add 2-3 cards first, test, then add more
2. **Test entities** - Use Developer Tools to verify entity IDs exist
3. **Save often** - Save after adding each card to catch errors early
4. **Mobile view** - Grid layout adapts automatically for mobile
5. **Customize later** - Get it working first, customize colors/icons after

---

**Total Time**: ~5 minutes
**Difficulty**: Easy (copy/paste)
**Result**: Professional energy monitoring + Tesla control! 🎉
