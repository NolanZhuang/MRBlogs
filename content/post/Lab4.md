---
title: "Lab Homework 4: Unity Roll-A-Ball in VR"
slug: "lab4"
date: 2025-12-22
weight: 8
author: Yan Zhuang
draft: false
---

## Introduction

After completing the classic **Roll-a-Ball** Unity tutorial, the next step was to upgrade the project into a **VR** experience. Using the workflow provided in the course slides, I transformed the original desktop-based game into an immersive VR application where the player can interact with the Roll-a-Ball scene using VR controllers.

---

## How I Approached the Task

Rather than rebuilding everything from scratch, I reused as much of the original Roll-a-Ball project as possible. My approach was:

1. Export the existing Roll-a-Ball project as a Unity package.
2. Import it into a new VR-enabled Unity project.
3. Set up VR essentials such as the camera rig and controller tracking.
4. Rebuild the scene layout for VR scale and interaction.
5. Replace keyboard input with VR controller input.

---

## Exporting and Importing the Roll-a-Ball Project

I exported the original project using **Assets → Export Package**, selecting all scenes, scripts, and prefabs.  
In the VR project, I used **Assets → Import Package → Custom Package** to bring everything back in.

### Problem Encountered
After importing, Unity reported script errors due to a naming conflict between `PlayerController.cs` and scripts included with the VR integration.

### Solution
I resolved this by renaming the Roll-a-Ball player controller script and removing unused keyboard input code.

---

## Creating a VR Scene

To make the game comfortable in VR:

- I deleted the default `Main Camera`
- Created a large floor plane for VR
- Added a cube as a table
- Used an empty GameObject to organize static objects

---

## Adding the VR Camera Rig

I added an **OVRCameraRig** using Meta XR Tools and ensured it replaced the default camera. This enabled head tracking in VR.

---

## Controller Tracking and Interaction

Controller tracking was added as a building block and attached to the left and right controller anchors.  
The **index trigger** was used as the primary input:

- Trigger press selects the Roll-a-Ball board
- Trigger release drops it

This interaction was implemented using trigger colliders and `OnTriggerEnter()` logic.

---

## Updating UI for VR

The original 2D UI was converted to **World Space UI**:

- Canvas render mode set to *World Space*
- TextMeshPro used for score and win text
- UI positioned inside the 3D scene

---

## Problems and Lessons Learned

- VR scale must be adjusted carefully to avoid discomfort
- Keyboard input does not translate directly to VR
- Organizing imported assets prevents confusion

---

## Conclusion

Converting Roll-a-Ball into a VR project showed how existing Unity games can be extended into immersive experiences. This project strengthened my understanding of VR setup, controller input, and spatial UI design in Unity.