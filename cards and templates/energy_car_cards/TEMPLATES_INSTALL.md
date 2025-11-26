# Button Card Templates - Installation Guide

## 📋 What is this file?

`button_card_templates.yaml` contains all the templates needed for the energy and car cards to work properly.

## 🎯 Templates Included

1. **base_card** - Foundation for all cards
2. **light_card** - Light controls with toggle icon
3. **switch_card** - Switch/device controls
4. **climate_card** - Climate control with temperature adjustment
5. **cover_card** - Cover/shutter controls
6. **room_header** - Page section headers
7. **info_card** - Status display cards

---

## 🚀 Installation Methods

### Method 1: Add to Raw Dashboard Configuration (Recommended)

**For new dashboards or testing:**

1. Go to **Settings → Dashboards**
2. Click **"+ ADD DASHBOARD"**
3. Name it (e.g., "Dashboard Energia")
4. After creation, click **⋮ menu → Edit Dashboard**
5. Click **⋮ menu → Raw configuration editor**
6. **Copy the ENTIRE contents** of `button_card_templates.yaml`
7. **Paste at the TOP** of your dashboard YAML, before `views:`

Your dashboard should look like this:

```yaml
button_card_templates:
  base_card:
    tap_action:
      action: toggle
    # ... rest of templates ...

  info_card:
    # ... template definition ...

views:
  - title: Home
    path: home
    cards:
      # Your cards here
```

8. Click **SAVE**

---

### Method 2: Add to Existing Dashboard

**If you already have a dashboard:**

1. Edit your dashboard → **Raw configuration editor**
2. Find the `button_card_templates:` section (if it exists)
3. **Copy the templates** from `button_card_templates.yaml`
4. **Paste them INSIDE** the existing `button_card_templates:` section
5. Make sure indentation is correct
6. Click **SAVE**

Example - Merging with existing templates:

```yaml
button_card_templates:
  # Your existing templates
  my_old_template:
    styles:
      card:
        - background: red

  # Add new templates below
  base_card:
    tap_action:
      action: toggle
    # ...

  info_card:
    # ...

views:
  # Your views
```

---

### Method 3: Include in YAML Mode Dashboard

**For advanced users with YAML mode dashboards:**

1. Save `button_card_templates.yaml` to your Home Assistant config directory:
   ```
   /homeassistant/dashboards/button_card_templates.yaml
   ```

2. In your main dashboard file, include it:
   ```yaml
   button_card_templates: !include dashboards/button_card_templates.yaml

   views:
     - title: Home
       # ...
   ```

---

## ✅ Verification

After installation, test if templates work:

1. Add a test card to any view:
   ```yaml
   - type: custom:button-card
     entity: light.any_light
     name: Test
     template: light_card
   ```

2. If the card displays correctly with rounded corners and proper styling, templates are working!

3. If you get an error "Template light_card not found":
   - Check templates are at the TOP of the dashboard
   - Verify indentation is correct
   - Clear browser cache and refresh

---

## 🎨 Theme Variables Required

These templates use theme variables. Make sure your theme defines:

```yaml
# In your theme file
contrast1: "#1a1a1a"
contrast2: "#2a2a2a"
contrast4: "#3a3a3a"
contrast10: "#5a5a5a"
contrast16: "#7a7a7a"
contrast20: "#9a9a9a"
black: "#000000"
white: "#ffffff"
yellow: "#FFD700"
blue: "#42A5F5"
green: "#4CAF50"
red: "#F44336"
purple: "#9C27B0"
```

If colors don't look right, adjust these in your active theme.

---

## 📦 What's Next?

After installing templates, you can use any of the energy or car cards:

1. **Copy individual card YAML** from the card files
2. **Paste into your dashboard** under a view's `cards:` section
3. Cards will automatically use the templates!

Example:
```yaml
views:
  - title: Energia
    path: energia
    cards:
      - type: custom:button-card
        entity: sensor.w_shelly_todos_juntos
        name: Potência Atual
        template: info_card
        # ... rest from energy_current_power.yaml
```

---

## 🐛 Troubleshooting

### "Template not found" error
- Templates must be at dashboard root level, not inside views
- Check YAML indentation (use 2 spaces, not tabs)
- Restart Home Assistant if needed

### Cards look broken
- Verify theme variables are defined
- Check browser developer console for errors
- Ensure `custom:button-card` is installed (HACS)

### Styles not applying
- Clear browser cache (Ctrl+F5)
- Check theme is active
- Verify no YAML syntax errors

---

## 📝 Example: Complete Dashboard with Templates

```yaml
# Copy from button_card_templates.yaml
button_card_templates:
  base_card:
    # ... all templates here ...
  light_card:
    # ...
  info_card:
    # ...

# Your dashboard views
views:
  - title: Energia
    path: energia
    type: custom:grid-layout
    layout:
      grid-template-columns: repeat(auto-fill, minmax(min(100%, 160px), 1fr))
      grid-gap: 12px
      padding: 12px
    cards:
      # Copy from energy_current_power.yaml
      - type: custom:button-card
        entity: sensor.w_shelly_todos_juntos
        name: Potência Atual
        template: info_card
        # ...

      # Copy from energy_period.yaml
      - type: custom:button-card
        entity: sensor.edp_periodo_atual
        name: Período Atual
        template: info_card
        # ...

  - title: Carro
    path: carro
    cards:
      # Copy from car_battery_large.yaml
      # ...
```

---

**Need Help?**
- Check the main README.md for card usage examples
- Verify all entity IDs match your system
- Test one card at a time

**Ready to go!** 🚀
