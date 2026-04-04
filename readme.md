# Legible Shared Autonomy: Implicit Communication of Robot Belief through Motion

---

## Abstract

Shared autonomy systems combine user input with autonomous assistance to help users with motor impairments control robot arms to perform everyday manipulation tasks, by inferring user goals and providing appropriate guidance. However, the robot's internal beliefs about user goals cannot be observed by users. Traditional shared autonomy systems provide assistance along efficient shortest paths toward inferred goals, but when multiple objects lie in similar directions, such assistive motion remains ambiguous and fails to reveal the specific goal identified by the robot. This creates two critical problems. First, when the robot correctly infers the goal, users continue controlling because they cannot perceive understanding from ambiguous assistive motion, wasting effort when autonomous completion would suffice. Second, when the robot misunderstands intent, users cannot quickly detect errors until assistive motion diverges significantly, requiring substantial corrective input. We address this by introducing legible motion into shared autonomy, where robot actions must both advance toward the goal and clearly reveal which goal has been inferred, enabling users to understand the robot's beliefs and adjust control accordingly. The robot modulates communication strength through confidence-aware adaptive authority allocation by providing assertive legible assistive actions when confident while increasing user authority when uncertain, transforming shared autonomy into transparent bidirectional collaboration. User studies including 2D simulation and physical six degree-of-freedom robot arm experiments demonstrate that legible shared autonomy significantly improves users' understanding of robot beliefs and reduces user control effort compared to standard shared autonomy. 

---

## Experimental Setup

<p align="center">
  <img src="figures/experimental_setup.png" alt="Experimental Setup" width="700"/>
</p>

**Design:** Within-subjects study with 20 participants

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
    <td align="center"><img src="trajectory_animations/participant_dong_trajectories.gif" width="200"/><br><sub>Participant 8</sub></td>
    <td align="center"><img src="trajectory_animations/participant_gong_trajectories.gif" width="200"/><br><sub>Participant 9</sub></td>
    <td align="center"><img src="trajectory_animations/participant_shuxian_trajectories.gif" width="200"/><br><sub>Participant 14</sub></td>
    <td align="center"><img src="trajectory_animations/participant_sun_trajectories.gif" width="200"/><br><sub>Participant 16</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="trajectory_animations/participant_wangchao_trajectories.gif" width="200"/><br><sub>Participant 17</sub></td>
    <td align="center"><img src="trajectory_animations/participant_wangqi_trajectories.gif" width="200"/><br><sub>Participant 18</sub></td>
    <td align="center"><img src="trajectory_animations/participant_xing_trajectories.gif" width="200"/><br><sub>Participant 19</sub></td>
    <td align="center"><img src="trajectory_animations/participant_zhang_trajectories.gif" width="200"/><br><sub>Participant 20</sub></td>
  </tr>
</table>

---

## Main Results

<p align="center">
  <img src="figures/combined_figure.png" alt="Results" width="900"/>
</p>

**Transparency Metrics:**
- Understanding rate: 38% → 96-99% (Standard SA → Legible)
- Statistical significance: χ²(2) = 136.33, p < 0.001
- Prediction accuracy: 54% → 96-99%
- Statistical significance: χ²(2) = 89.72, p < 0.001

**Subjective Experience:**
- Intuitiveness ratings: 3.90 → 8.35 (1-10 scale)
- Collaboration ratings: 4.25 → 7.00
- Strong correlation between measures: r = 0.66, p < 0.001

**User Effort (Panel d):**
- Mean user input norm: λ=0: 8.92 ± 7.71 → λ=5: 4.25 ± 4.60 → λ=10: 3.53 ± 3.51
- Legible motion reduces user effort by 52% (λ=5) and 60% (λ=10) vs. standard SA
- Overall effect: Kruskal-Wallis H(2) = 30.68, p < 0.001
- Pairwise tests (Bonferroni-corrected): λ=0 vs λ=5: p < 0.001 \*\*\*, λ=0 vs λ=10: p < 0.001 \*\*\*, λ=5 vs λ=10: p = 1.000 (ns)
- Both legible conditions significantly outperform standard SA; no significant difference between the two legibility levels

---

## Installation

```bash
git clone <your-repo-url>
cd legible_autonomy
python -m pip install numpy pygame matplotlib pandas scipy pillow
```

## Reproduce

### Run the experiment

```bash
python experiment_collection.py
```

### Reproduce the main analysis figure

```bash
python analyze_data.py --input ./experiment_data --output ./figures
```

## Main files

- `experiment_collection.py` - interactive experiment
- `analyze_data.py` - statistical analysis and main figure
- `core/shared_autonomy.py` - shared-autonomy policy
- `core/legibility.py` - legibility objective

## Note

Pre-generated figures and trajectory animations are already included in the repository, so you can inspect the results directly without rerunning the full pipeline.
