# Visual Spectrum

**Visual Spectrum** is a mixed reality application for the Meta Quest 3S that transforms your passthrough camera feed into a real-time spectral visualization lab. Using custom GLSL shaders applied directly to the camera image, it renders 43 distinct visual modes — from scientific imaging simulations and motion analysis tools to audio-reactive visualizations and live magnetic field mapping.

Every mode runs entirely on-device with no cloud dependency. The passthrough view remains active at all times, keeping you grounded in your real environment while the app layers visual information on top of it.

---

## Hardware Requirements

- **Meta Quest 3S** (primary target; also compatible with Meta Quest 3)
- **iPhone with GyrOSC app** — required for Magnetic Vision mode only (Mode 42)
- Both devices on the same Wi-Fi network for Magnetic Vision

---

## Controls

| Input | Action |
|---|---|
| **A / X Button** | Next mode |
| **B / Y Button** | Previous mode |
| **Thumbstick Up/Down** | Zoom in / out (most modes) |
| **Thumbstick Up/Down** | Adjust sensitivity (Magnetic Vision mode) |
| **Trigger** | Toggle freeze (Strobe / Frame Freeze mode) |
| **Trigger** | Calibrate baseline (Magnetic Vision mode) |

The mode name is displayed at the bottom of the view for 3 seconds after each change.

---

## Modes

Modes are organized into eight categories. Use A/X and B/Y to cycle through all 43.

---

### Standard Imaging (Modes 0–8)

| # | Name | Description |
|---|---|---|
| 0 | **Normal RGB** | Unmodified passthrough — fully transparent overlay. |
| 1 | **Night Vision** *(Simulated)* | Green-channel amplification and gamma boost to simulate low-light intensification. |
| 2 | **False Color** | Luminance mapped to a full-spectrum color ramp — cool tones for dark regions, warm tones for bright. |
| 3 | **Spectral Exaggeration** | Hue and saturation pushed beyond natural values to make subtle color differences visible. |
| 4 | **Channel Isolation** | Cycles through red, green, and blue channels individually to reveal per-channel detail. |
| 5 | **Edge + Color Hybrid** | Sobel edge detection blended over the original color image — outlines objects while preserving color. |
| 6 | **Infrared** *(Simulated)* | Near-IR simulation: vegetation brightens, sky darkens, skin tones shift warm. |
| 7 | **Ultraviolet** *(Simulated)* | UV-fluorescence simulation with scintillation sparkle on high-luminance surfaces. |
| 8 | **Color Space Rotation** | Continuously rotates the RGB color axes through HSV space, cycling all hues over time. |

---

### Motion & Temporal Analysis (Modes 9–12)

| # | Name | Description |
|---|---|---|
| 9 | **Motion Amplification** | Frame-differenced motion signal amplified and tinted; subtle movement becomes visible. |
| 10 | **Temporal Persistence** | Each frame blends with a decaying history buffer — moving objects leave glowing trails. |
| 11 | **Focus Peaking** | Highlights in-focus edges with a bright color overlay, similar to a camera's focus-assist mode. |
| 12 | **Strobe / Frame Freeze** | Pulses the view at a configurable strobe rate. Trigger button freezes on a single frame. |

---

### Color Processing (Modes 13–15)

| # | Name | Description |
|---|---|---|
| 13 | **Selective Color** | Preserves a single target hue and desaturates everything else to grayscale. |
| 14 | **Posterization** | Reduces the image to a small number of discrete color levels for a graphic, screen-printed look. |
| 15 | **Contrast Enhancement** | Stretches the luminance histogram between configurable black and white points. |

---

### Sensor Simulation (Modes 16–17)

| # | Name | Description |
|---|---|---|
| 16 | **UV Scintillation** *(Simulated)* | Adds animated sparkle to bright surfaces, simulating UV fluorescence response. |
| 17 | **Polarization** *(Simulated)* | Simulates a rotating polarizing filter — reflective surfaces dim and brighten as the virtual angle sweeps. |

---

