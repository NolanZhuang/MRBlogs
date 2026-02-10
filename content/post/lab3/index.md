---
title: "Lab Homework 3: Unity Roll-A-Ball"
slug: "lab3"
url: "/post/lab3/"
date: 2025-12-17
weight: 7
author: Yan Zhuang
draft: false
---

## Introduction

In this blog post, I describe my experience implementing Unity’s official beginner tutorial **Roll-a-Ball**. The goal of the task is to build a small 3D game where the player controls a rolling ball, collects pickups, and tracks a score. This task helped me understand core Unity concepts such as physics, scripting, input, and UI.

---

## How I Approached the Task

I followed the tutorial step by step and focused on understanding *why* each component was added rather than only copying instructions. My workflow was:

1. Set up the scene and core GameObjects.
2. Add player movement using physics.
3. Implement collectible objects.
4. Add UI elements to display the score.
5. Test and refine the gameplay.

---

## Scene Setup

I started with a new **3D project** in Unity.

### Environment
- Created a **Plane** and named it `Ground`.
- Added a **Sphere** to act as the player and named it `Player`.
- Added a **Rigidbody** component to the player so it could interact with physics.
- Froze rotation on the X and Z axes to keep the ball from tipping over.

### Pickups
- Created a **Cube**, resized it, and named it `Pickup`.
- Positioned it slightly above the ground.
- Duplicated it multiple times across the plane.

The following screenshot shows the overall setup:

![Scene Overview](scene.png)

---

## Player Movement Script

To move the player, I created a C# script and attached it to the Player object.

```csharp
void OnMove(InputValue movementValue)
{
    Vector2 movementVector = movementValue.Get<Vector2>();
    movementX = movementVector.x;
    movementY = movementVector.y;
}

void FixedUpdate()
{
    rb.AddForce(new Vector3(movementX, 0.0f, movementY) * speed);
}
```

Using `FixedUpdate()` ensured that movement was consistent with Unity’s physics system.

The following screenshot shows the player inspector:

![Player Inspector](player.png)

---

## Collecting Pickups

To detect when the player touched a pickup, I used trigger colliders.

- Marked each Pickup’s Box Collider as **Is Trigger**.
- Added a script to the Player that detects collisions and disables the pickup object.

This made pickups disappear when collected and prepared the logic for scoring.

---

## Score UI

I added a simple UI system:
- Created a **Canvas**
- Added a **Text** element to display the score

A script updated the score whenever a pickup was collected.

The following screenshot shows the Score UI:

![Count](play.png)

---

## Problems I Encountered

### Objects Falling Through the Floor
Some pickups fell through the ground.

**Cause:**  
The Ground object did not have a collider.

**Solution:**  
Ensuring the Plane had a Collider component solved this issue.

---

## What I Learned

- Physics-based movement should use `Rigidbody` and `FixedUpdate()`.
- Unity scenes depend heavily on correct component setup.
- Naming and organizing GameObjects early makes debugging much easier.
- UI requires both visual elements (Canvas/Text) and scripts to update values.

---

## Conclusion

The Roll-a-Ball tutorial provided a strong foundation for understanding Unity’s workflow. By completing this task, I gained confidence working with physics, scripts, and UI. This experience made Unity feel more approachable and prepared me for building more complex interactive tasks in the future.
