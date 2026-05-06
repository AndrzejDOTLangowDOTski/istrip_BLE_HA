# ⚠️ THIS IS A FORK ⚠️

## FORKED FROM [vakintosh/istrip_plus_HA](https://github.com/vakintosh/istrip_plus_HA)

> **VIBE CODED USING AI — Anthropic Claude (free tier)**
>
> Big thank you to [@vakintosh](https://github.com/vakintosh) for the original work.
> I'm sorry for butchering your code with AI. You did the hard part — I just tweaked it with Claude's help. Respect. 🙏

---

# iStrip+ BLE Light — Home Assistant Custom Integration

Custom integration for controlling **Diyife / iStrip+** Bluetooth LED strip lights from Home Assistant.

**Protocol:** Bluetooth Low Energy (BLE), AES-128 ECB encrypted payloads

Tested on:
- Diyife Smart LED Strip Light (model HLS12, 5M, 150 LED)
- Home Assistant OS 17.2 / Core 2026.4.4
- Proxmox with USB Bluetooth passthrough

Based on: [vakintosh/istrip_plus_HA](https://github.com/vakintosh/istrip_plus_HA)

---

## Features

- ON / OFF
- RGB color control
- Brightness (0–255)
- 12 built-in effects
- Per-effect speed control (1–100)
- Auto-reconnect on BLE disconnect
- AES-128 ECB encrypted BLE communication

### Effects

| Effect | Effect |
|---|---|
| 7-Color Fade | 3-Color Fade |
| 7-Color Breathing | 3-Color Breathing |
| 7-Color Flash | 3-Color Flash |
| Red Breathing | Red Strobe |
| Blue Breathing | Blue Strobe |
| Green Breathing | Green Strobe |

### Default speeds per effect type

| Effect type | Default speed | Reason |
|---|---|---|
| Flash (7-Color, 3-Color) | 100 | Fast by design |
| Strobe (Red, Blue, Green) | 100 | Fast by design |
| Breathing (Red, Blue, Green, 7-Color, 3-Color) | 1 | Slow / smooth by design |
| Fade (7-Color, 3-Color) | 1 | Slow / smooth by design |

Speeds are overridable at runtime via `istrip.set_effect` (with optional `speed`) or `istrip.set_speed`.

---

## Requirements

- Home Assistant with Bluetooth integration configured
- USB Bluetooth adapter (if running in VM — USB passthrough required)
- Diyife / iStrip+ BLE LED strip

---

## Installation (manual)

```bash
cd /config/custom_components
git clone https://github.com/AndrzejDOTLangowDOTski/istrip_BLE_HA.git temp_istrip
cp -r temp_istrip/istrip ./istrip
rm -rf temp_istrip
```

Restart Home Assistant, then:

**Settings → Devices & Services → Add Integration → iStrip BLE Light**

---

## Custom Services

### `istrip.set_effect`

| Field | Type | Required | Description |
|---|---|---|---|
| `entity_id` | string | yes | Target light entity |
| `effect` | string | yes | Effect name (see list above) |
| `speed` | int 1–100 | no | Animation speed (overrides default for this effect) |

### `istrip.set_speed`

| Field | Type | Required | Description |
|---|---|---|---|
| `entity_id` | string | yes | Target light entity |
| `speed` | int 1–100 | yes | Speed for current active effect |

---

## Known Limitations

- `subscribe to notifications` warning is expected — it does not affect functionality
- Auto-discovery via Bluetooth requires the device to be advertising
- Only 3 devices can be active simultaneously per BT adapter (hardware limit)

---

## License

MIT
