# Quark‑U5‑SOM
Ultra‑low‑power **STM32U5A9** System‑on‑Module in a standard **M.2 2230 Key‑E** card  
<5 mA run‑current · 64 MB Octo‑SPI Flash · 32 MB PSRAM · 8‑bit RGB display · open‑hardware

[![license: CERN‑OHL‑P v2](https://img.shields.io/badge/license-CERN--OHL--P%20v2-blue.svg)](LICENSE)
[![hardware‑release](https://img.shields.io/badge/release‑docs-latest-brightgreen.svg)](docs/)

---

## What is it?
**Quark‑U5‑SOM** is a drop‑in M.2 card that delivers MCU‑class power efficiency with the I/O richness usually found on bigger modules.  
It pairs an STM32U5A9 (Arm Cortex‑M33, TrustZone, LTDC) with dual Octo‑SPI memory, all on a 22 × 30 mm PCB that fits any Key‑E socket.

### Key features
* **< 5 mA** at 120 MHz graphics workload  
* **64 MB NOR + 32 MB PSRAM** on shared Octo‑SPI bus  
* **8‑bit RGB + HSYNC/VSYNC/DE/PCLK** directly from the MCU LTDC  
* **USB‑FS, CAN‑FD, SDIO/SPI**, plenty of GPIO/ADC/PWM  
* Single **3 V3** supply; RTC **VBAT** pin exposed  
* Footprint room for an optional on‑carrier Wi‑Fi/BLE module  
* Completely open: KiCad design files, STEP model, and manufacturing docs licensed under **CERN‑OHL‑P v2**

### Repo structure
* TBD *

### Quick start
1. Plug the SOM into any **Key‑E M.2** socket providing 3 V3.  
2. SWD header on the carrier gives full debug access.  
3. Flash the demo firmware (`firmware/demo_rgb_lcd`) to light up a 480 × 272 TFT.  
4. Typical current: **≈ 4.8 mA** (RGB + SPI + 120 MHz).

> Detailed electrical specs, mechanical drawing, and BOM are in **docs/U5‑2230‑SOM_datasheet.pdf**.

---

## Contributing
Issues, pull requests, and forks are welcome.  
Please read `CODE_OF_CONDUCT.md` before contributing.

---

## License
Hardware design files are released under **CERN‑OHL‑P v2**.  
Software examples are under **MIT**.  See the LICENSE file for details.
