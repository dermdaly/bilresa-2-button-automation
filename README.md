# Bilresa Light Control Blueprint for Home Assistant

A reusable Home Assistant blueprint for controlling lights or light groups using the **IKEA Bilresa 2-button switch**.

This blueprint replaces multiple duplicated automations with a single, clean, reusable configuration per room.

---

## Features

Control your lights intuitively using button gestures:

- **Button 1 single press** → Increase brightness  
- **Button 2 single press** → Decrease brightness  
- **Button 1 long press** → Set brightness to 100%  
- **Button 2 long press** → Turn off  
- **Button 1 double press** → Warmer (lower Kelvin)  
- **Button 2 double press** → Cooler (higher Kelvin)  

---

##  Why This Blueprint?

If you’ve tried setting this up manually, you’ll know the pain:

- Multiple automations per light
- Lots of duplication
- Hardcoded entity IDs
- Manual tuning of colour temperature steps

This blueprint solves all of that:

- ✅ One automation per room instead of six  
- ✅ No duplicated YAML  
- ✅ No hardcoded entities  
- ✅ Works with any light or light group  
- ✅ Dynamically adapts to each light’s colour temperature range  

---

## How It Works

The blueprint:

- Listens to Bilresa button **event entities**
- Detects gesture types (`multi_press_1`, `multi_press_2`, `long_press`)
- Routes actions using a single automation
- Calculates colour temperature dynamically based on:
  - `min_color_temp_kelvin`
  - `max_color_temp_kelvin`

This ensures consistent behaviour across different bulbs and setups.

---

## Installation

### Option 1: Import via URL (recommended)

1. Go to **Settings → Automations & Scenes → Blueprints**
2. Click **Import Blueprint**
3. Paste the URL to `bilresa_light.yaml` in this repo

---

### Option 2: Manual install

1. Copy `bilresa_light.yaml` to: /config/blueprints/automation/
(or a subfolder, e.g. `/config/blueprints/automation/dermdaly/`)

2. Reload automations:
   - Developer Tools → YAML → **Reload Automations**

---

## Setup

1. Go to **Blueprints**
2. Select this blueprint
3. Click **Create Automation**

Fill in:

| Field | Example |
|------|--------|
| Button 1 event | `event.bilresa_dual_button_button_1_2` |
| Button 2 event | `event.bilresa_dual_button_button_2_2` |
| Target light/group | `light.main_dining_light` |
| Brightness step | 20 |
| Warmth step | 15 |

---

##  Requirements

- Home Assistant with blueprint support
- IKEA Bilresa 2-button switch
- Button exposed as **event entities**
- Lights must support:
  - `brightness`
  - `color_temp_kelvin`

---

## Supported Event Types

Tested with:

- `multi_press_1` → single press  
- `multi_press_2` → double press  
- `long_press` → long press  

These may vary depending on your integration (Matter, Zigbee, etc.). i tested with Bilresa using matter over thread.

---

## Notes on Colour Temperature

Colour temperature is adjusted dynamically using the light’s supported range.

Instead of fixed steps, this blueprint:

- Calculates the full Kelvin range
- Applies a percentage-based step
- Clamps values to avoid invalid ranges

This results in more consistent behaviour across different bulbs.

---

## Troubleshooting

### Blueprint not appearing
- Ensure file is in: /config/blueprints/automation
- Reload automations

---

### Buttons not triggering
- Check event entities in **Developer Tools → States**
- Confirm `event_type` values match your setup

---

### Warmth feels off
- Adjust **Warmth step** (try 10–20%)

---

## Example Use Case

A room with multiple bulbs grouped into a single light:

- Use one Bilresa switch
- Create one automation using this blueprint
- Control brightness and warmth seamlessly across the group

---

## License

MIT License

---

## Author

Dermot Daly  


---

## Contributing

Suggestions and improvements welcome. Feel free to open an issue or PR.