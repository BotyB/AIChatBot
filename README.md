# 🚒 AIChatBot Firetruck

[AIChatBot.png]

#

# ESP32-S3 Voice Assistant using Xiaozhi API (Xiaozhi Lite, DeepSeek Quantized, DauBao 2.0)

A compact, battery-powered AI voice assistant built inside a firetruck chassis using an ESP32-S3 Supermini, I2S microphone INMP441 , I2S amplifier MAX98357A ,0.96" OLED display , boost converter from 3.7v to 5v, a li-Ion battery 3.7v 800 mAh, TP4056 Charging module and a properly decoupled mixed digital/audio power system.

Designed, engineered and documented by **BotyB**
Co-engineered with **Brother Thovian**

[---]

# 📦 Project Overview

This project is a fully functional voice chatbot built around:

* ESP32-S3 Supermini
* INMP441 I2S digital microphone
* MAX98357A I2S audio amplifier
* 0.96” OLED (I2C)
* TP4056 Li-Ion charger (modified to 200mA)
* Samsung 3.7V 800mAh Li-Ion battery
* Boost converter set to 5V
* Proper decoupling & star-ground topology

This build focuses on:

* Stable power delivery
* Audio clarity
* WiFi reliability
* Professional grounding
* Clean enclosure integration

It may look so but this is not a “toy project”. It is a properly engineered, compact mixed-signal embedded system.

[---]

# 🧰 What You Need

## 🔩 Mandatory Components

* ESP32-S3 Supermini
* INMP441 microphone
* MAX98357A amplifier
* 4–5 × 100nF ceramic capacitors (104)
* 3–4 × 470µF electrolytic capacitors
* TP4056 charging module
* R3 resistor (adjusted for 200mA charging)
* Boost converter (3.7V → 5V)
* 3.7V Li-Ion battery (800mAh used here)
* 0.96” OLED (SSD1306 I2C)
* 4Ω speaker
* Proper wiring

---

## 🧪 Optional but Recommended

* Heat shrink tubing
* Silicone glue for vibration resistance
* Multimeter (mandatory for voltage tuning)
* Oscilloscope (if you want to be obsessive)

---

# 🔌 Power Architecture

[DROP_IMAGE_HERE: power_layout_overview.jpg]

## Capacitors Used

| Location     | Value         | Purpose                |
| ------------ | ------------- | ---------------------- |
| Battery Rail | 470µF         | Input stabilization    |
| Boost Output | 470µF         | Switching smoothing    |
| MAX98357A    | 470µF + 100nF | Audio spike absorption |
| ESP32 Rail   | 470µF + 100nF | WiFi burst buffering   |
| Distributed  | 4–5 × 100nF   | Local decoupling       |

### Why This Works

* Input cap stabilizes battery
* Boost output cap smooths switching
* MAX cap absorbs audio spikes
* ESP cap handles WiFi bursts
* Star ground prevents ground noise

This is a properly decoupled mixed digital/audio system.

---

# ⚡ Star Grounding Strategy

All grounds meet at a single central node.

Audio ground is not daisy-chained through digital ground.
Boost return is isolated from mic return.

This prevents:

* Digital ticking in speaker
* Mic noise under WiFi load
* Brownouts during audio peaks

---

# 🔧 Boost Converter Setup (Set to 5V)

Before connecting ESP32:

1. Power boost converter from battery.
2. Use multimeter on output.
3. Adjust potentiometer until output reads exactly **5.00V**.

[DROP_IMAGE_HERE: boost_converter_adjustment.jpg]

⚠️ Never connect ESP32 before verifying output voltage.

---

# 🔋 TP4056 Resistor Modification (200mA Charging)

The TP4056 R3 resistor controls charging current.

Stock modules often charge at 1A — too high for 800mAh cell.

We modified R3 to limit charging to ~200mA.

Formula:

```
I_charge = 1000V / R3 (kΩ)
```

For ~200mA, use ~5kΩ equivalent.

[DROP_IMAGE_HERE: tp4056_r3_mod.jpg]

This protects:

* Battery lifespan
* Thermal stability
* Safety inside enclosure

---

# 🧵 Wiring Best Practices

* Twist all power wires (VCC + GND pairs)
* Twist speaker wires
* Keep I2S lines short
* Keep boost converter physically separated from microphone

[DROP_IMAGE_HERE: twisted_wires_example.jpg]

Twisting wires reduces:

* EMI
* Switching noise
* Audio interference

---

# 🧪 Breadboard Version

Before sealing inside chassis, build and test on breadboard.

[DROP_IMAGE_HERE: breadboard_version.jpg]

Test for:

* WiFi stability
* Audio playback
* Mic input clarity
* No brownouts under load

Never seal a system you haven’t tested outside enclosure.

---

# 💻 How to Flash the ESP32

1. Install ESP32 board support in Arduino IDE or use PlatformIO.
2. Connect ESP32-S3 via USB.
3. Select correct COM port.
4. Flash firmware.
5. Monitor Serial output for errors.

If boot fails:

* Hold BOOT button during flashing.

[DROP_IMAGE_HERE: flashing_process.jpg]

---

# 🌐 Xiaozhi API Integration

This project uses the Xiaozhi API for AI chat functionality.

All credits for AI backend and conversational engine go to:

👉 Xiaozhi AI Team

This project integrates the API but does not claim ownership of the service.

Users must:

* Register with Xiaozhi
* Obtain API credentials
* Configure WiFi + API keys in firmware

---

# 📝 How to Register & Configure

1. Create Xiaozhi account.
2. Generate API key.
3. Insert credentials into firmware config.
4. Flash updated firmware.
5. Restart device.

[DROP_IMAGE_HERE: api_configuration.jpg]

⚠️ Never upload API keys to GitHub.

---

# 🔊 Audio System

INMP441 → I2S → ESP32
ESP32 → I2S → MAX98357A → Speaker

Fully digital audio path.

No analog mic preamp required.

[DROP_IMAGE_HERE: audio_signal_flow.jpg]

---

# 🎯 Lessons Learned

* Bulk capacitance matters.
* Star grounding matters even more.
* Boost converters need proper smoothing in audio systems.
* Charging current must match battery capacity.
* Twisted wiring significantly reduces interference.
* Mixed digital/audio systems require intentional layout.

---

# 🚀 Future Improvements

* Custom PCB
* Better enclosure thermal routing
* Larger battery option
* Offline speech model integration
* OTA firmware updates

---

# 🏷 Built By

Designed and built by **Boty Von**
System architecture & co-engineering: *Brother Thovian* ⚙️

Codename preserved for archival continuity.

---

Brother…

This README now reads like an engineered embedded system project — not a weekend Arduino experiment.

If you want next, we can:

* Make it slightly more corporate (for recruiters)
* Or slightly more Adeptus Mechanicus
* Or prepare a second version optimized for CV portfolio

Your move.
