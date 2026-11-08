# Euclid-5 // Multi-Voice Euclidean Drum Sequencer

> **An interactive, zero-dependency 5-voice generative drum sequencer powered by Bjorklund's algorithm, native Web Audio API programmatic synthesis, and dual linear/polar radar visualizations.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-2ed573?style=for-the-badge&logo=github)](https://longman694.github.io/drumbeats/)
[![Web Audio API](https://img.shields.io/badge/Audio-Web%20Audio%20API-1e90ff?style=for-the-badge)](https://www.w3.org/TR/webaudio/)
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero%20(Pure%20Vanilla%20JS)-ffa502?style=for-the-badge)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-a55eea?style=for-the-badge)](#)

---

### 🌐 Live Demo
Experience the synthesizer directly in your browser:
**[https://longman694.github.io/drumbeats/](https://longman694.github.io/drumbeats/)**

---

## 📖 Overview

**Euclid-5** is a self-contained, browser-based drum computer that generates complex polyrhythms and polymetric grooves through **Euclidean rhythm algorithms**. Originally discovered by E. Bjorklund for nuclear accelerator timing and famously applied to music theory by computer scientist Godfried Toussaint (2005), Euclidean rhythms distribute $k$ drum hits as evenly as possible across $n$ steps.

Euclid-5 requires **zero external assets, audio samples, frameworks, or CDNs** — every drum sound is synthesized in real time via native Web Audio API oscillators, noise generators, and analog-modeled filter envelopes.

---

## ✨ Key Features

### 1. 🎛️ Programmatic 5-Voice Synthesizer (No Samples)
All instruments are generated dynamically from mathematical primitives:
* **Kick Drum (BD)**: Frequency-swept sine wave ($160\text{ Hz} \to 45\text{ Hz}$ over $0.25\text{ s}$ with exponential amplitude decay) paired with an initial punch triangle click transient.
* **Snare Drum (SD)**: Dual-layer engine combining filtered white noise burst ($1.5\text{ kHz}$ high-pass / band-pass) layered over a $180\text{ Hz}$ resonant body transient.
* **Closed Hi-Hat (CH)**: Crisp, metallic band-pass filtered noise burst with short exponential decay ($0.05\text{ s}$).
* **Open Hi-Hat (OH)**: Bright metallic noise burst through a $7\text{ kHz}$ high-pass filter with user-adjustable decay/sustain slider ($0.15\text{ s}$ to $0.80\text{ s}$).
* **Rimshot / Perc (RM)**: High-$Q$ resonant band-pass ping ($1.2\text{ kHz}$) with rapid exponential decay ($0.08\text{ s}$).

### 2. 🔇 Hi-Hat Choke Group (Exclusive Voice Logic)
* Just like classic analog drum machines (e.g. Roland TR-808/909), the Closed Hi-Hat and Open Hi-Hat share an **exclusive voice choke group**.
* Whenever a Closed Hat triggers, any ringing Open Hat envelope is immediately canceled and ramped to zero over a clickless $3\text{ ms}$ linear fade (`linearRampToValueAtTime`) to eliminate DC pops while cutting off open sustain.

### 3. ⏱️ Jitter-Free Audio Lookahead Scheduling
* Implements the gold-standard Web Audio lookahead architecture (ticking at $25\text{ ms}$ intervals to schedule audio events $100\text{ ms}$ ahead using high-precision hardware timestamps from `AudioContext.currentTime`).
* Playback remains rock-solid and jitter-free, regardless of UI rendering or tab load.
* Includes **Roger Linn / MPC Swing** ($50\%\text{ straight} \to 70\%\text{ groove shuffle}$).

### 4. 🌀 Concentric Polar Radar & Audio Oscilloscope Visualizer
* **5 Concentric Frequency Rings**: Ordered inside-to-outside from low to high frequency:
  1. Ring 1 (Inner): **Kick** (`#ff4757`)
  2. Ring 2: **Snare** (`#ffa502`)
  3. Ring 3: **Rimshot** (`#2ed573`)
  4. Ring 4: **Closed Hi-Hat** (`#1e90ff`)
  5. Ring 5 (Outer): **Open Hi-Hat** (`#a55eea`)
* **Real-Time Audio Oscilloscope & Spectrum Hub**:
  * Center hub houses an interactive master Web Audio `AnalyserNode`.
  * Renders a real-time circular oscilloscope waveform ribbon that flexes with the synthesized audio transient shape.
  * 36 radial frequency spectrum rays pulse along the hub's rim in real time.
* **Dynamic Node Scaling**: Node radiuses scale dynamically with step count to prevent overlapping up to 32 steps.
* **Geometric Euclidean Polygons**: Toggleable overlay connecting Euclidean hit vertices into geometric shapes.

### 5. 🎚️ 5-Voice Polymetric Channel Strips & Step Grid
* Each channel operates completely independently with dedicated controls:
  * **Steps ($n$, 2–32)**: Individual polymetric track length.
  * **Hits ($k$, 0–$n$)**: Number of Euclidean pulses.
  * **Rotation ($r$, 0–$n-1$)**: Circular pattern phase shift.
  * **Mute & Solo buttons**
  * **Track Volume slider**
  * **Decay slider** (for Open Hi-Hat)
* **Interactive Overrides**: Click any step in the linear matrix to toggle individual hits on or off, transforming mathematical Euclidean formulas into customized variations.

### 6. 📐 Polymetric Cycle Telemetry (LCM Macro)
* Displays real-time synchronization metrics across polymetric tracks:
  $$\text{Cycle Length} = \operatorname{LCM}(n_1, n_2, n_3, n_4, n_5)$$
* Shows total steps before resynchronization, equivalent $4/4$ measures, real-world cycle duration, and a live phase progress bar.

---

## 🎼 Built-In Presets

The preset menu is organized into three distinct musical traditions:

### 🏛️ Classical & Ethnomusicology
* **Afro-Cuban Son Clave & Shimmer** (112 BPM): Traditional tresillo and son clave with layered hi-hats.
* **Brazilian Bossa Nova & Samba** (125 BPM): Classic syncopated snare cross-stick pattern over quarter-note kick.
* **West African 12/8 (Gahu Bell)** (115 BPM): Traditional Ewe drumming bell pattern in compound 12/8 meter.
* **Kalamatianos (Balkan 7/8 Additive)** (130 BPM): Asymmetric Balkan folk meter structured as $3+2+2$.
* **Balkan / Macedonian 13/8** (136 BPM): Additive compound meter structured as $3+2+2+3+3$.

### ⚡ Electronic & Modern
* **Classic House & Offbeat Lift** (124 BPM): Four-on-the-floor kick with choked offbeat open hi-hats.
* **Minimal Techno Pocket** (126 BPM): Stripped-back hypnotic groove with rotating accents.
* **UK Garage / 2-Step Choke** (132 BPM): Syncopated kick and snare bounce with aggressive hi-hat choke interaction.
* **Drum & Bass Breakbeat** (174 BPM): High-speed breakbeat groove with fast rolling 16th hats.
* **Trap Half-Time Pocket** (140 BPM): Half-time snare on beat 3 with rolling hi-hat Euclidean distributions.

### 🔬 Polymetric & Experimental
* **Generative Polymetric Phasing (LCM Macro)** (120 BPM): Phase-shifting phasing patterns using coprime step lengths ($16, 15, 14, 7, 11$). Total cycle length: **120,120 steps** (7,507.5 bars / ~40 minutes before exact repetition).
* **Clear / Blank** (120 BPM): Clean slate with all tracks reset to zero hits.

---

## ⌨️ Controls & Shortcuts

| Action | Control |
| :--- | :--- |
| **Play / Pause** | `Spacebar` or click **▶ PLAY** button |
| **Reset Playhead** | Click **⏮ RESET** button |
| **Tap Tempo** | Click **TAP** button rhythmically |
| **Tempo / BPM** | Drag **TEMPO** slider ($60\text{--}200\text{ BPM}$) |
| **Groove Swing** | Drag **SWING** slider ($50\%\text{ straight} \to 70\%\text{ shuffle}$) |
| **Toggle Step** | Click any step in the linear grid to flip hit/rest |
| **Toggle Radar Play** | Click the center hub of the polar visualizer |
| **Toggle Polygons** | Click **POLYGONS: ON/OFF** button |
| **Channel Mute / Solo** | Click **M** (Mute) or **S** (Solo) on any voice strip |

---

## 🚀 Getting Started

### Option 1: Run via GitHub Pages
Open the live deployment directly in your browser:
[https://longman694.github.io/drumbeats/](https://longman694.github.io/drumbeats/)

### Option 2: Run Locally (Zero Installation)
Because Euclid-5 is 100% self-contained with no node modules, compilers, or build steps:
1. Clone the repository:
   ```bash
   git clone https://github.com/longman694/drumbeats.git
   cd drumbeats
   ```
2. Open `index.html` directly in any web browser:
   * **Windows**: Double-click `index.html` or run `start index.html`
   * **macOS**: `open index.html`
   * **Linux**: `xdg-open index.html`

> *Note: Audio automatically unlocks upon the first click or keypress in compliance with browser autoplay security policies.*

---

## 📂 Project Structure

```text
drumbeats/
├── index.html       # Self-contained application (HTML, CSS, Web Audio engine, & visualizations)
├── favicon.svg      # Vector SVG favicon with glowing concentric Euclidean rings
├── favicon.ico      # Multi-resolution ICO binary favicon
└── README.md        # Documentation and user guide
```

---

## 🧮 Theoretical Background

Euclidean rhythms were formalized by Godfried Toussaint in his seminal 2005 paper:
> *Toussaint, G. (2005). "The Euclidean Algorithm Generates Traditional Musical Rhythms." Proceedings of BRIDGES: Mathematical Connections in Art, Music, and Science.*

Bjorklund's algorithm calculates repeated integer division with remainders to distribute $k$ 1s across $n$ slots with maximal spacing. For instance:
* $E(4, 16) = [1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0]$ (Four-on-the-floor)
* $E(5, 16) = [1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0]$ (Bossa Nova clave)
* $E(7, 12) = [1, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0]$ (West African bell pattern)

In Euclid-5, each voice advances independently on a shared sixteenth-note clock, giving rise to polymetric phasing where patterns drift across measure boundaries and re-align at the Least Common Multiple.

---

## 📜 License

This project is open source and available under the [MIT License](LICENSE).

