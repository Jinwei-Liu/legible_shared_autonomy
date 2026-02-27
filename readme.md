# Legible Shared Autonomy: Implicit Communication of Robot Belief through Motion

---

## Abstract

Shared autonomy systems combine human input with autonomous assistance to help users with motor impairments control robot arms by inferring user goals and providing guidance. However, the robot's internal beliefs about user goals cannot be observed by users. Traditional shared autonomy systems provide assistance along efficient shortest paths toward inferred goals, but when multiple objects lie in similar directions, such assistive motion remains ambiguous and fails to reveal the specific target identified by the robot. This creates two critical problems. First, when the robot correctly infers the goal, users continue controlling because they cannot perceive understanding from ambiguous assistive motion, wasting effort when autonomous completion would suffice. Second, when the robot misunderstands intent, users cannot quickly detect errors until assistive motion diverges significantly, requiring substantial corrective input. We address this by introducing legible motion into shared autonomy: robot actions must both advance toward the goal and clearly reveal which goal has been inferred, enabling users to understand the robot's beliefs and adjust control accordingly. The robot modulates communication strength through confidence-aware adaptive control authority: providing assertive legible assistance when confident while increasing user authority when uncertain, transforming shared autonomy into transparent bidirectional collaboration. User studies with a six degree-of-freedom robot arm demonstrate X\% reduction in user control effort compared to standard shared autonomy while maintaining task success rates.

---

## Key Contributions

**1. Action-Level Legibility Metric**

We propose the first action-level legibility metric suitable for real-time control:

$$\mathcal{L}(\boldsymbol{a}_R \mid s^t, \theta^*) = \log \pi_H(\boldsymbol{a}_R \mid s^t, \theta^*) - \log \max_{\theta \neq \theta^*} \pi_H(\boldsymbol{a}_R \mid s^t, \theta)$$

Unlike prior trajectory-level approaches that optimize complete paths offline, our metric enables efficient computation at each timestep.

**2. Dual Optimization Framework**

Robot action selection balances legibility and task performance:

$$\boldsymbol{a}_R^* = \arg\max_{\boldsymbol{a}_R} \left[ \lambda \mathcal{L}(\boldsymbol{a}_R \mid s^t, \theta^*) + Q(\boldsymbol{a}_R, s^t, \theta^*) \right]$$
---

## Experimental Setup

<p align="center">
  <img src="figures/experimental_setup.pdf" alt="Experimental Setup" width="700"/>
</p>

**Design:** Within-subjects study with 10 participants

**Conditions:**
- λ=0 (Standard SA): Efficient but ambiguous motion
- λ=5 (Medium Legibility): Balanced approach  
- λ=10 (High Legibility): Maximum discriminative motion

**Workspace:** 2D environment (800×600 pixels) with two closely spaced goals creating directional ambiguity

---

## Trajectory Animations

<table>
  <tr>
    <td align="center"><img src="trajectory_animations/participant_1_trajectories.gif" width="200"/><br><sub>Participant 1</sub></td>
    <td align="center"><img src="trajectory_animations/participant_2_trajectories.gif" width="200"/><br><sub>Participant 2</sub></td>
    <td align="center"><img src="trajectory_animations/participant_3_trajectories.gif" width="200"/><br><sub>Participant 3</sub></td>
    <td align="center"><img src="trajectory_animations/participant_4_trajectories.gif" width="200"/><br><sub>Participant 4</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="trajectory_animations/participant_5_trajectories.gif" width="200"/><br><sub>Participant 5</sub></td>
    <td align="center"><img src="trajectory_animations/participant_6_trajectories.gif" width="200"/><br><sub>Participant 6</sub></td>
    <td align="center"><img src="trajectory_animations/participant_7_trajectories.gif" width="200"/><br><sub>Participant 7</sub></td>
    <td align="center"><img src="trajectory_animations/participant_10_trajectories.gif" width="200"/><br><sub>Participant 10</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="trajectory_animations/participant_11_trajectories.gif" width="200"/><br><sub>Participant 11</sub></td>
    <td align="center"><img src="trajectory_animations/participant_12_trajectories.gif" width="200"/><br><sub>Participant 12</sub></td>
    <td align="center"><img src="trajectory_animations/participant_13_trajectories.gif" width="200"/><br><sub>Participant 13</sub></td>
    <td align="center"><img src="trajectory_animations/participant_15_trajectories.gif" width="200"/><br><sub>Participant 15</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="trajectory_animations/participant_dong_trajectories.gif" width="200"/><br><sub>Participant Dong</sub></td>
    <td align="center"><img src="trajectory_animations/participant_gong_trajectories.gif" width="200"/><br><sub>Participant Gong</sub></td>
    <td align="center"><img src="trajectory_animations/participant_shuxian_trajectories.gif" width="200"/><br><sub>Participant Shuxian</sub></td>
    <td align="center"><img src="trajectory_animations/participant_sun_trajectories.gif" width="200"/><br><sub>Participant Sun</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="trajectory_animations/participant_wangchao_trajectories.gif" width="200"/><br><sub>Participant Wangchao</sub></td>
    <td align="center"><img src="trajectory_animations/participant_wangqi_trajectories.gif" width="200"/><br><sub>Participant Wangqi</sub></td>
    <td align="center"><img src="trajectory_animations/participant_xing_trajectories.gif" width="200"/><br><sub>Participant Xing</sub></td>
    <td align="center"><img src="trajectory_animations/participant_zhang_trajectories.gif" width="200"/><br><sub>Participant Zhang</sub></td>
  </tr>
</table>

---

## Main Results

<p align="center">
  <img src="figures/combined_figure.pdf" alt="Results" width="900"/>
</p>

**Transparency Metrics:**
- Understanding rate: 36% → 94-98% (Standard SA → Legible)
- Prediction accuracy: 48% → 96-98%
- Statistical significance: χ²(2) = 66.01, p < 0.001

**Subjective Experience:**
- Intuitiveness ratings: 3.70 → 7.70 (1-10 scale)
- Collaboration ratings: 3.60 → 7.70
- Strong correlation between measures: r = 0.92, p < 0.001

**Key Finding:** Medium and high legibility produced equivalent benefits, suggesting moderate emphasis suffices for transparency while preserving efficiency.

---

## Repository Structure
```
legible_autonomy/
├── figures/                          # Paper figures
│   ├── experimental_setup.pdf
│   ├── beta_heatmap.pdf
│   └── combined_figure.pdf
│
├── trajectory_animations/            # Participant trajectory GIFs
│   ├── participant_001_trajectories.gif
│   ├── participant_002_trajectories.gif
│   └── ...
│
├── experiment_data/                  # Raw experiment data
├── core/                            # Core algorithms
├── experiment_collection.py         # Main experiment interface
└── analyze_data.py                  # Statistical analysis
```

---

## Reproducing Results

**Installation:**
```bash
git clone <repository-url>
cd legible_autonomy
pip install -r requirements.txt
```

**Generate trajectory animations:**
```bash
python generate_trajectory_animations.py --input ./experiment_data --output ./trajectory_animations
```

**Run statistical analysis:**
```bash
python analyze_data.py --input ./experiment_data --output ./figures
```
