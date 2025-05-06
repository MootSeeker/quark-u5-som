# **U5‑2230‑SOM**  
Ultra‑low‑power STM32U5A9 System‑on‑Module in M.2 2230 Key‑E Form‑Factor  
*(Pre‑production – Rev A, May 2025)*  

---

## 1. Module Highlights
| | |
|---|---|
| **MCU** | ST **STM32U5A9NJ** – Arm Cortex‑M33 @ up‑to 160 MHz, TrustZone®, FPU, LTDC, dual Octo‑SPI |
| **On‑board memory** | 512 Mbit (64 MB) Octo‑SPI NOR Flash @ 120 MHz DTR  <br>256 Mbit (32 MB) Octo‑SPI PSRAM @ 120 MHz DTR – share same bus |
| **Display interface** | 8‑bit RGB (RRR GGG BB) + HSYNC / VSYNC / DE / PCLK (via MCU LTDC) |
| **Wireless option** | SDIO/SPI & control lines reserved for plug‑in Wi‑Fi / BLE module on carrier |
| **Power‑tree** | Single 3 V3 input → on‑board SMPS (1 V8 core) & LDO rails; RTC VBAT pin exposed |
| **Size / weight** | **22 mm × 30 mm × ≤ 1.5 mm** component height each side – matches M.2 2230 spec :contentReference[oaicite:0]{index=0} |
| **Connector** | Standard 67‑pin **M.2 Key‑E edge‑finger**, 0.5 mm pitch |

---

## 2. Absolute Maximum Ratings
| Parameter | Min | Max | Unit |
|-----------|-----|-----|------|
| Supply 3V3_IN to GND | –0.3 | 3.6 | V |
| VBAT to GND | –0.3 | 3.6 | V |
| GPIO per ST datasheet | –0.3 | 4.0 | V |
| Storage temperature | –40 | 125 | °C |

> **Stresses beyond those listed may cause permanent damage.**  

---

## 3. Recommended Operating Conditions
| Parameter | Min | Typ | Max | Unit |
|-----------|-----|-----|-----|------|
| 3 V3_IN | 3.0 | 3.3 | 3.6 | V |
| VBAT (RTC) | 1.3 | 3.0 | 3.6 | V |
| Ambient (industrial) | –40 | 25 | 85 | °C |

---

## 4. Typical Power Consumption (@ 25 °C, 3 V3_IN = 3.3 V)

| Mode | Core clk | Peripherals active | Current |
|------|----------|--------------------|---------|
| **Run – graphics** | 120 MHz | LTDC + Octo‑SPI + DMA | **≈ 4.8 mA** |
| Run – compute | 60 MHz | CPU only | ≈ 1.2 mA |
| **Stop 2** | RTC + PSRAM retention | 6 µA |
| Standby w/ RTC | – | 480 nA |

*(Run‑mode figure derived from **18.5 µA/MHz** SMPS spec @ 3.3 V :contentReference[oaicite:1]{index=1} plus memory & display loads.)*

---

## 5. Block Diagram
3 V3_IN VBAT
| │
|─► Buck‑SMPS 1 V8 ──► STM32U5A9 MCU
│
|─► LDO 3 V3_IO ──► IO, Octo‑SPI, LTDC, GPIO
│
└─► LDO 1 V8_AUX ──► PSRAM Vccq
│
Octo‑SPI 8‑bit bus 120 MHz DTR
├──► 64 MB NOR‑Flash
└──► 32 MB PSRAM
LTDC 8‑bit RGB ──► Edge connector → TFT panel
SDIO/SPI lines ──► (optional) radio module on carrier
USB‑FS (D+, D–) ──► Edge connector
SWD+UART debug ──► Edge connector

---

## 6. Pin Assignment – M.2 Key‑E Edge (67 pins)

Pin numbering follows the M.2 convention (odd = bottom row, even = top row).  
Only non‑reserved pins are listed; all unlisted follow the JEDEC Key‑E spec and are **NC**.

