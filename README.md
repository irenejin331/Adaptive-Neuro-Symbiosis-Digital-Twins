# Adaptive-Neuro-Symbiosis-Digital-Twins
An AI-driven human-machine interaction framework integrating multimodal intent recognition, cognitive digital twins-based real-time simulation, and adaptive robotic control.
# Adaptive Neuro-Symbiosis Digital Twin (ANS-DT)
### Multimodal Human Intent Recognition and Adaptive Robot Control for Human–Robot Collaboration

## Overview

**Adaptive Neuro-Symbiosis Digital Twin (ANS-DT)** is a human–robot collaboration (HRC) framework that integrates multimodal human intent recognition with synchronized digital twins to enable adaptive and safety-aware robotic behavior.

This demonstration illustrates a shared-workspace scenario in which a human worker reaches into a shared parts bin while a robotic arm performs a part-transfer operation.

The framework conceptually connects two digital-twin layers:

- **Cognitive Digital Twin (CDT):** Interprets human behavior by integrating visual and physiological information to estimate human intent and confidence.
- **Robotic Digital Twin (RDT):** Adapts robotic speed and operational states according to the estimated human intent and safety conditions.

The objective is to demonstrate how human-centered intelligence can support more responsive, collaborative, and safety-aware robotic systems.

## Demo Preview

The demonstration presents a simulated human–robot workcell with:

- A human worker performing reaching and interaction movements.
- A robotic arm transferring parts within a shared workspace.
- A cognitive twin visualizing human intent and multimodal fusion.
- A digital-twin coordination layer monitoring operational and fallback states.
- A robotic twin dynamically adjusting its speed according to the estimated interaction state.

## System Architecture

The ANS-DT framework consists of three interconnected components.

### 1. Cognitive Digital Twin (CDT)

The cognitive twin estimates human intent using multimodal information.

The conceptual AI architecture uses a **CNN-LSTM with cross-attention fusion**, integrating:

- **Visual information:** Human movement and body-motion observations.
- **Physiological information:** Human physiological signals.
- **Multimodal fusion:** Adaptive weighting of visual and physiological features.

The fusion mechanism is represented as:

\[
Z = w_v Z_{vision} + w_p Z_{physiology}
\]

where:

- \(Z_{vision}\): Visual feature representation.
- \(Z_{physiology}\): Physiological feature representation.
- \(w_v\): Visual modality weight.
- \(w_p\): Physiological modality weight.

The cognitive twin publishes the following information:

| Variable | Description |
|---|---|
| Intent State | Estimated human interaction state |
| Confidence | Intent prediction confidence |
| Vision Weight | Contribution of visual information |
| Physiology Weight | Contribution of physiological information |

### 2. Digital Twin Coordination Layer

The coordination layer connects cognitive intelligence with robotic behavior.

It monitors human intent and operational conditions while maintaining a fallback mechanism for safety-aware control.

The demonstration includes the following intent states:

- `monitoring`
- `reach_predicted`
- `reach_active`
- `retreating`

The corresponding digital-twin operational states include:

- `NormalOperation`
- `SpeedLimited`
- `SafeHold`

The coordination layer illustrates bidirectional learning and fallback logic between the cognitive and robotic twins.

### 3. Robotic Digital Twin (RDT)

The robotic twin adapts its operational speed based on the interaction state.

The demonstration uses a normalized robot speed scale:

\[
S_{robot} \in [0,1]
\]

where:

- `1.0`: Full operating speed.
- Intermediate values: Reduced operating speed.
- Values approaching `0`: Near-stop or safe-hold behavior.

When human reaching activity is predicted or detected, the robotic twin progressively reduces its speed. When the interaction risk decreases, the system restores normal operation.

This demonstrates the concept of intent-aware adaptive robot control rather than relying exclusively on static safety boundaries.

## Demonstration Workflow

The simulated scenario illustrates the following interaction sequence:

