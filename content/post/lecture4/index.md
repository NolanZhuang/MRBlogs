---
title: "Lecture Homework 4: Final Presentation"
date: 2026-02-09
weight: 4
author: Yan Zhuang
draft: false
---

## Introduction

This blog post presents the final design and evaluation of a VR locomotion technique inspired by the core interaction of **Angry Birds**. The goal of this project was to explore an alternative, physics-inspired approach to locomotion that emphasizes direct manipulation, player agency, and playful experimentation.

---

## 1. Design Ideation: Angry Birds as Inspiration

The initial idea for this locomotion system was inspired by the familiar *pull-and-release* mechanic from **Angry Birds**.

Instead of traditional joystick-based movement, locomotion is driven by:
- Stretching (pulling) an object  
- Releasing it to generate motion  

This metaphor was chosen because it is:
- Intuitive and playful  
- Closely tied to physical action  
- Easy to understand without complex instructions  

---

## 2. Implementation Overview

### Interactive Objects
Several interactive objects (white spheres) are placed throughout the scene. These objects act as locomotion anchors.

### Locomotion Mechanics
- Players can **grab and pull** an object to build up speed  
- **Pulling distance** determines the *magnitude* of the speed  
- **Head/gaze direction** determines the *direction* of movement  

Additional behaviors include:
- Looking upward beyond a certain angle allows **diagonal upward movement**, enabling jumping  
- While moving, if the player grabs another object, movement **immediately stops** next to it  
- When no interaction occurs, movement speed **gradually decreases**, preventing abrupt stops  

This creates a locomotion system that blends physics-based motion with embodied interaction.

---

## 3. Design Challenges

While the interaction was engaging, several challenges emerged during development.

### Direction Mapping
A major design question was:
- Should the movement direction follow the **pull direction**, or the **player’s viewing direction**?

Using gaze direction improved spatial awareness but also increased cognitive load.

### Control Difficulty
Participants reported that:
- The system was **very hard to control**, especially for precise navigation  
- Small differences in pulling distance or object placement had large effects on movement  

These challenges highlight the trade-off between expressive control and usability.

---

## 4. Evaluation Method

A small user study was conducted to evaluate the system with multiple users.

### Participants
- **3 participants**  
  - 2 male, 1 female  
  - Average age: **25.3 years**  
  - All had prior VR experience  

Each participant completed the same task using the locomotion technique, and results were averaged.

---

## 5. Results

### Objective Metrics
- **Average time per round:** **581 seconds**  
- **Average accuracy per round:** **63.7 / 68**  

### Subjective Metrics (1–10 scale)
- **Motion sickness:** **4**  
- **Task workload:** **8.3**  
- **Presence:** **7.7**  
- **Enjoyment:** **7**  

---

## 6. Discussion

The results suggest a clear pattern:

- **Low motion sickness** indicates that gradual acceleration and deceleration helped maintain comfort  
- **High workload** reflects the system’s demand for precision and continuous attention  
- **Strong presence and enjoyment** show that players felt immersed and engaged despite the difficulty  

A consistent qualitative takeaway was:

> **“Enjoyable but quite hard to master.”**

Performance was also **strongly influenced by the size and placement of interactive objects**, emphasizing how critical spatial layout is in object-driven locomotion systems.

---

## 7. Conclusion and Future Work

This Angry Birds–inspired locomotion technique demonstrates that:
- Physics-based, object-driven movement can be highly engaging  
- Increased player agency often comes with higher cognitive and physical demands  
- Careful tuning is essential to balance expressiveness and control  

Potential future improvements include:
- Adaptive scaling of pulling strength  
- Visual previews of movement trajectories  
- Improved object placement and spacing guidelines  

Overall, this project shows that unconventional locomotion metaphors can offer compelling alternatives to standard VR movement techniques—especially when exploration and playfulness are key design goals.

You can find the slides in the following address:
[Final Presentation](https://docs.google.com/presentation/d/1y8KI89u7LLW6RgMuevrOSQLwFNj6Cqqm/edit?usp=drive_link&ouid=105344196558666390232&rtpof=true&sd=true)
