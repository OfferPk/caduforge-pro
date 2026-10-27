# CADUForge Pro (v1.0.0)

### CCSDS 131.0-B-4 & ISO 22641 TM Synchronization & Channel Access Data Unit (CADU) Studio

CADUForge Pro is an aerospace-grade developer studio, Channel Access Data Unit (CADU) synthesizer, 32-bit Attached Synchronization Marker (ASM) correlator, CCSDS LFSR Pseudo-Randomizer, Reed-Solomon (255, 223\) codec, and 10-point normative compliance auditor designed for spacecraft flight software teams, ground station engineers (NASA DSN, ESA ESTRACK, KSAT, MBRSC UAE), and commercial mission operators (Artemis lunar landers, Earth-observation CubeSats, Mars exploration orbiters).

---

## 🌟 Key Capabilities

- **Normative CADU Synthesis (CCSDS 131.0-B-4)**: Assembles synchronous Channel Access Data Units combining the 32-bit Attached Sync Marker (`0x1ACFFC1D`) with scrambled telemetry transfer frames (TM, AOS, or USLP).  
- **CCSDS LFSR Pseudo-Randomizer**: Implements generator polynomial \$h(x) \= x^8 \+ x^7 \+ x^5 \+ x^3 \+ 1\$ with frame-boundary state resets (`0xFF`), generating the standard sequence (`0xFF480EC0...`) to guarantee high symbol transition density (\$\\ge 35%\$) and eliminate discrete RF spectral peaks.  
- **ASM Correlation State Machine**: Features a multi-threshold Hamming distance correlator simulating ground station telemetry receiver synchronization across Search, Check, Lock, and Flywheel tracking states.  
- **Reed-Solomon (255, 223\) Error Correction**: Computes 32-octet parity using Galois Field \$\\text{GF}(2^8)\$ arithmetic (\$p(x) \= x^8 \+ x^7 \+ x^2 \+ x \+ 1 \= \\text{0x187}\$) with interleaving depth support (\$I \= 1..8\$) for burst error protection.  
- **Symbol Transition Density Analyzer**: Analyzes transition percentages, consecutive identical bit run-lengths, and DC balance between raw and scrambled telemetry streams.  
- **10-Point Normative Compliance Auditor**: Automated verification engine enforcing rules `CADU-001` through `CADU-010`.

---

## 📂 Project Structure

cadu-forge-pro/

├── source-code/

│   ├── cadu-engine.js           \# Core ASM correlator, LFSR scrambler & CADU assembler

│   ├── cadu-auditor.js          \# 10-point normative compliance auditor

│   ├── cadu\_cli.py              \# Pure Python 3 CLI executable

│   ├── cadu-cli.py              \# Pure Python 3 CLI alias

│   ├── test\_runner.py          \# 10-suite unit test runner

│   └── index.html               \# Interactive Mission Control operations console

├── build/

│   └── cadu-forge-pro-v1.0.0.zip \# Standalone production bundle

├── documentation/

│   ├── CCSDS\_CADU\_SPECIFICATION.md \# Normative protocol specification

│   └── CADU\_COMPLIANCE\_MATRIX.md   \# 10-point requirement traceability

└── screenshots/

    ├── architecture-diagram.svg  \# System architecture diagram

    └── cadu-studio-preview.svg    \# Operations console preview

---

## 🚀 Quick Start

### Running Automated Tests

python3 source-code/test\_runner.py \-v

### Command Line Interface

\# Synthesize standard CADU from telemetry frame payload

python3 source-code/cadu\_cli.py \--mode cadu \--payload "TM\_FRAME\_SCID=0x0042;SCIENCE\_DATA"

\# Decode a raw hex CADU and recover telemetry frame

python3 source-code/cadu\_cli.py \--mode decode \--payload "TM\_TELEMETRY"

\# Compare symbol transition density between raw and scrambled streams

python3 source-code/cadu\_cli.py \--mode density \--payload "00000000000000000000"

\# Run 10-Point Normative Compliance Audit on synthesized CADU

python3 source-code/cadu\_cli.py \--mode audit \--payload "ORBITAL\_TELEMETRY\_BURN\_DATA"

### Launching the Web Operations Console

Open `source-code/index.html` in any web browser to access the interactive Mission Control dashboard, visual CADU builder, ASM correlator, transition density analyzer, and 10-point compliance scorecard.