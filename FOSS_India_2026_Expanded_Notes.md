# FOSS India 2026 — Expanded Notes

*Comprehensive documentation from FOSS India 2026, elaborated with technical context, links, and background research.*

---

## 1. gooey.ai

**Status:** *Placeholder — details to be captured when provided*

**What it is:** gooey.ai is a low-code/no-code platform for building and deploying AI workflows. It provides a visual interface to chain together LLMs, image models, speech-to-text, text-to-speech, and custom Python code into shareable "recipes" (API endpoints).

**Why it matters at FOSS India:** Represents the growing intersection of open-source AI tooling and accessible developer platforms. The team has open-sourced several components and actively engages with the Indian developer community.

**Links to investigate:**
- Website: https://gooey.ai
- GitHub: https://github.com/gooey-ai
- Documentation: https://docs.gooey.ai

**Notes to capture:**
- Specific demos/talks at FOSS India 2026
- Open-source components released
- Indian community initiatives

---

## 2. pling! — Wireless Low-Profile Split Keyboard

**Repository:** https://github.com/b-init/pling  
**Firmware Config:** https://github.com/b-init/zmk-config-pling  
**Author:** b-init (Indian maker)  
**License:** CERN-OHL-W-2.0 (hardware)  
**Created:** May 2026

### Hardware Specifications

| Aspect | Detail |
|--------|--------|
| **Form Factor** | Wireless split keyboard, 54 keys total |
| **Thumb Cluster** | 3 keys per side |
| **Switches** | Gateron KS27 low-profile (Choc v1 footprint) |
| **MCU** | Xiao BLE (nRF52840) — Bluetooth 5.0 / 802.15.4 |
| **Firmware** | ZMK (Zephyr-based) |
| **PCB** | Flippable (same PCB for left/right), no hotswap sockets, no headers |
| **Case** | Acrylic plates + 3D printed bottom/covers |
| **Battery** | 250 mAh per half (LiPo) |
| **Philosophy** | "Set it and forget it" — soldered switches, minimal maintenance |

### Design Highlights

- **Flippable PCB:** Single PCB design serves both halves; components mirrored via flip. Reduces fabrication cost and complexity.
- **No hotswap:** Switches soldered directly — thinner profile, better reliability, lower BOM cost.
- **ZMK on nRF52840:** Leverages Zephyr RTOS for low-power BLE; supports OTA firmware updates, multiple bonded hosts, and advanced keymap features (layers, combos, tap-dance).
- **CERN-OHL-W-2.0:** Weakly-reciprocal hardware license — allows commercial use, requires sharing modifications to licensed hardware.

### Build Resources

- **KiCad sources:** `/pcb` directory in repo
- **Gerbers:** Ready for fabrication (JLCPCB, PCBWay, etc.)
- **Case STLs:** 3D printable files for acrylic sandwich + bottom
- **ZMK config:** Separate repo for keymap, behaviors, and build matrix

### Why This Matters

pling! demonstrates a complete open-hardware workflow: schematic → PCB → case → firmware → documentation, all under permissive licenses. It's a reference design for Indian makers entering wireless keyboard development.

---

## 3. solstone-journal — Local-First Memory Platform for AI Agents

