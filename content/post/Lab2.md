---
title: "Lab Homework 2: Setup Unity"
date: 2025-12-01
weight: 6
author: Yan Zhuang
draft: false
---

## What I was trying to do

My goal was to set up **Unity 6 (6000.0.60f1)** and follow Unity’s beginner workflow to build a **simple first 3D scene**: a ground plane, a few objects, basic lighting, and a camera view that looks “game-like” when I press Play.

I treated it like a small checklist: **install → create project → build scene → press Play → save**.

---

## How I approached the task

### 1 Install Unity 6 (6000.0.60f1) via Unity Hub
- Installed **Unity Hub**
- In Hub → **Installs** → **Install Editor**
- Selected **6000.0.60f1**
- Included:
  - **Microsoft Visual Studio** (for C# scripting later)
  - Any platform modules I might need later (Android/WebGL/etc.)

---

### 2 Create a new 3D project
In Unity Hub → **Projects** → **New Project**:
- Template: **Universal 3D**
- Project name: something like `MyFirst3DScene`
- Location: a folder you can easily find again (I put it on D:\)

When Unity opened, I checked the basic panels:
- **Hierarchy** (what’s in the scene)
- **Scene view** (edit world)
- **Game view** (what the player sees)
- **Inspector** (edit selected object)

---

## Building my first 3D scene

### 1 Create a ground
- Hierarchy → Right-click → **3D Object → Plane**
- Renamed it to `Ground`
- Reset Transform (Inspector → three dots menu → **Reset**), then adjusted scale if needed

### 2 Add a few objects (so it doesn’t look empty)
- **3D Object → Cube** → renamed `Box`
- **3D Object → Sphere** → renamed `Ball`
- Moved them up on Y so they sit above the ground (e.g., Y = 0.5 for cube)

### 3 Add simple materials (optional but makes it clearer)
- Project window → Right-click → **Create → Material**
- Created `Mat_Ground`, `Mat_Box`, `Mat_Ball`
- Dragged materials onto objects in the Scene view
- Adjusted color in Inspector

### 4 Lighting check
Most 3D templates already include a **Directional Light**.
- Selected `Directional Light`
- Rotated it slightly so shadows look nice and the scene has depth

### 5 Camera framing
Most templates already include a `Main Camera`.
- Moved the camera to a simple angle (slightly above and looking down at the objects)
- Pressed **Play** to check what the scene looks like in Game view
- Exited Play mode and adjusted again if needed

---

## Saving the scene (the part I almost skipped)
This sounds obvious, but it’s easy to forget when you’re new.

- File → **Save** (or Save As…)
- Created a folder: `Assets/Scenes/`
- Saved as: `Main.unity`

If the project later has multiple scenes, saving them in `Assets/Scenes/` keeps things organized.

---

## What I wish I knew at the start

1) **Hierarchy is the truth.**  
If something is “missing,” it’s usually either disabled, moved far away, or the camera isn’t looking at it.

2) **Scene view vs Game view are different.**  
Scene view is for editing; Game view is what the camera shows.

3) **Name and organize early.**  
Renaming `Cube` to `PlayerBox` (or similar) and putting scenes in `Assets/Scenes/` prevents confusion later.

---

## Conclusion

Getting Unity installed was straightforward, but the biggest learning came from understanding the editor workflow:
**create objects → place them with transforms → check lighting/camera → press Play → save the scene**.

Now that I have a working “first 3D scene,” the next step is adding interaction (simple movement or physics) — but even this basic setup already makes Unity feel much less intimidating.
