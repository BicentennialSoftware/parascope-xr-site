# Parascope XR

**Parascope XR** is a mixed reality application for the Meta Quest 3S that transforms your passthrough camera feed into a real-time spectral visualization lab. Using custom GLSL shaders applied directly to the camera image, it renders 50 distinct visual modes — from scientific imaging simulations and motion analysis tools to audio-reactive visualizations, live magnetic field mapping, real-time barometric pressure monitoring, live 3D spatial point-cloud scanning via ARKit, and live LiDAR depth visualization streamed wirelessly from an iPhone.

Every mode runs entirely on-device with no cloud dependency. The passthrough view remains active at all times, keeping you grounded in your real environment while the app layers visual information on top of it.

---

## Hardware Requirements

- **Meta Quest 3S** (primary target; also compatible with Meta Quest 3)
- **iPhone with GyrOSC app** ($0.99, App Store) — required for Magnetic Vision (Mode 42)
- **iPhone with ZIG SIM app** (free, App Store) — required for Barometric Pressure (Mode 43)
- **iPhone with ZIG SIM Pro app** (App Store) — required for ARKit Spatial Scanner (Mode 44)
- **iPhone 12 or later with Record3D app** (free + in-app purchase, App Store) — required for LiDAR modes (45–49)
- Both devices on the same Wi-Fi network for all iPhone-dependent modes

---

## Controls

| Input | Action |
|---|---|
| **A / X Button** | Next mode |
| **B / Y Button** | Previous mode |
| **Thumbstick Up/Down** | Zoom in / out (most modes) |
| **Thumbstick Up/Down** | Adjust sensitivity (Magnetic Vision mode) |
| **Thumbstick Up/Down** | Adjust view scale (LiDAR modes 45–49) |
| **Trigger** | Toggle freeze (Strobe / Frame Freeze mode) |
| **Trigger** | Calibrate baseline (Magnetic Vision / Barometric Pressure modes) |

The mode name is displayed at the bottom of the view for 3 seconds after each change.

---

## Modes

Modes are organized into eight categories. Use A/X and B/Y to cycle through all 50.

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
| 43 | **Barometric Pressure** | Live barometric pressure monitoring with a 2-minute seismograph-style history graph. Edge vignette shifts blue/violet on pressure drops and amber/red on rises. Alerts pulse when deviation exceeds 0.5 hPa from baseline. |

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

### Barometric Pressure Visualization (Mode 43)

| # | Name | Description |
|---|---|---|
| 43 | **Barometric Pressure** | Live pressure monitoring with scrolling history graph and anomaly alerts. |

#### How It Works

An iPhone running **ZIG SIM** (free, App Store) sends barometric pressure readings from the iPhone's built-in sensor over UDP/JSON to the Quest on port 9000. The app records one sample per second and maintains a 2-minute rolling history.

#### Visualization

- **Edge vignette** tints the scene border based on pressure trend: blue/violet for dropping pressure, amber/red for rising pressure
- **Seismograph graph** at the bottom of the view plots the last 2 minutes of readings as a glowing colored line — green at baseline, blue for drops, amber/red for rises
- **Baseline reference** — a faint center line marks the calibrated zero point
- **Alert pulse** — edges flash when pressure deviates more than 0.5 hPa from baseline

#### Setup

1. Install **ZIG SIM** (free) on iPhone (App Store)
2. Put both devices on the same Wi-Fi network
3. In ZIG SIM: set target IP to the Quest's IP address, port **9000**, enable **Barometer**
4. Switch to Mode 43 — the first reading auto-sets the baseline
5. Optional: pull trigger to manually recalibrate the baseline to the current reading
6. Watch the graph — sudden drops are associated with cold spots and pressure anomalies

#### HUD Display (Mode 43)

- Connection status
- Current pressure in hPa
- Delta from baseline (±hPa) — shows `!` when alert threshold is exceeded

---

### ARKit Spatial Scanner (Mode 44)

| # | Name | Description |
|---|---|---|
| 44 | **ARKit Spatial Scanner** | Live 3D point cloud of your environment, captured by ARKit on an iPhone and streamed wirelessly to the Quest in real time. |

#### How It Works

An iPhone running **ZIG SIM Pro** (App Store) streams ARKit feature points over UDP/JSON to the Quest on port 9000. ARKit continuously tracks hundreds of 3D world-space anchor points as the phone camera scans the environment. The Quest receives up to 128 of these points per frame, converts them from ARKit's right-handed coordinate system to Unity's left-handed system, and renders them as a glowing particle cloud floating 1.5 m ahead of you.

#### Visualization