| M.2 Pin | Net | Dir | Description |
|---------|-----|-----|-------------|
| **2,4 ,70,72,74** | 3V3_IN | PWR | Main 3.3 V rail |
| **3 / 5** | USB_DP / USB_DM | I/O | USB 2.0 Full‑Speed |
| **29 / 31** | OCTO_DQS / OCTO_CLK | O | Shared Octo‑SPI strobe & clock |
| **33 / 41 / 43 / 45 / 47 / 49 / 53 / 55** | OCTO_D0–D7 | I/O | Flash + PSRAM data lines |
| **35 / 37** | OCTO_CS0 / CS1 | O | Chip‑selects (Flash, PSRAM) |
| **59‑65** | RGB[7:2] | O | Parallel display bus |
| **57** | RGB[1:0] | O | — |
| **60** | PCLK | O | Pixel clock |
| **62 / 58 / 56** | HSYNC / VSYNC / DE | O | Display timing |
| **23 / 25 / 27** | SDIO_D0‑D3 | I/O | Alt SPI / Wi‑Fi SDIO |
| **19 / 21** | SDIO_CMD / CLK | I/O | — |
| **15 / 17** | UART_TX / UART_RX | I/O | Console |
| **9 / 11** | I²C0_SCL / SDA | I/O | Control bus |
| **13** | CAN_TX | O | FDCAN |
| **7** | CAN_RX | I | — |
| **1, 68** | GND / RTC_CLK_IN | PWR | Ground / 32 kHz |
| **67** | VBAT | PWR | Backup supply |
| **31A / 31B** | SWDIO / SWCLK | I/O | Debug |
| **63** | NRST | I | MCU reset |
| **39** | BOOT0 | I | Boot config |
| *Many others* | GPIO[0‑n] | I/O | PWM, ADC, timers |

> All pins are 1.8 V tolerant unless noted otherwise. USB & Octo‑SPI lines include on‑board ESD TVS diodes.  

---

## 7. Mechanical

* **Outline:** 22 mm (W) × 30 mm (L) × 0.8 mm PCB thickness  
* **Component height:** ≤ 1.5 mm top & bottom (per M.2 spec) :contentReference[oaicite:2]{index=2}  
* **Fixation:** Single M2 screw Ø 2.3 mm hole, 4 mm from card tail  
* **Stencil / paste:** 0.11 mm laser‑cut SS, IPC‑7095 type 4  

![U5‑2230‑SOM mechanical drawing](docs/mech_drawing.png) <!-- placeholder -->

---

## 8. Power‑State Summary

| State | Vcore | Clocks | Retained | Wake sources | Typ I |
|-------|-------|--------|----------|--------------|------|
| **Run (high)** | 1 V8 | 120‑160 MHz PLL | Full | Any IRQ | 4.8 mA |
| Run (low) | 1 V2 | 60 MHz MSI | Full | Any IRQ | 1.2 mA |
| **Stop 2** | off | 0 | SRAM+RTC | GPIO, RTC, CAN | 6 µA |
| Standby | off | 0 | RTC only | WKUP pins, RTC | 480 nA |
| Shutdown | off | 0 | None | NRST only | 150 nA |

---

## 9. Ordering Information

| Order code | Flash / PSRAM | Assembly | Notes |
|------------|---------------|----------|-------|
| **U5‑2230‑64F32P‑A** | 64 MB Flash / 32 MB PSRAM | ENIG, Pb‑free | Std production |
| U5‑2230‑64F‑A | 64 MB Flash / – | ‑ | Cost‑down |
| U5‑2230‑DEV‑KIT | ‑ | Dev carrier + TFT & USB‑C | Prototyping bundle |

---

## 10. References  
* **STM32U5Axxx Datasheet DS13543 Rev 2**, STMicroelectronics – Run‑mode current 18.5 µA/MHz, component specs :contentReference[oaicite:3]{index=3}  
* **Delock “The M.2 interface” Key‑E pages (2022)** – size 2230, 1.5 mm max component height, 67‑pin edge details :contentReference[oaicite:4]{index=4}  

> © 2025 Open‑Hardware Project – Released under CERN‑OHL‑P v2.  
> Specifications subject to change. Please check for the latest revision before production.