### Motion Analysis (Modes 18–25)

| # | Name | Description |
|---|---|---|
| 18 | **Motion-Triggered Edges** | Edges are only drawn where motion is detected; static regions are suppressed. |
| 19 | **Edge Persistence Map** | Detected edges accumulate and slowly decay, building a ghosted map of object outlines over time. |
| 20 | **Motion Direction Binning** | Colors pixels by the cardinal direction of motion — up, down, left, right each get a distinct hue. |
| 21 | **Edge Flow Vectors** | Visualizes optical-flow direction as a hue-wheel overlay, with brightness keyed to flow magnitude. |
| 22 | **Motion Magnitude Zones** | Divides motion intensity into discrete color bands — slow motion cool, fast motion hot. |
| 23 | **Motion History Trails** | Persistent motion trails with decay; recent movement is bright, older movement fades. |
| 24 | **Object Segmentation** | Attempts to separate moving foreground objects from the static background using frame differencing. |
| 25 | **Motion-Based Zoom** | Applies a dynamic zoom effect keyed to motion magnitude — moving regions appear larger. |

---

### Sensor Fusion (Modes 26–27)

| # | Name | Description |
|---|---|---|
| 26 | **Audio-Visual Sync** | Microphone amplitude modulates color saturation and brightness in real time. |
| 27 | **Head Motion Compensation** | Applies a stabilization warp based on head velocity from the IMU to reduce perceived shake. |

---

### Practical Tools (Modes 28–30)

| # | Name | Description |
|---|---|---|
| 28 | **Measurement Mode** | Overlays scale reference lines to assist with visual distance or size estimation. |
| 29 | **Document Capture** | Applies adaptive contrast and perspective correction hints optimized for reading flat text. |
| 30 | **Low-Light Enhancement** | Multi-stage gain, gamma lift, and noise-suppression pass for dim environments. |

---

### Anomaly Detection (Modes 31–33)

| # | Name | Description |
|---|---|---|
| 31 | **Entropy Visualization** | Maps local pixel entropy (disorder/texture complexity) to a color overlay — patterns stand out. |
| 32 | **Temporal Anomaly Detection** | Highlights regions that deviate from the recent temporal average — sudden changes glow bright. |
| 33 | **Frequency Analysis** | Spatial frequency decomposition; high-frequency detail rendered as one color, low-frequency as another. |

---

### Utility (Mode 34)

| # | Name | Description |
|---|---|---|
| 34 | **Stuck Pixel Fix** | Cycles the display through full red, green, blue, white, and black fields to exercise stuck pixels. |

---

### 3D Spatial Depth (Modes 35–37)

These modes use the Quest 3S depth sensor via the AR Foundation occlusion API. A USE_SCENE permission prompt will appear on first launch.

| # | Name | Description |
|---|---|---|
| 35 | **Wireframe Mesh** | Depth data rendered as an edge-detected wireframe showing the geometry of the room. |
| 36 | **Low Poly** | Depth rendered as flat-shaded polygonal regions, giving the environment a faceted, low-polygon aesthetic. |

---

### Creative & Motion (Modes 38–39)

| # | Name | Description |
|---|---|---|
| 38 | **Neon Glow** | Multi-scale Sobel edge detection with angle-based hue assignment — edges glow in neon colors that follow their own orientation. A bloom halo fans out from each edge. |
| 39 | **Long Exposure** | Accumulates camera frames in a persistent buffer; motion leaves bright luminous trails while static areas remain sharp. Blend and persistence are tunable. |

---

### Audio Visualization (Modes 40–41)

These modes use the device microphone. A RECORD_AUDIO permission prompt will appear on first use. The app sets the Android audio mode to MODE_NORMAL so ambient and speaker audio is captured alongside voice.

| # | Name | Description |
|---|---|---|
| 40 | **Waveform Overlay** | Live PCM waveform drawn as a glowing green line across the center of the view. Dominant frequency is displayed at the top of the screen in Hz. |
| 41 | **Spectrum Analyzer** | 32-band frequency spectrum rendered as color-coded vertical bars (red → yellow → cyan from low to high frequency). Bars are center-screen, limited in height so passthrough remains visible. Peak frequency shown in Hz overlay. |

