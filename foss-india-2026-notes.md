# FOSS India 2026 Notes

## gooey.ai
- Mentioned in chat — need to capture context/details when provided

## pling! — github.com/b-init/pling
- Wireless low-profile split keyboard (54 keys, 3-key thumb cluster)
- Gateron KS27 low-profile switches
- Xiao BLE (nrf52840) + ZMK firmware
- Flippable PCB, no hotswap, no headers — "set it and forget it"
- Acrylic + 3D printed case, 250mAh batteries
- KiCad sources + gerbers in `/pcb`
- Firmware config: github.com/b-init/zmk-config-pling
- License: CERN-OHL-W-2.0 (hardware), created May 2026
- Author: b-init (likely Indian maker given FOSS India context)

## solstone-journal — github.com/solpbc/solstone-journal
- Personal memory platform / local-first journal for AI agents
- "A memory your agents can work from. On your device, owned by you."
- Ingests audio → speaker-attributed transcripts (Parakeet), screen frames → descriptions
- Surfaces people, companies, projects, tools, meetings, commitments automatically
- Knowledge graph that builds itself; facets for project/context grouping
- Local folder structure: `chronicle/YYYYMMDD/`, `entities/<id>/`
- Integrates with Claude Code, Codex, Gemini CLI via `journal` skill
- Architecture: Rust crates (`solstone-core-*`), supervisor + services, SQLite FTS index
- License: AGPL-3.0-only, by sol pbc (solpbc.org)
- 12k+ commits, active since May 2025
- No telemetry/analytics; signed releases (minisign)
- Part of solstone family: macOS, Windows, Linux apps in separate repos

## OPANqr — github.com/serv0id/OPANqr
- PAN Card QR Code Reader (Python) — decodes "Enhanced 2.0 Secure QR Codes" on PAN/e-PAN cards
- Reverse-engineered from Android app (com.pv.scr.pancardreader) — no public spec exists
- Usage: `pip install -r requirements.txt`, then decode via `--string` or `--file`
- Optional `--verify` flag to verify QR signature using public key
- Blog post: desrever.dev/posts/opanqr/
- Author: serv0id (Indian developer, blog at desrever.dev)

## Shreyas Minocha — shreyasminocha.me
- 2nd-year PhD at Georgia Tech (School of Cybersecurity and Privacy), SPDR lab with Dr. Mike Specter
- Research: age verification systems, digital identity
- Publication: "Papers, Please: A First Look at Age Verification on the Web" (IEEE S&P 2026)
- Projects: gyan85 (Yan85 emulator/disassembler for pwn.college), yfs-fuse (FUSE adapter for COMP 421 filesystem)
- Interests: speedcubing (WCA), CTFs, chess, languages, coin collecting, open contributions (Wikipedia, OpenStreetMap, MusicBrainz, Archive.org, OpenLibrary)
- Site: shreyasminocha.me / shr.cx — content CC BY-SA 4.0

## SFLC.in — Software Freedom Law Center, India (sflc.in)
- Founded 2010, Delhi-based donor-supported legal services org
- Mission: defend digital freedoms, promote FOSS, privacy, free speech, innovation, equality
- Special Consultative Status with UN ECOSOC
- Registered society under Societies Registration Act, 1860
- Team: lawyers, policy analysts, technologists, students (~33 staff)
- Key initiatives:
  - **Digital Defenders Network (DDN)** — pan-India lawyer community for digital rights
  - **Internet Shutdowns Tracker** — documents state-imposed internet bans
  - **Free Speech Tracker** — crowd-sourced tracking of free speech violations/laws
  - **Pro-bono legal aid** for FOSS developers
  - **Policy engagement** — informed tech law decisions
- India FOSS 2026 partner/organizer
- Resources for protestors (offline comms, legal help, know-your-rights)
- Contact: +91-11-43587126, mail@sflc.in, press@sflc.in
- K-9, 2nd Floor, Birbal Road, Jangpura Extension, New Delhi 110014