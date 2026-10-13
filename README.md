# atakhrf1

<img width="1192" height="1068" alt="layout-5a" src="https://github.com/user-attachments/assets/168db6cb-6c5a-40ed-a7e9-d2dbb759ec0d" />
<img width="1776" height="1068" alt="layout-6" src="https://github.com/user-attachments/assets/48665e72-7286-4c11-b1eb-50f3b1851245" />


**ATAK plugin that turns a HackRF One plugged into your Android phone or tablet into a portable spectrum analyzer, drone/RF detection tool and RSSI direction finder, reporting to the ATAK map via Cursor-on-Target (CoT).**

*Português: [README.pt-BR.md](README.pt-BR.md)*

> Independent community project. Not affiliated with or endorsed by the TAK Product Center, Great Scott Gadgets or any vendor.
> Receive-only. You are responsible for complying with the radio and privacy laws of your country.

## Download

Get the signed plugin from **[Releases](../../releases/latest)**: `ATAK-Plugin-atakhrf1-<version>-...-civ-release.apk`.
It is signed by the TAK.gov Third Party Pipeline, so it loads in the **Play Store ATAK-CIV 5.6**.

1. Install the APK on the Android device (`adb install -r <file>.apk`, or open it on the device).
2. Open ATAK, accept the plugin load prompt, then open **atakhrf1** from the toolbar.
3. Plug in the HackRF One (USB-C/OTG) and grant USB permission.

> If you previously installed a locally built (debug) version, uninstall it first: the signature is different.

## What it does

The panel has four tabs: **Scan | Hunt | AI | Catalog**. Works on tablets and phones.

### Scan
- Live spectrum and waterfall, adjustable threshold, HackRF detected and operated entirely from the plugin.
- Four interest categories, each showing only compatible tools: **Drones, Cellular, Two-way radios, ISM**.
- Band presets per category with analysis profiles: cellular (uplink/downlink aware, operator by band), radio channel plans (FRS/GMRS, PMR446, UHF/VHF, marine, aeronautical), Wi-Fi 2.4 GHz, FPV 5.8 GHz, generic ISM.
- Modes: **band analysis**, **free spectrum** (generic peaks), **general drone scan** (7 bands) and **burst scan** (narrow windows, DroneID burst timing).
- Drone signature database (44 sourced entries) and FPV channel matching from 433 MHz to 5.8 GHz, including 900 MHz to 1.3 GHz analog FPV and long-range control links.
- Detections stay highlighted on the spectrum with age-based colors, and drone-scan alerts are retained in a banner until cleared.
- **Listen**: FM/AM demodulation with squelch and auto-listen.
- **Inspect**: 1 MHz window (about 1 kHz resolution) with spectrum and waterfall, using a dedicated I/Q receiver.
- **Record I/Q**: 5 seconds at 2 Msps to `.cs8` + `.json` (frequency, gains, position, time), with a configurable storage limit. Never deletes on its own.

### Hunt
- RSSI-based direction finding of fixed-frequency drone links (Wi-Fi 2.4 GHz, analog FPV 5.8 GHz): rotate a directional antenna with the compass, or walk with GPS.
- Live map output in ATAK: measurement trail, bearing line, estimated source and uncertainty circle. The line shows direction only; the circle is uncertainty, not a guarantee.

### AI (optional, online only)
- Second opinion from an LLM on peaks and candidates. Offline, the plugin runs normally and never waits on it.
- Anthropic and any OpenAI-compatible endpoint (OpenRouter, Ollama, Gemini compatible endpoint...). **Test AI** button included.
- Honest verdicts: Likely (70%+), Possible (40-69%), Inconclusive (<40%), Unknown. The most cautious level wins. It never identifies a person or a transmitter.

### Catalog
- Persistent frequency catalog (Observations, Captures, Alerts) with filters and CSV export.
- Send an entry to the map as CoT. The position is where the signal was received strongest, **not** the source position, and the marker text says so.
- **Clear** removes the plugin's markers directly from the ATAK map.

### Map and diagnostics
- CoT with stable UIDs (`a-u-A` for drone candidates, `a-u-G` otherwise). No GPS fix means no position is published.
- Periodic diagnostic snapshots (battery, memory, thermal state, running mode).
- Releases are cumulative: a regression test fails if a function from an earlier version becomes unreachable.

## Limitations
- Detection is energy-based triage. It does not identify drone model or serial number (that is Remote ID's job).
- One HackRF serves one application at a time.
- The AI API key is stored in plain text in the plugin's preferences on the device. Use a free-tier or restricted key.
- Unexplained device reboots have been observed on a Galaxy Tab A7 Lite during scans; the cause is not confirmed and diagnostics are built in to help investigate.
- Hunting only works on fixed-frequency links; frequency-hopping links (OcuSync, ELRS) are not supported.

## Requirements
- ATAK-CIV 5.6 on Android, HackRF One, USB OTG.

## Support the project

If atakhrf1 is useful to you, you can support its development with a Pix donation (Brazil):

[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-donate-FFDD00?logo=buymeacoffee&logoColor=black)](https://buymeacoffee.com/tiagoufbao)

**Pix key (email):** `tiagoufba@gmail.com`

## Terms of use
The plugin is distributed free of charge, as a binary only. The source code is not published. You may use it, but you may not redistribute, modify or resell it without permission. Provided "as is", without warranty. ATAK and its SDK are subject to their own terms.

## Third-party software
The plugin includes **libusb** (LGPL-2.1, https://github.com/libusb/libusb) and **libhackrf** (BSD-3-Clause, https://github.com/greatscottgadgets/hackrf). Their source code is available at those links.