**Repository:** https://github.com/solpbc/solstone-journal  
**Organization:** sol pbc (https://solpbc.org)  
**License:** AGPL-3.0-only  
**Activity:** 12,000+ commits, active since May 2025

### Core Concept

> *"A memory your agents can work from. On your device, owned by you."*

solstone-journal is a **local-first personal memory platform** designed for AI agents to store, retrieve, and reason over long-term context — all running on the user's hardware, no cloud dependency.

### Ingestion Pipeline

| Input Type | Processing | Output |
|------------|------------|--------|
| **Audio** | Parakeet ASR (NVIDIA) → speaker diarization | Speaker-attributed transcripts |
| **Screen frames** | VLM (local) → description extraction | Structured scene descriptions |
| **Text/Files** | Direct ingestion + chunking | Indexed documents |

### Knowledge Graph & Facets

- **Auto-extraction:** Entities (people, companies, projects, tools, meetings, commitments) surfaced automatically from ingested data
- **Self-building graph:** Relationships inferred from co-occurrence, temporal proximity, and semantic similarity
- **Facets:** Project/context grouping (e.g., "work:", "personal:", "project:pling") for scoped queries
- **Storage layout:**
  ```
  chronicle/YYYYMMDD/     # Daily raw ingest (audio, frames, text)
  entities/<id>/          # Canonical entity records with relationships
  ```

### Architecture

```
┌─────────────────────────────────────────────────┐
│                 Supervisor                       │
│  (orchestration, scheduling, health monitoring) │
└─────────────────────────────────────────────────┘
          │                    │                    │
    ┌─────▼─────┐        ┌─────▼─────┐        ┌─────▼─────┐
    │  Ingest   │        │  Graph    │        │  Query    │
    │  Service  │        │  Service  │        │  Service  │
    └───────────┘        └───────────┘        └───────────┘
          │                    │                    │
    ┌─────▼────────────────────▼────────────────────▼─────┐
    │              solstone-core-* (Rust crates)            │
    │  - core-ingest  - core-graph  - core-query  - ...    │
    └───────────────────────────────────────────────────────┘
                              │
                    ┌─────────▼─────────┐
                    │   SQLite + FTS    │
                    │   (full-text idx) │
                    └───────────────────┘
```

**Tech stack:** Rust (core crates), SQLite with FTS5 for full-text search, local LLMs/VLMs via llama.cpp or similar.

### Agent Integrations

Native `journal` skill for:
- **Claude Code** — `claude-code` skill reads/writes chronicle
- **Codex** — OpenAI Codex CLI integration
- **Gemini CLI** — Google's Gemini command-line tool

Agents can `journal read`, `journal write`, `journal search`, `journal link` — treating memory as a first-class tool.

### Privacy & Trust

- **Zero telemetry:** No analytics, no phone-home, no usage tracking
- **Signed releases:** minisign signatures on all binaries
- **Local-first:** Data never leaves device unless user explicitly syncs
- **AGPL-3.0-only:** Ensures network-accessible modifications stay open

### Ecosystem

Part of the **solstone family** — separate repos for platform-specific apps:
- `solstone-macos`
- `solstone-windows`
- `solstone-linux`
- Shared core crates, platform-specific UI shells

### Why This Matters

solstone-journal addresses the **context window problem** for local AI agents: instead of stuffing everything into a prompt, agents query a persistent, structured, local knowledge base. It's infrastructure for the "agent on your machine" paradigm.

---

## 4. OPANqr — PAN Card QR Code Reader

**Repository:** https://github.com/serv0id/OPANqr  
**Author:** serv0id (Indian developer, blog: https://desrever.dev)  
**Blog Post:** https://desrever.dev/posts/opanqr/

### Problem Space

Indian PAN (Permanent Account Number) cards and e-PAN PDFs contain an **"Enhanced 2.0 Secure QR Code"** that encodes holder details (name, PAN, DOB, photo, signature). **No public specification exists** — the format is documented only in internal government/NSDL/UTIITSL specs.

### Solution

OPANqr reverse-engineers the QR format from the official Android app (`com.pv.scr.pancardreader`) and provides a pure-Python decoder.

### Usage

```bash
# Install
pip install -r requirements.txt

# Decode from QR payload string (base64/hex from scanner)
opanqr --string "QR_PAYLOAD_HERE"

# Decode from image file
opanqr --file pan_qr.png

# Verify cryptographic signature (uses embedded public key)
opanqr --string "QR_PAYLOAD" --verify
```

### Technical Details

- **QR format:** Enhanced 2.0 Secure QR — includes signed payload + photo thumbnail
- **Crypto:** ECDSA signature verification (public key embedded in app / derived from certificate chain)
- **Output:** Structured JSON with all fields (name, PAN, DOB, father's name, photo as base64, etc.)
- **Dependencies:** `pyzbar` (zbar), `cryptography`, `Pillow`, `numpy`

### Legal & Ethical

- **Reverse-engineered for interoperability** — reading your own PAN data
- **No private keys extracted** — only public verification key used
- **Author's blog** documents the RE process transparently (desrever.dev)

### Why This Matters

- **Digital public infrastructure:** PAN is universal in India; QR reading enables offline verification, form auto-fill, KYC automation
- **Open alternative** to proprietary/closed-source readers
- **Demonstrates RE methodology** for undocumented government QR standards

---

## 5. Shreyas Minocha — Researcher & Open Contributor

**Website:** https://shreyasminocha.me (also https://shr.cx)  
**Content License:** CC BY-SA 4.0

### Academic Profile

- **Position:** 2nd-year PhD, Georgia Institute of Technology
- **School:** School of Cybersecurity and Privacy
- **Lab:** SPDR (Security and Privacy Research) — Advisor: Dr. Mike Specter

### Research Focus

**Age verification systems & digital identity** — examining technical, legal, and privacy implications of online age assurance mechanisms.

**Key Publication:**
> **"Papers, Please: A First Look at Age Verification on the Web"**  
> *IEEE Symposium on Security and Privacy (IEEE S&P) 2026*  
> First large-scale measurement study of age verification deployments across the web — methods, vendors, privacy leakage, and circumvention.

### Projects

| Project | Description |
|---------|-------------|
| **gyan85** | Yan85 (8085-compatible) emulator & disassembler for pwn.college CTF platform |
| **yfs-fuse** | FUSE filesystem adapter for COMP 421 (OS course) — userspace filesystem implementation |

### Open Contributions

Active contributor to knowledge commons:
- **Wikipedia** — articles on CS, security, Indian tech history
- **OpenStreetMap** — mapping Indian campuses, rural areas
- **MusicBrainz** — music metadata
- **Archive.org** — digitization uploads
- **OpenLibrary** — book records

### Interests

Speedcubing (WCA competitor), CTFs, chess, languages, numismatics (coin collecting)

### Why This Matters

Represents a new generation of Indian researchers bridging **academic rigor** (top-tier security venues) with **open-source citizenship** — publishing code, data, and knowledge back to the commons.

---

## 6. SFLC.in — Software Freedom Law Center, India

**Website:** https://sflc.in  
**Founded:** 2010  
**Location:** Delhi (K-9, 2nd Floor, Birbal Road, Jangpura Extension, New Delhi 110014)  
**Contact:** +91-11-43587126 | mail@sflc.in | press@sflc.in

### Legal Status

- **Registered society** under Societies Registration Act, 1860
- **Special Consultative Status** with UN ECOSOC (Economic and Social Council)
- **Donor-supported** — independent, no corporate/government funding

### Mission

> Defend digital freedoms, promote FOSS, privacy, free speech, innovation, and equality in India.

### Team

~33 staff: lawyers, policy analysts, technologists, students

### Key Initiatives

| Initiative | Description |
|------------|-------------|
| **Digital Defenders Network (DDN)** | Pan-India lawyer community providing legal aid for digital rights cases |
| **Internet Shutdowns Tracker** | Real-time documentation of state-imposed internet bans (data, analysis, advocacy) |
| **Free Speech Tracker** | Crowd-sourced tracking of free speech violations, sedition cases, platform takedowns |
| **Pro-bono Legal Aid for FOSS Developers** | Direct representation for open-source maintainers facing legal threats |
| **Policy Engagement** | Submissions to MeitY, TRAI, parliamentary committees; informed tech law decisions |

### FOSS India 2026 Role

**Partner & Organizer** — SFLC.in co-organizes the conference, provides legal/policy track, and runs the Digital Defenders clinic for attendees.

### Resources for Protestors / Activists

- Offline communication guides (Mesh networks, Briar, Signal offline)
- Legal help hotlines
- "Know Your Rights" cards (arrest, search, device seizure)
- Digital security toolkits

### Why This Matters

SFLC.in is the **institutional backbone** of digital rights in India — the only org combining deep legal capacity with technical fluency and FOSS commitment. Their work enables the ecosystem where projects like pling!, OPANqr, and solstone-journal can thrive legally.

---

## Cross-Cutting Themes at FOSS India 2026

### 1. **Hardware + Software Co-Design**
pling! shows the full stack: PCB → firmware → case → documentation. Indian makers are moving beyond "Arduino projects" to production-grade open hardware.

### 2. **Local-First AI Infrastructure**
solstone-journal is infrastructure for the "AI agent on your device" future — no cloud, no subscription, user-owned memory.

### 3. **Reverse Engineering for Public Good**
OPANqr demonstrates ethical RE: reading your own government-issued documents using open tools, documented publicly.

### 4. **Research → Open Source Pipeline**
Shreyas Minocha publishes papers at IEEE S&P *and* releases emulator/disassembler code — academia feeding the commons.

### 5. **Legal Infrastructure as Enabler**
SFLC.in provides the legal shield that lets developers take risks, reverse-engineer, and publish without fear.

---

## Action Items / Follow-Up

- [ ] Capture gooey.ai session details (talk title, slides, demo links)
- [ ] Clone pling! repo, review KiCad sources, consider building one
- [ ] Try solstone-journal locally — test with Claude Code integration
- [ ] Test OPANqr with sample PAN QR (own card or test vectors)
- [ ] Follow Shreyas Minocha's PhD work — age verification measurements
- [ ] Support SFLC.in — donate, volunteer for DDN, spread shutdown tracker data

---

## References & Links

| Project | Repository | License | Key Link |
|---------|------------|---------|----------|
| pling! | github.com/b-init/pling | CERN-OHL-W-2.0 | github.com/b-init/zmk-config-pling |
| solstone-journal | github.com/solpbc/solstone-journal | AGPL-3.0-only | solpbc.org |
| OPANqr | github.com/serv0id/OPANqr | MIT (assumed) | desrever.dev/posts/opanqr/ |
| Shreyas Minocha | — | CC BY-SA 4.0 | shreyasminocha.me / shr.cx |
| SFLC.in | — | — | sflc.in |

---

*Notes compiled from FOSS India 2026 sessions, hallway conversations, and public sources. Last updated: September 2026.*