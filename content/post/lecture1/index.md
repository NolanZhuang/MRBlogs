---
title: "Lecture Homework 1: Sketch and present 3 ideas for Locomotion in VR"
slug: "lecture1"
url: "/post/lecture1/"
date: 2025-12-09
weight: 1
author: Yan Zhuang
draft: false
---

## Background

In the scenario, the user starts in a **ground view** with the nearby environment visible. At some point, they want to see something far away, so they need to move to a **sky view** (a higher vantage point) to observe a larger area. A key constraint in this scenario is that **the movement is passive**: the system moves the user rather than the user actively walking/joysticking.

This is an interesting locomotion problem in VR because passive motion can easily increase discomfort and reduce spatial understanding. The slides propose three techniques to handle this “ground → sky” transition, each with different trade-offs.

A ground view may look like:

![Ground View](ground.png)

A sky view may look like:

![Sky View](sky.png)

---

## Technique 1: Suddenly Jump

**Idea:** No continuous motion is shown. The experience is segmented by fades.

**How it works (from the slides):**
1. The ground view **fades to black**.
2. The view stays **totally black** briefly.
3. The black view **fades back in** to the sky view.
4. The user never sees motion between start and end (“No movement”).

**Why it might help:**  
Because the user does not visually experience motion, the visual-vestibular mismatch is reduced, which can improve comfort for some users.

**Main limitation:**  
The user loses all motion cues. This can weaken spatial awareness (e.g., “Where did I come from?”) and make the transition feel like a teleport cut.

---

## Technique 2: Bystander

**Idea:** The user remains stationary, but watches an **avatar** travel along the path first, so the system can “explain” the movement before switching viewpoints.

**How it works (from the slides):**
1. The user stays in the ground view and watches an animation of an avatar (yellow capsule) moving along a trajectory (red line).
2. The avatar starts from the user’s position and travels to the end point.  
   This implies: “you are the avatar and you will move along this trajectory.”
3. When the animation ends, the view **fades to black** and then **fades in** to the sky view (still “No movement” experienced by the user directly).

**Why it might help:**  
It provides **path information** (trajectory and direction) without forcing the user to visually experience continuous self-motion. This can preserve spatial understanding better than a pure jump.

**Main limitation:**  
The user still does not feel/see themselves moving. Also, the technique depends on users correctly interpreting the avatar as “me.”

The following image is a screen shot during Bystander method:

![Bystander](bystander.png)

---

## Technique 3: Tunnel Vision

**Idea:** Show continuous motion, but reduce discomfort by limiting motion to a smaller central area while keeping the periphery stable.

**How it works (from the slides):**
1. The user experiences the movement from ground to sky.
2. A **tunnel opens at the center** of the view. The user can only see the motion inside this tunnel.
3. The **outer part** of the view stays static and continues showing the ground view.
4. When movement ends, the outer part of the tunnel **fades out**, revealing the full sky view.

**Why it might help:**  
This technique reduces motion sickness by stabilizing peripheral vision (a common comfort strategy). At the same time, it preserves some **continuous motion cues**, which can support orientation.

**Main limitation:**  
It can feel visually artificial, and it may reduce situational awareness during the transition because the user’s effective field of view is temporarily restricted.

The following image is a screen shot during Tunnel Vision method:

![Tunnel](tunnel.png)

---

## Evaluation (How to Compare the Techniques)

The slides propose evaluating these techniques with both objective and subjective measures.

### Task-based spatial measure
After the user reaches the end point (sky view), ask them to **find out the start point** (where they came from).  
This tests whether the locomotion method preserves the user’s spatial understanding of the environment and the path taken.

### Objective metric
- **Task completion time**: how long it takes to identify/return to the start point (or indicate it correctly).

### Subjective metric
- **Questionnaire**: collect comfort and preference feedback (e.g., nausea, dizziness, perceived control, clarity of movement).

You can find the slides in the following address:
[3 Locomotion Techniques](https://docs.google.com/presentation/d/1RqtAztxM7Qlg1F_CP0Eo_1WcrRcRL1hB/edit?usp=drive_link&ouid=105344196558666390232&rtpof=true&sd=true)