1. **Normal Operation:** The robot operates at its nominal speed while monitoring the human worker.
2. **Intent Prediction:** The cognitive twin detects an emerging reaching movement and updates the estimated intent.
3. **Multimodal Fusion:** Visual and physiological modality weights are dynamically represented in the cognitive twin.
4. **Adaptive Speed Reduction:** The robotic twin reduces its speed as human interaction risk increases.
5. **Safe-Hold Behavior:** During active human interaction, the robot transitions toward a near-stop state.
6. **Recovery:** As the interaction concludes, the system progressively restores normal robotic operation.

## Technical Implementation

### Simulation Environment

The demonstration is developed as an animated 3D digital-twin scene using Universal Scene Description (OpenUSD).

| Component | Description |
|---|---|
| Scene Format | OpenUSD (`.usda`) |
| Portable Asset | USDZ (`.usdz`) |
| Preview | MP4 |
| Coordinate System | Z-up |
| Measurement Unit | Meters |
| Animation Frame Rate | 24 FPS |
| Animation Duration | Approximately 13 seconds |
| Animation Samples | 313 |

### USD Scene Structure

The scene contains the following major elements:

```text
World
├── Looks
│   ├── Materials
│   └── Surface Shaders
├── Workcell
├── Table
├── BinA_Shared
├── BinB_Supply
├── Robot
├── Human
├── PartA
├── PartB
└── ANS_DT
    ├── CDT_Cognitive
    ├── RDT_Robotic
    ├── DT_Core
    ├── SharedZoneBinA
    └── SpeedGauge
```

### Digital-Twin Data Representation

The USD scene includes custom animation attributes representing the state of the ANS-DT framework:

| USD Attribute | Function |
|---|---|
| `ans:intent:state` | Human intent classification |
| `ans:intent:confidence` | Intent confidence |
| `ans:fusion:visionWeight` | Visual modality contribution |
| `ans:fusion:physiologyWeight` | Physiological modality contribution |
| `ans:fallback:state` | Digital-twin fallback state |
| `ans:robot:speedScale` | Adaptive robot speed |

These attributes are time-sampled and synchronized with the animated scene.

## Repository Structure

```text
ANS-DT/
│
├── demo/
│   ├── hrc_ans_dt_demo_preview.mp4
│   ├── hrc_ans_dt_demo.usda
│   └── hrc_ans_dt_demo.usdz
│
└── README.md
```

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/irenejin331/Adaptive-Neuro-Symbiosis-Digital-Twins.git
cd Adaptive-Neuro-Symbiosis-Digital-Twins
```

### 2. Explore the Demo

Open the MP4 preview:

```text
demo/hrc_ans_dt_demo_preview.mp4
```

### 3. Open the 3D Digital Twin

Open either of the following assets using a compatible OpenUSD viewer or 3D application:

```text
demo/hrc_ans_dt_demo.usda
```

or

```text
demo/hrc_ans_dt_demo.usdz
```

Compatible USD applications can be used to inspect the scene and its animated properties.

## Current Demonstration Scope

**Important:** This repository contains a visual and animated digital-twin demonstration.

The intent states, confidence values, multimodal fusion weights, and robot speed adjustments are scripted stand-ins for model and control outputs.

The current assets demonstrate the proposed system architecture and interaction workflow. They do not constitute a live connection to physiological sensors, a deployed CNN-LSTM inference pipeline, or a physical robot controller.

## Future Development

Potential extensions of the ANS-DT framework include:

- Real-time human pose estimation using RGB-D cameras.
- Integration of physiological sensing, including EEG, EMG, ECG, and GSR/EDA.
- Deployment of CNN-LSTM-based multimodal intent recognition.
- Real-time cognitive and robotic digital-twin synchronization.
- Integration with NVIDIA Isaac Sim and ROS 2.
- Reinforcement-learning-based adaptive robot trajectory and speed control.
- Real-world validation of human–robot collaboration and safety performance.

## Research Contribution

ANS-DT explores a human-centered approach to intelligent robotic collaboration by connecting human cognitive-state estimation with adaptive robotic behavior.

Rather than treating human presence as a static obstacle, the framework considers human intent as a dynamic source of information for robotic decision-making.

By integrating multimodal sensing, AI-based intent recognition, digital-twin coordination, and adaptive robotic control, this research aims to advance safer and more intelligent human–robot collaborative environments.

---
