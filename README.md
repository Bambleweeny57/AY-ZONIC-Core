# AY-ZONIC-CORE Rev2.0

AY-ZONIC-CORE is a modular PSG interface designed for the ZX81, supporting both ZON-X and ZON-X-81 compatibility via simplified A4-only decode logic. Rev2.0 introduces gate economy, contributor-friendly schematic clarity, and expansion-ready I/O via AY-3-8912 Port A.

> **This project continues from [JonZON-X](https://github.com/Bambleweeny57/JonZON-X), which was closed at Rev1.4** after timing issues were discovered in demo playback. AY-ZONIC-CORE pivots to the AY-3-8912 for improved register selection and platform stability.

## 🔧 Features

- **Dual-mode decode logic** via DIP switch:
  - **DIP OFF** → A4 pulled high → ZON-X-81 mode
  - **DIP ON** → A4 sourced from ZX81 Expansion Bus → ZON-X mode
- **AY-3-8912 PSG integration** with clean register selection and audio output
- **Series resistors** on data bus for signal protection
- **Pull-ups** from ZX81 Expansion Bus to PSG for stable logic levels
- **Port A expansion header** with +5V and GND for SD card experimentation
- **/RD decode support** for future peripheral interaction

## 🧠 Decode Logic Overview

The schematic uses A4-only address decoding to simplify logic and reduce gate count. A DIP switch selects between fixed A4 (ZON-X-81) and dynamic A4 from the ZX81 bus (ZON-X), allowing flexible compatibility without schematic duplication.

```text
+-------------------------+
| DIP Switch              |
|                         |
| OFF → A4 = High         |
| ON  → A4 from ZX81 Bus  |
+-------------------------+
```

## 🔌 Expansion Header (Port A)

Port A of the AY-3-8912 exposes:
- **+5V**
- **GND**
- **User I/O lines** for experimentation

This enables SD card interfacing and other peripheral hacks without modifying the core schematic.

## 🗂️ Repository Structure

- `ay-zonic-core.pdf` — Rev2.0 schematic (KiCad source available on request)
- `README.md` — This file
- `docs/` — Contributor notes, overlays, and onboarding diagrams (coming soon)

## 🧭 Contributor Notes

- Keep DIP switch logic annotated in overlays
- Label Port A lines clearly for expansion use
- Use series resistors and pull-ups as shown for safe bus interaction
- Future revisions may include playback logic or UI hooks — modularity is key

## 🛠️ Status

✅ Rev2.0 schematic complete  
🧪 Expansion header tested with SD interface  
📚 Documentation in progress

---

For questions, forks, or onboarding help, feel free to open an issue or start a discussion. Let the AY-3-8912 sing!

