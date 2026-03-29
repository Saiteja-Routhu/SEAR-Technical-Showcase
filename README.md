# SEAR-Technical-Showcase
# 🔥 SEAR: Physics-Based Brawler
[cite_start]**A hyper-kinetic first-person predator game where momentum generates heat, heat generates power, and stopping means death.** [cite: 7, 8]

[cite_start]**Role:** Lead Technical Developer (Solo) [cite: 4, 44]  
[cite_start]**Engine:** Unreal Engine 5.5 (Blueprints) [cite: 3, 39]  
[cite_start]**External Tools:** Python (Automated QA), Blender (Procedural IK topology) [cite: 554, 597]  

---

## 📌 Project Overview
SEAR is a vertical-slice technical showcase built to demonstrate rigorous systems architecture, modular visual scripting, and automated QA pipelines. [cite_start]The core mechanic replaces standard FPS movement with direct, independent control of asymmetrical mechanical legs via an impulse-momentum physics framework[cite: 44, 67, 143].

This repository documents the Blueprint architecture, Finite State Machine (FSM) logic, and Python-driven testing protocols used to build and stabilize the game.

## ⚙️ Technical Architecture

To prevent visual scripting spaghetti, SEAR relies on a strictly decoupled Actor Component architecture communicating via Blueprint Interfaces.

### Core Components
* `BP_KineticCharacter`: The host class. [cite_start]Owns the FSM Enum and Enhanced Input bindings[cite: 545].
* [cite_start]`AC_ParkourMovement`: Handles wall-run raycasts, stiction detection, Surface Normal reads, and Slingshot compression math[cite: 545].
* [cite_start]`AC_KineticDynamo`: Manages the Redline gauge, Friction Forging energy accumulation, Overheat logic, and procedural music layer triggers[cite: 545].
* [cite_start]`AC_LegLeft` / `AC_LegRight`: Manages independent leg physics variables (mass, friction coefficient) and strike logic[cite: 545].

### Locomotion Physics
[cite_start]Wall-running is not a toggle; it is a physics consequence of velocity[cite: 90]. 
* [cite_start]**Friction Economy:** $F_{friction} = \mu \cdot F_N \ge mg$ [cite: 93]
* [cite_start]**Vector Combat:** Every kick utilizes the Impulse-Momentum Theorem ($J = F \cdot \Delta t = m \cdot \Delta v$) combined with Newton's Third Law to calculate recoil and trajectory[cite: 144, 146, 147].

---

## 🧠 AI & State Management

### 12-State FSM
All movement and combat are strictly governed by `EKineticPlayerState` to ensure clean transitions at high velocities. Key states include:
* `Wall_Running`: Gravity counteracted by friction; [cite_start]Forging active[cite: 547].
* [cite_start]`Anchored_Left` / `Anchored_Right`: Single-leg surface locking[cite: 547].
* [cite_start]`Suspended_SloMo`: Movement halted; kinetic energy compresses into potential energy ($PE = \frac{1}{2}mv^2$)[cite: 132, 547].

### RL-Principled Behavior Trees
[cite_start]Enemies utilize Behavior Trees and Environment Query Systems (EQS) designed with Reinforcement Learning principles[cite: 187]. [cite_start]They maintain lightweight session logs of the player's vector trajectories to adapt positioning and dodge probabilities in real-time, providing predictive AI without the overhead of full ML inference[cite: 188, 189, 193].

---

## 🤖 Automated QA Pipeline

[cite_start]Manual testing is insufficient for a physics-based wall-running system[cite: 595]. SEAR utilizes a custom automated testing pipeline:
* [cite_start]**Headless Python Agents:** Bots run 24/7 stress tests specifically targeting collision holes within wall-running logic and brutalist geometry[cite: 596, 598].
* [cite_start]**Jira Integration:** Upon successful geometry clipping or physics failure, the Python script auto-generates a Jira ticket containing the level name, coordinates, velocity at failure, and reproduction steps for immediate regression testing[cite: 600].

---
*Note: This repository serves as technical documentation and architectural proof-of-concept. Proprietary game assets and compiled binaries are not hosted publicly.*
