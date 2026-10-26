# CONNECT 4D 
Vibecoded by Lorenzo Granado

> An interactive four-dimensional Connect Four and Qubic strategy matrix played inside a $4 \times 4 \times 4 \times 4$ Tesseract ($256$ hyper-cells, $10$ synchronized 3D projection cubes, and $520$ winning lines).

---

## Table of Contents

1. [Overview](#overview)
2. [Mathematical Foundation (The 520 Winning Lines)](#mathematical-foundation-the-520-winning-lines)
3. [The Complete Tesseract Guide](#the-complete-tesseract-guide)
   - [1. The 4 Coordinates ($X, Y, Z, W$)](#1-the-4-coordinates-x-y-z-w)
   - [2. Winning Lines in 4D Space](#2-winning-lines-in-4d-space)
   - [3. The 2D Hyper-Matrix Grid](#3-the-2d-hyper-matrix-grid)
   - [4. The 10 3D Hyper-Cube Projections](#4-the-10-3d-hyper-cube-projections)
   - [5. Dashboard, Move Log & PGN](#5-dashboard-move-log--pgn)
   - [6. Physics, AI & Move Confirmation](#6-physics-ai--move-confirmation)
   - [7. Tactical Assist & Dimension Inspector](#7-tactical-assist--dimension-inspector)
   - [8. Aesthetics, Themes & Audio Synthesizer](#8-aesthetics-themes--audio-synthesizer)
4. [Keyboard Shortcuts Reference](#keyboard-shortcuts-reference)
5. [Key Features & Architecture](#key-features--architecture)
6. [How to Run and Host](#how-to-run-and-host)
7. [Author & License](#author--license)

---

## Overview

**Connect 4D** expands the classic game of vertical gravity alignment and $4 \times 4 \times 4$ Qubic into Euclidean 4-space ($\mathbb{R}^4$). 

Instead of a single flat grid, the board consists of a complete **tesseract** of $4 \times 4 \times 4 \times 4 = 256$ cells. To make 4D spatial relationships readable without VR equipment, the game provides two synchronized views:
- **A 2D Hyper-Matrix:** A $4 \times 4$ macro-grid of $4 \times 4$ micro-grids with no visual occlusion.
- **10 Independent 3D Projections:** Isometric 3D wireframe cubes projecting every planar and spatial slice so that *every single 4D winning line appears as an unbroken 3D line in at least one cube*.

---

## Mathematical Foundation (The 520 Winning Lines)

In any $n$-dimensional hypercube of side length $k = 4$, a winning line consists of $4$ collinear cells whose coordinates step uniformly by $\Delta \in \{-1, 0, 1\}$. 

The number of winning lines where exactly $d$ coordinates vary ($1 \le d \le 4$) is calculated by:

$$\binom{n}{d} \cdot 2^{d - 1} \cdot k^{n - d}$$

For $n = 4$ dimensions and $k = 4$ cells per edge:

| Dimension Type | Varying Axes ($d$) | Formula | Total Lines | Description |
| :--- | :---: | :---: | :---: | :--- |
| **1D Orthogonal** | $d = 1$ | $\binom{4}{1} \cdot 2^0 \cdot 4^3 = 4 \cdot 1 \cdot 64$ | **256** | Standard straight rows, columns, vertical pegs, or hyper-strands. |
| **2D Planar Diagonals** | $d = 2$ | $\binom{4}{2} \cdot 2^1 \cdot 4^2 = 6 \cdot 2 \cdot 16$ | **192** | Diagonals across 2D slices ($XY, XZ, XW, YZ, YW, ZW$). |
| **3D Cube Diagonals** | $d = 3$ | $\binom{4}{3} \cdot 2^2 \cdot 4^1 = 4 \cdot 4 \cdot 4$ | **64** | Spatial cross-diagonals across 3D cubic volumes. |
| **4D Hyper-Diagonals** | $d = 4$ | $\binom{4}{4} \cdot 2^3 \cdot 4^0 = 1 \cdot 8 \cdot 1$ | **8** | Corner-to-opposite-corner hyper-space diagonals traversing all four axes. |
| **Total** | | | **520** | **Total distinct 4-in-a-row winning lines** |

---

## The Complete Tesseract Guide

### 1. The 4 Coordinates ($X, Y, Z, W$)
Every cell within the 256-cell matrix is addressed by four integer coordinates:

$$(X, Y, Z, W) \quad \text{where} \quad X, Y, Z, W \in \{1, 2, 3, 4\}$$

- **$X \in \{1, 2, 3, 4\}$:** Horizontal axis (Left to Right) inside any micro-grid or cubic slice.
- **$Y \in \{1, 2, 3, 4\}$:** Vertical axis (Bottom to Top) along a physical rod (the Gravity drop axis).
- **$Z \in \{1, 2, 3, 4\}$:** Depth axis (Front to Back). Represented as Macro-Rows in the 2D grid.
- **$W \in \{1, 2, 3, 4\}$:** Hyper-depth axis (4th spatial dimension). Represented as Macro-Columns in the 2D grid.

### 2. Winning Lines in 4D Space
A winning line is formed by any ordered set of 4 cells:

$$C_s = (X_0 + s \cdot \Delta x, \; Y_0 + s \cdot \Delta y, \; Z_0 + s \cdot \Delta z, \; W_0 + s \cdot \Delta w) \quad \text{for } s \in \{0, 1, 2, 3\}$$

where $(\Delta x, \Delta y, \Delta z, \Delta w) \in \{-1, 0, 1\}^4 \setminus \{(0, 0, 0, 0)\}$.

### 3. The 2D Hyper-Matrix Grid
The left panel flattens 4-space into a $4 \times 4$ matrix of $4 \times 4$ micro-boards:
- **Macro-Columns ($W = 1 \dots 4$) and Macro-Rows ($Z = 1 \dots 4$):** Select which $(W, Z)$ cross-section you are observing.
- **Micro-Columns ($X = 1 \dots 4$) and Micro-Rows ($Y = 4 \dots 1$):** Inside each cell block, $X$ advances horizontally and $Y$ advances vertically from base level $Y_1$ to top level $Y_4$.
- Click **Hide Grid** (or press `1`) to dedicate full screen width to the 3D projection view.

### 4. The 10 3D Hyper-Cube Projections
Because human vision is 3D, slicing a 4D object along its major planes reveals all inner structures without perspective distortion:
- **Row 1 ($W = 1 \dots 4$):** Four cubes at fixed $W$, with depth mapped along $Z_1 \to Z_4$.
- **Row 2 ($Z = 1 \dots 4$):** Four cubes at fixed $Z$, with depth mapped along $W_1 \to W_4$.
- **Row 3 ($W = Z$ and $W = -Z$):** Two diagonal hyper-slice projections where $W$ and $Z$ change simultaneously ($W_1 Z_1 \to W_4 Z_4$ and $W_1 Z_4 \to W_4 Z_1$).
- **Single-Cube Orbit Rotation:** Dragging any individual cube rotates only that specific projection. Zoom is locked so cubes maintain consistent scale.

### 5. Dashboard, Move Log & PGN
- **Turn Indicators & Counters:** Real-time counters track placed pieces ($P$) and active 3-in-a-row unblocked threats ($T$).
- **State Timeline & Jump:** Use **Back** ($\leftarrow$) and **Forward** ($\to$) buttons, or click any move chip (`#0`, `#1`, `#2`...) to jump directly to any prior board state.
- **PGN Export / Import:** Matches can be serialized into standardized Connect 4D Portable Game Notation (PGN) or imported via the modal (`E` / `J`).
- **Shareable Game Links:** Clicking **Copy Game Link** (`Y`) encodes the complete game state into a compressed binary Base64URL string (`?g=...`) that can be sent to anyone.

### 6. Physics, AI & Move Confirmation
- **Gravity Y-Drop vs. Free 4D Qubic:**
  - *Gravity Y-Drop (Default):* Pieces drop down vertical rods to the lowest unoccupied $Y$ level for column $(X, Z, W)$.
  - *Free 4D Qubic:* Pieces float in 4D space and can be placed directly into any open cell.
- **2-Click Confirm vs. 1-Click Instant:**
  - *2-Click Confirm (Default):* First click locks the cell/column for inspection; second click (or `Enter`) confirms the move.
  - *1-Click Instant:* Places the piece immediately upon clicking.
- **Game Modes:** 1-Player vs. AI, 2-Player Pass-and-Play, and AI vs. AI exhibition (pausable with `Space`).
- **AI Engine:** Heuristic evaluation engine with 2-ply minimax lookahead on Master difficulty.

### 7. Tactical Assist & Dimension Inspector
- **Threat Radar (`T`):** Highlights every cell that creates an immediate win for either player.
- **Ghost Diagonals (`L`):** Projects dashed rays through the hovered or locked piece for all active winning lines passing through it.
- **Distinct Line IDs (`C`):** Color-codes each line ($L_1 \dots L_{15}$) across all 10 cubes so corresponding 3D projections can be identified at a glance.
- **$1\times$ Canonical Only (`K`):** Deduplicates ghost rays so each 4D line is drawn in only one canonical 3D cube.
- **Dimension Inspector (`X`):** Inspects exact coordinates $(X, Y, Z, W)$ of any locked cell and lists all intersecting hyper-lines.

### 8. Aesthetics, Themes & Audio Synthesizer
- **Paper & Pencil Aesthetic (Default):** Graph-paper notebook style with fountain-pen blue circles ($O$) and red-pencil crosses ($X$).
- **Sci-Fi Matrix Aesthetic:** Glowing hologram interface with luminous spheres and laser overlays.
- **Light & Dark Themes:** Warm parchment / daylight mode or charcoal / deep-space mode.
- **Web Audio API Synthesizer:** Real-time procedural sound effects for piece locks, drops, and victories without external audio assets.

---

## Keyboard Shortcuts Reference

| Key | Action |
| :---: | :--- |
| <kbd>Enter</kbd> | Confirm locked move |
| <kbd>Esc</kbd> | Unlock selected cell / Dismiss active modal |
| <kbd>&larr;</kbd> / <kbd>U</kbd> | Undo / Step back in history |
| <kbd>&rarr;</kbd> / <kbd>R</kbd> | Redo / Step forward in history |
| <kbd>N</kbd> | Start new game |
| <kbd>F</kbd> | Toggle distraction-free Fullscreen mode |
| <kbd>O</kbd> | Open Game & Assist Settings modal |
| <kbd>X</kbd> | Open Dimension Inspector & Diagonal ID Key |
| <kbd>H</kbd> / <kbd>?</kbd> | Open How 4D Works Guide |
| <kbd>E</kbd> | Export Connect 4D PGN |
| <kbd>J</kbd> | Import Connect 4D PGN |
| <kbd>Y</kbd> | Copy shareable game link (`?g=...`) |
| <kbd>1</kbd> | Toggle 2D Hyper-Matrix Grid visibility |
| <kbd>2</kbd> | Toggle 10 3D Hyper-Cubes visibility |
| <kbd>G</kbd> | Toggle Gravity Y-Drop / Free 4D Qubic mode |
| <kbd>M</kbd> | Cycle player modes (1P vs AI / 2P Pass / AI vs AI) |
| <kbd>Space</kbd> | Pause / Resume AI vs AI match |
| <kbd>D</kbd> | Cycle AI Difficulty (Casual / Tactical / Master) |
| <kbd>T</kbd> | Toggle Threat Radar overlay |
| <kbd>L</kbd> | Toggle Ghost Diagonals overlay |
| <kbd>C</kbd> | Toggle Distinct Line Colors ($L_1 \dots L_{15}$) |
| <kbd>K</kbd> | Toggle $1\times$ Canonical Cube deduplication |
| <kbd>I</kbd> | Request AI Tactical Hint |
| <kbd>P</kbd> | Switch aesthetic (Paper & Pencil / Sci-Fi Matrix) |
| <kbd>B</kbd> | Switch theme (Light / Dark) |
| <kbd>S</kbd> | Toggle procedural sound synthesizer |
| <kbd>7</kbd> / <kbd>8</kbd> / <kbd>9</kbd> | Camera angle presets for selected cube (Iso / Top / Front) |
| <kbd>0</kbd> | Cycle 3D projection cube layouts |

---

## Key Features & Architecture

- **Zero Build Step:** The entire game runs from a single HTML file with no Node.js, Webpack, or npm dependencies.
- **Hardware-Accelerated HTML5 Canvas:** The 3D engine computes perspective transformations and depth sorting natively on an HTML5 `<canvas>`.
- **SVG Overlay Layer:** Winning lines and 2D hyper-diagonals are rendered via dynamic SVG overlays with vector precision.
- **State Compression:** Game state URLs use bitwise packing into Base64URL parameters, allowing complex board states to be shared via short URLs.
- **Full Touch and Mobile Support:** Supports desktop mouse drag rotation as well as single-finger touch interaction on mobile devices.
