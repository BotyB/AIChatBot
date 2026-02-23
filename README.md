# 🚒 AIChatBot Firetruck

![Main Image](AIChatBot.png)

[---]

# ESP32-S3 Voice Assistant using Xiaozhi API (Xiaozhi Lite, DeepSeek Quantized, DauBao 2.0)

A compact, battery-powered AI voice assistant built inside a firetruck chassis using an ESP32-S3 Supermini, I2S microphone INMP441 , I2S amplifier MAX98357A ,0.96" OLED display , boost converter from 3.7v to 5v, a li-Ion battery 3.7v 800 mAh, TP4056 Charging module and a properly decoupled mixed digital/audio power system.

Designed, engineered and documented by **BotyB**

[---]

# 📦 Project Overview

This project is a fully functional voice chatbot built around:

* ESP32-S3 Supermini
* INMP441 I2S digital microphone
* MAX98357A I2S audio amplifier
* 0.96” OLED (I2C) -> (When searching do check for display to have **4** pins not 8)
* TP4056 Li-Ion charger (modified to 200mA)
* Samsung 3.7V 800mAh Li-Ion battery -> (You can use any space battery you have with good health)
* Boost converter set to 5V
* Proper decoupling & star-ground topology

This build focuses on:

* Stable power delivery
* Audio clarity
* WiFi reliability
* Professional grounding
* Clean enclosure integration
* Proof of concept for a toy integrated AIChatBot

It may look so but this is not a “toy project”. It is a properly engineered, compact mixed-signal embedded system.

[---]

# What You Need with AliExpress examples

## Mandatory Components

* ESP32-S3 Supermini                             -> Link : https://shorturl.at/zLChx
* INMP441 microphone                             -> Link : https://shorturl.at/EX8jN
* MAX98357A amplifier                            -> Link : https://shorturl.at/SnJsn
*Ceramic Capacitors (104)                        -> Link : https://shorturl.at/riOb9
* Electrolytic Capacitors Kit                    -> Link : https://shorturl.at/HwgME
* TP4056 charging module                         -> Link : https://shorturl.at/miefV
* Resistor Kit (adjusted for 200mA charging)     -> Link : https://shorturl.at/NT6mV
* Boost converter (3.7V → 5V)                    -> Link : https://tinyurl.com/4dsx7dfj
* 3.7V Li-Ion battery (800mAh used here)         -> Link : https://tinyurl.com/yyrns89w 
* 0.96” OLED (SSD1306 I2C)                       -> Link : https://tinyurl.com/y2un2hme
* 4-8 Ω  2W speaker                              -> Link : https://tinyurl.com/zsnsfz8t or https://tinyurl.com/299k8ejv


[---]

## 🧪 Optional but Recommended

* Heat shrink tubing
* Silicone glue for vibration resistance
* Multimeter (mandatory for voltage tuning)


[---]

# 🔌 Power Architecture

[DROP_IMAGE_HERE: power_layout_overview.jpg]

## Capacitors Used

| Location     | Value         | Purpose                |
| ------------ | ------------- | ---------------------- |
| Battery Rail | 470µF + 100nF | Input stabilization    |
| Boost Output | 470µF + 100nF | Switching smoothing    |
| MAX98357A    | 470µF + 100nF | Audio spike absorption | -> o.1
| ESP32 Rail   | 470µF + 100nF | WiFi burst buffering   |

**Legend: 470µF are Electrolytic Capacitors 10v or max 16v and 100nF are Ceramic 104 Capacitors**
*o.1 -> You can up 470µF to 680-1000 µF if module stops randomly*

### Why This Works

* Input cap stabilizes battery
* Boost output cap smooths switching
* MAX cap absorbs audio spikes
* ESP32 cap handles WiFi bursts
* Star ground prevents ground noise

This is a properly decoupled mixed digital/audio system.

[---]

# ⚡ Star Grounding Strategy

All grounds meet at a single central node.

Audio ground is not daisy-chained through digital ground.
Boost return is isolated from mic return.

This prevents:

* Digital ticking in speaker
* Mic noise under WiFi load
* Brownouts during audio peaks

[---]

# 🔧 Boost Converter Setup (Set to 5V)

Before connecting ESP32:

1. Power boost converter from battery.
2. Use multimeter on output.
3. Adjust potentiometer until output reads exactly **5.00V**.

[DROP_IMAGE_HERE: boost_converter_adjustment.jpg]

⚠️ Never connect ESP32 before verifying output voltage.

[---]

# 🔋 TP4056 Resistor Modification (200mA Charging)

The TP4056 R3 resistor controls charging current.

Stock modules often charge at 1A — too high for 800mAh cell.

We modified R3 to limit charging to ~200mA.

Formula:

[---]

I_charge = 1000V / R3 (kΩ)

[---]

For ~200mA, use ~5kΩ equivalent.

[DROP_IMAGE_HERE: tp4056_r3_mod.jpg]

This protects:

* Battery lifespan
* Thermal stability
* Safety inside enclosure

[---]

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
The project is using **TanDev's** Flasher and Text-to-Speech backend so all credits are going for him for letting me use his flasher

All credits for AI backend and conversational engine go to:  

https://xiaozhi.me/login?redirect=/console/agents

https://tandev.click

This project integrates the API but does not claim ownership of the service. All services and credits regarding AI Agents go to Xiaozhi AI Team, DeepSeek AI Team.

Users must:

* Register with Xiaozhi
* Obtain API credentials
* Configure WiFi + API keys in firmware
* Configure Agent as pleased
* Re-flash Online, if connected you can directly change the settings.

---

# How to Register & Configure

1. Create Xiaozhi account.
2. Generate API key.
3. Insert credentials into firmware config.
4. Flash updated firmware.
5. Restart device.


[---]

# Audio System

INMP441 → I2S → ESP32
ESP32 → I2S → MAX98357A → Speaker

Fully digital audio path.

No analog mic preamp required.

[DROP_IMAGE_HERE: audio_signal_flow.jpg]

[---]

# Lessons Learned

* Bulk capacitance matters. (Always solder capacitors directly ON module pins and sometimes INLINE)
* Star grounding matters even more. Especially as close as possible to MAIN power Rail e.g. Buck OUT pins, short wires
* Boost converters need proper smoothing in audio systems. Some modules have high sudden drain so they need capacitors for sudden spikes 
* Charging current must match battery capacity. Never Charge small batteries 400 mAh with e.g. 1A, it will overheat or enev blow up on you!
* Twisted wiring significantly reduces interference. Always twist GND and VCC together to cancel any EMI it might pick up
* Mixed digital/audio systems require intentional layout.


[---]


# Built By

Designed and built by ***BotyB***
System architecture & co-engineering: *Brother Thovian*
