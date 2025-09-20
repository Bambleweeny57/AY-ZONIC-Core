# AY-ZONIC-CORE Rev2.0

AY-ZONIC-CORE is a modular PSG interface designed for the ZX81, supporting both ZON-X and ZON-X-81 compatibility via simplified A4-only decode logic. Rev2.0 introduces gate economy, contributor-friendly schematic clarity, and expansion-ready I/O via AY-3-8912 Port A.

> **This project continues from [JonZON-X](https://github.com/Bambleweeny57/JonZON-X), which was closed at Rev1.4** after timing issues were discovered in demo playback. AY-ZONIC-CORE retains the same A4-based decode logic but drops A5 and A6, simplifying the design to single PSG support and saving a gate.

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

The schematic uses simplified A4-only address decoding, inherited from JonZON-X Rev1.4. By removing A5 and A6 from the decode path, Rev2.0 drops multi-PSG support in favor of gate economy and contributor clarity.

You can view the decode logic diagram [here](https://github.com/Bambleweeny57/AY-ZONIC-Core/blob/main/images/decode_logic.png).

### Legacy Reference — JonZON-X Rev1.4 Decode Matrix (A5/A6 omitted)

| A0–A4 | A2 | A7 | /IOREQ | /WR | /RD | BDIR | BC1 | Operation             |
|-------|----|----|--------|-----|-----|------|-----|------------------------|
| —     | 1  | 1  | 0      | 1   | 1   | 1    | 1   | Write to register      |
| —     | 1  | 1  | 0      | 0   | 1   | 0    | 1   | Write to PSG           |
| —     | 1  | 1  | 1      | 0   | 0   | 1    | 0   | Read from PSG          |
| —     | —  | —  | —      | —   | —   | 0    | 0   | Inactive               |

> Rev2.0 removes A5 and A6, streamlining the logic and focusing on single PSG support.

---

## 🔌 Expansion Header (Port A)

Port A of the AY-3-8912 exposes:
- **+5V**
- **GND**
- **User I/O lines** for experimentation

This enables SD card interfacing and other peripheral hacks without modifying the core schematic.

## 🗂️ Repository Structure

- `ay-zonic-core.pdf` — Rev2.0 schematic (KiCad source available on request)
- `README.md` — This file
- `images/` — Decode logic diagram and overlays
- `docs/` — Contributor notes and onboarding diagrams (coming soon)

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