- **Point cloud** rendered as particles with depth-based color grading: near points glow warm white/yellow, far points shift to cool cyan
- **Cyan scanline sweep** pulses horizontally across the passthrough image to suggest active spatial scanning
- **Subtle vignette** frames the corners in dark cyan to focus attention on the scan volume
- The passthrough image is dimmed slightly so the point cloud stands out against the real environment

#### Setup

1. Install **ZIG SIM Pro** on iPhone (App Store)
2. Put both devices on the same Wi-Fi network
3. In ZIG SIM Pro: set target IP to the Quest's IP address, port **9000**, enable **ARKit** mode (feature points)
4. Set message rate to 10–30 Hz for smooth updates
5. Switch to Mode 44 — the HUD shows "Waiting..." until the first packet arrives, then "Connected" with a live point count

#### HUD Display (Mode 44)

- Connection status (`Waiting...` / `Connected`)
- Live feature point count

---

### LiDAR Visualization Suite (Modes 45–49)

An iPhone running **Record3D** streams a live RGBD video frame over WebRTC to the Quest on the local WiFi network. Each frame is a side-by-side texture — HSV-encoded depth on the left half, RGB color on the right. The Quest auto-discovers the iPhone by scanning the local network and connects automatically within ~8 seconds of switching to any LiDAR mode.

Requires **iPhone 12 or later** (LiDAR scanner required). iPhone 14 Pro or later delivers the best depth resolution.

**Scale control:** In any LiDAR mode, **thumbstick up/down** adjusts the view scale (0.15× to 1.0×) so you can size the image to match your physical environment without rebuilding.

| # | Name | Description |
|---|---|---|
| 45 | **LiDAR Depth Scan** | Per-pixel depth heatmap on a black background. Near surfaces glow hot white, mid-range turns green, distant surfaces shift to cyan. Passthrough is completely replaced inside the LiDAR frame. |
| 46 | **LiDAR RGB+Depth** | iPhone's live color image tinted by depth — real surface colors blended with the depth ramp. Passthrough shows outside the LiDAR frame. |
| 47 | **LiDAR Contour Bands** | Depth rendered as topographic contour bands with bright lines at equidistant depth intervals, like an elevation map. |
| 48 | **LiDAR Edge Outlines** | Bright outlines appear at depth discontinuities — object silhouettes and surface boundaries glow where near and far regions meet. |
| 49 | **LiDAR Bands+Edges** | Contour bands and edge outlines combined for maximum spatial detail. |

#### Color Scale

| Distance | Color |
|---|---|
| < 0.3 m | Hot white flash |
| 0.3 – 1.0 m | Warm amber / orange |
| 1.0 – 2.0 m | Bright green |
| 2.0 – 2.8 m | Cyan / blue |
| > 2.8 m or no reading | Black (Mode 45) or passthrough (Modes 46–49) |

#### Setup

1. Install **Record3D** on iPhone (App Store, free; WiFi streaming requires in-app purchase)
2. Put both devices on the same WiFi network
3. Open Record3D and start WiFi streaming
4. Switch to any LiDAR mode (45–49) — the app auto-discovers the iPhone and connects within ~8 seconds
5. Use **thumbstick up/down** to adjust the scale until objects appear at a natural size

#### HUD Display

- Connection status (`Waiting...` / `Connected | 192.168.x.x`)
- Auto-reconnects if the signal drops

---

## Permissions

| Permission | Required For |
|---|---|
| `CAMERA` | All modes — passthrough camera feed |
| `RECORD_AUDIO` | Modes 40–41 (audio visualization) |
| `MODIFY_AUDIO_SETTINGS` | Modes 40–41 (ambient audio capture) |
| `INTERNET` | Modes 42–49 (OSC/UDP/WebRTC reception) |
| `ACCESS_NETWORK_STATE` | Modes 42–49 |
| `com.oculus.permission.USE_SCENE` | Modes 35–36 (depth sensor) |
| `com.oculus.permission.EYE_TRACKING` | Gaze-aware features |
| `com.oculus.permission.HAND_TRACKING` | Future hand-input support |

---

## Privacy Policy

Parascope XR does not collect, store, transmit, or share any personal data.

- **Camera**: processed in real time on-device; no frames are saved or transmitted unless you explicitly take a photo or start a video recording using the in-app capture feature.
- **Microphone**: audio samples are processed in real time on-device for visualization only; no audio is recorded or transmitted.
- **Network (Modes 42–49)**: the app receives sensor data from GyrOSC (port 7000, UDP), ZIG SIM Pro (port 9000, UDP), and Record3D (WebRTC over local WiFi) on the same network. No data is sent beyond the local network. No internet connection is required.
- **Depth sensor**: depth data is used only for real-time visualization and is not stored.

No account, login, or personal information is required to use this app.

---



## Developer Information

**Developer:** Bicentennial Software  
bicentennialsoftware@gmail.com

[Privacy Policy](privacy-policy.md)

---


