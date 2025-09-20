# 🔊AY-ZONIC-Core

AY-ZONIC-Core is a modular PSG interface designed for the ZX81, supporting both ZON-X and ZON-X-81 compatibility via simplified A4-only decode logic. Rev2.0 introduces gate economy, contributor-friendly schematic clarity, and expansion-ready I/O via AY-3-8912 Port A.

> **This project continues from [JonZON-X](https://github.com/Bambleweeny57/JonZON-X), which was closed at Rev1.4** after timing issues were discovered in demo playback. AY-ZONIC-Core retains the same A4-based decode logic but drops A5 and A6 simplifying the design to single PSG support and saving a gate.

## 🔧 Features

- **Dual-mode decode logic** via DIP switch:
  - **DIP OFF** → A4 pulled high → ZON-X-81 mode
  - **DIP ON** → A4 sourced from ZX81 Expansion Bus → ZON-X mode
- **AY-3-8912 PSG integration** with clean register selection and audio output
- **Series resistors** on data bus for signal protection
- **Pull-ups** from ZX81 Expansion Bus to PSG for stable logic levels
- **Port A expansion header** with +5V and GND for SD card and I/O experimentation
- **/RD decode support** for future peripheral interaction and PSG reads

## 🧠 Decode Logic Overview

The schematic uses simplified A4-only address decoding, inherited from JonZON-X Rev1.4. By removing A5 and A6 from the decode path, Rev2.0 drops multi-PSG support in favor of gate economy and contributor clarity.

You can view the decode logic diagram [here](https://github.com/Bambleweeny57/AY-ZONIC-Core/blob/main/images/decode_logic.png).

### DIP Switch Logic — A4 Routing Modes

| DIP Switch | A4 Source             | Mode         | Description                                      |
|------------|-----------------------|--------------|--------------------------------------------------|
| OFF        | Pulled high (via pull-up) | ZON-X-81     | Forces A4 = 1 for simplified decode              |
| ON         | From ZX81 Expansion Bus  | ZON-X        | Enables dynamic A4 control from host             |

> This DIP-controlled logic allows seamless switching between ZON-X and ZON-X-81 compatibility without modifying the schematic.

### Decode Logic Explanation

The PSG is selected when:
- **A4 = 1** (via DIP or bus)
- **A7 = 1** (to avoid bus conflicts)
- **A2 = 1** (used internally by the PSG)
- **/IOREQ = 0** (active I/O cycle)
- **/WR and /RD** combinations determine the operation:
  - `/WR = 1`, `/RD = 1` → Write to register
  - `/WR = 0`, `/RD = 1` → Write to PSG
  - `/WR = 0`, `/RD = 0` → Read from PSG

> `/RD` is now decoded explicitly to support read operations from the PSG and future SD card and I/O interfaces.

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
- **8 digital I/O lines** (AIO0–AIO7)
- **+5V** and **GND** for powering peripherals

This enables SD card interfacing, experimental I/O modules, and future expansion without modifying the core schematic.

### Expansion Header Pinout

| Pin | Signal | Description               |
|-----|--------|---------------------------|
| 1   | AIO0   | Port A bit 0              |
| 2   | AIO1   | Port A bit 1              |
| 3   | AIO2   | Port A bit 2              |
| 4   | AIO3   | Port A bit 3              |
| 5   | AIO4   | Port A bit 4              |
| 6   | AIO5   | Port A bit 5              |
| 7   | AIO6   | Port A bit 6              |
| 8   | AIO7   | Port A bit 7              |
| 9   | +5V    | Power supply for expansion|
| 10  | GND    | Ground                    |

> This header is ideal for SD card experiments, LED arrays, or future playback logic modules. All signals are directly mapped from the AY-3-8912 Port A.

---

## 🗂️ Repository Structure

- `pdf/ay-zonic-core.pdf` — Rev2.0 schematic (KiCad source available on request)
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