**Technical notes:** Frequency data is computed via a manual DFT with precomputed twiddle factors on logarithmically-spaced bins (80 Hz – 8 kHz) with a Hann window to reduce spectral leakage. This approach bypasses the Unity AudioSource DSP chain entirely, which would return zeros at volume 0.

---

### Magnetic Field Visualization (Mode 42)

| # | Name | Description |
|---|---|---|
| 42 | **Magnetic Vision** | Real-time magnetic dipole field line visualization driven by live magnetometer data from an iPhone. |

#### How It Works

An iPhone running the **GyrOSC** app ($0.99, App Store) sends magnetometer data over UDP/OSC to the Quest on a shared Wi-Fi network. The Quest receives the data on port 7000, computes field strength (√(x²+y²+z²) in μT), and renders the result as an interactive field line diagram.

#### Visualization

The rendering uses the exact magnetic dipole field line equation **r = r₀ · sin²(θ)** — the same formula that produces the classic iron-filings diagram around a bar magnet. The dipole axis rotates in real time to match the measured field direction.

- **Arcing field lines** curve from N pole to S pole, animated with flowing dashes
- **Color** maps to field strength: blue (weak) → cyan → green → orange → warm white (strong)
- **Speed** of the flowing dashes scales with field strength
- **Z-axis glow** at screen center: gold when the field points toward the viewer, blue when pointing away
- **Red dot** = north pole, **Blue dot** = south pole, positioned along the field axis
- **Thumbstick** adjusts sensitivity (9 levels: 0.25× to 8×) without leaving the mode
- **Trigger** calibrates the baseline to zero, stripping out Earth's ambient field (~50 μT) so only local anomalies show

#### Setup

1. Install **GyrOSC** on iPhone (App Store, $0.99)
2. Put both devices on the same Wi-Fi network
3. In GyrOSC: set target IP to the Quest's IP address, port **7000**, enable Magnetometer
4. Switch to Mode 42 — the HUD shows "Waiting..." until the first packet arrives, then "Connected"
5. Optional: pull trigger to zero the Earth background field

#### HUD Display (Mode 42)

A heads-up panel at the top of view shows three rows:
- Connection status
- Live field strength in μT
- Current sensitivity level

---

## Permissions

| Permission | Required For |
|---|---|
| `CAMERA` | All modes — passthrough camera feed |
| `RECORD_AUDIO` | Modes 40–41 (audio visualization) |
| `MODIFY_AUDIO_SETTINGS` | Modes 40–41 (ambient audio capture) |
| `INTERNET` | Mode 42 (OSC/UDP reception) |
| `ACCESS_NETWORK_STATE` | Mode 42 |
| `com.oculus.permission.USE_SCENE` | Modes 35–36 (depth sensor) |
| `com.oculus.permission.EYE_TRACKING` | Gaze-aware features |
| `com.oculus.permission.HAND_TRACKING` | Future hand-input support |

---

## Privacy Policy

Visual Spectrum does not collect, store, transmit, or share any personal data.

- **Camera**: processed in real time on-device; no frames are saved or transmitted unless you explicitly take a photo or start a video recording using the in-app capture feature.
- **Microphone**: audio samples are processed in real time on-device for visualization only; no audio is recorded or transmitted.
- **Network (Mode 42 only)**: the app listens on a local UDP port to receive magnetometer data from GyrOSC on the same network. No data is sent outbound. No internet connection is required or used.
- **Depth sensor**: depth data is used only for real-time visualization and is not stored.

No account, login, or personal information is required to use this app.

---

## Open Source

Source code is available at [github.com/christopherhe1/visual-spectrum](https://github.com/christopherhe1/visual-spectrum).

---

*Built with Unity 6 · OpenXR · AR Foundation · Meta XR SDK · targeting Meta Quest 3S*
