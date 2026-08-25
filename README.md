# Reinforcement Learning-Based Autonomous Rocket Landing

An end-to-end continuous control reinforcement learning system designing dynamic guidance algorithms for vertical booster landing within custom physics environments.

## Overview
Autonomous vertical landing of reusable rocket boosters is a high-dimensional, non-linear continuous control problem. This project formulates a custom 2D Gymnasium environment (`RocketLanding-v0`) and trains Deep Q-Networks (DQN) and Deep Deterministic Policy Gradient (DDPG) agents to learn thrust and vectoring policies from raw state feedback.

---

## Markov Decision Process (MDP) Formulation

* **State Space ($S \in \mathbb{R}^6$)**:
  * Horizontal Position ($x$) and Vertical Position ($y$)
  * Linear Velocities ($\dot{x}, \dot{y}$)
  * Tilt Angle ($\theta$) and Angular Velocity ($\dot{\theta}$)
* **Action Space ($A$)**:
  * Continuous main thruster throttle ($0\%$ to $100\%$)
  * Lateral orientation/gimbal thruster commands
* **Reward Engineering**:
  * Positive reward for soft touchdown within target landing pad coordinates ($v \le v_{\text{max}}$, $\theta \approx 0$).
  * Dense penalties for altitude descent rate, tilt magnitude, angular acceleration, and fuel consumption.

---

## System Pipeline
```text
[Gymnasium Kinematics Env] 
       ↓
[MDP & Reward Formulation] 
       ↓
[DQN / DDPG Policy Training] 
       ↓
[Policy Evaluation & Convergence Logging] 
       ↓
[ONNX Model Export] 
       ↓
[Client-Side ONNX Runtime Web App]
