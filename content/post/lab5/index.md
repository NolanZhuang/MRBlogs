---
title: "Lab Homework 5: Locomotion technique Implementation"
slug: "lab5"
date: 2026-02-09
weight: 9
author: Yan Zhuang
draft: false
---

## Introduction

In this blog post, I describe my implementation of locomotion technique. The idea originated from the game Angry Birds, where players can pull a slingshot in different directions and with different force to send birds flying in different trajectories to attack enemies. In my locomotion technique, the difference is player do not send birds flying anymore, instead, they send themselves. The goal of this project is to create an immersive and enjoyable VR experience.

![Angry Birds](birds.png)


---

## How I Approached the Task

I implemented my project step by step. My workflow was:

1. Set up the scene and player.
2. Create interactive object prefab.
3. Implement the core locomotion mechanism.
4. Test with different parameters and interactive object placements.

---

## Scene and Player Setup

I kept the original scene setup and made sure they have colliders to support correct collision with player.

### Player
- Enable **Use Gravity** and disable **Is Kinematic** in **Rigidbody** to ensure it will fall naturally due to gravity.
- Froze rotation of the player.
- Added **Box Collider** components to left and right hands to enable collision detection with interactive objects.

---

## Interactive object prefab creation

Interactive objects primarily serve two functions: one is to detect whether the player's controller is within the object's range, and the other is to highlight the object when the player's controller is within the object's range. For simplicity, I used a white sphere as the appearance of the interactive object, without adding any special shapes or materials.

To achieve the first function, I added a **Sphere Collider** component to the object and used collision detection to determine whether the player's controllers is within the object's range. Meanwhile, I enabled **Is Trigger** within **Sphere Collider** to avoid the impact of realistic collisions on player movement.

To achieve the second function, I wrote a simple code. When a collision is detected, it will replace the color of the object's current material with a different one to achieve a simple highlight effect. (Although the final version has not yet been integrated and used)

```csharp
public void SetHighlight(bool highlight)
{
    if (rend == null) return;

    isHighlighted = highlight;
    if (highlight)
    {
        rend.material.color = Color.yellow;
    }
    else
    {
        rend.material = originalMaterial;
    }
}
```

---

## Locomotion Implementation

This project uses a **hand-pull + release-boost** locomotion technique for VR. The idea is simple: when the player holds the **index trigger** near a interactive object, they “grab” and move themselves by pulling their hand. When they release the trigger after a sufficiently large pull, they get a short **boost** in the direction they are looking.

---

### 1 Trigger-gated grabbing (entering locomotion mode)

Locomotion only activates when the index trigger is pressed strongly and the hand is close to a valid surface. This avoids accidental movement when the player is just gesturing.

---

### 2 Pull locomotion = move player opposite to hand motion (with jitter deadzone)

Once pulling starts, the code computes the hand’s per-frame displacement and moves the player in the **opposite direction** (like pulling on a rope). A small deadzone filters controller jitter.

```csharp
Vector3 frameMovement = currentWorldPos - leftHandLastWorldPos;

if (frameMovement.magnitude > movementDeadzone)
{
    transform.position += -frameMovement;
    leftHandLastWorldPos = currentWorldPos;
}
```

**Key parameter:**  
- `movementDeadzone` (default ~0.01 m) ignores tiny hand motion (tracking noise).  
  - **Higher** = steadier but less responsive  
  - **Lower** = more responsive but may jitter

---

### 3 Net pull distance = intent detection for boost

To decide whether a “pull” is strong enough to deserve a boost, the script tracks the **net displacement** from pull start to release (not just small per-frame motion).

```csharp
Vector3 totalMovement = finalWorldPos - leftPullStartPos;
float finalNetDistance = totalMovement.magnitude;

if (finalNetDistance >= minPullDistance)
{
    TriggerBoost(finalNetDistance, "Left");
}
```

**Key parameter:**  
- `minPullDistance` (e.g., 0.08 m) prevents micro-pulls from triggering boosts.  
  - **Higher** = fewer accidental boosts  
  - **Lower** = easier to boost

---

### 4 Boost direction = HMD forward, with vertical comfort limits

Boosting uses the **HMD forward vector** so movement is head-relative (the user goes where they look). Vertical motion is constrained to avoid uncomfortable upward/downward acceleration. Only when the head-up angle exceeds a threshold **verticalAngleLimit** will vertical boost occur, resulting in a jumping effect.

```csharp
Vector3 lookDirection = hmd.transform.forward;

float verticalAngle = Vector3.Angle(lookDirection, Vector3.up);
if (verticalAngle > (90 - verticalAngleLimit) &&
    verticalAngle < (90 + verticalAngleLimit))
{
    lookDirection.y = 0;
    lookDirection.Normalize();
}
else if (lookDirection.y < 0)
{
    lookDirection.y = 0;
    lookDirection.Normalize();
}
```

**Key parameter:**  
- `verticalAngleLimit` controls the minimum head-up angle required for the jump.

---

### 5 Boost strength and duration (tuning speed vs comfort)

The boost speed scales with how far the hand was pulled, then runs for a limited duration.

```csharp
float distanceFactor = Mathf.Clamp01(netPullDistance / 0.5f);
float boostSpeed = distanceFactor * maxBoostSpeed;

boostTimer = boostDuration;
currentVelocity = lookDirection * boostSpeed;
```

**Key parameters:**
- `maxBoostSpeed`: upper limit of boost speed (comfort-critical; too high can cause sickness)
- `boostDuration`: how long the boost lasts (shorter feels snappier; longer feels like gliding)
- `maxSlideDistance`: safety limit so the player can’t drift too far while “grabbing”

In practice, these parameters are the main comfort/feel controls: I tuned them by repeatedly testing in headset and looking for sudden acceleration or loss of spatial stability.

### 6 Natural speed decay (friction-like slowdown)

To avoid the player sliding forever after a boost, velocity decays smoothly toward zero when the system is **not boosting** and **not currently pulling**. In the code, this is implemented with a `Lerp` toward `Vector3.zero`:

```csharp
if (!isBoosting && !leftHandPulling && !rightHandPulling)
{
    currentVelocity = Vector3.Lerp(currentVelocity, Vector3.zero, 3f * Time.deltaTime);
}
```

This behaves like a simple “air friction” model:
- movement gradually slows down,
- there is no sudden stop,
- comfort is improved because acceleration changes are smoother.

### 7 Sudden grab stop (safety brake while grabbing)

When the player starts pulling (grabbing) with a hand, the code immediately clears any residual velocity so the player does not keep moving while trying to interact.

Then, during grabbing, the system applies a stronger deceleration to quickly remove any remaining motion:

```csharp
if (isLeftGrabbing || isRightGrabbing)
{
    currentVelocity = Vector3.Lerp(currentVelocity, Vector3.zero, 10f * Time.deltaTime);

    if (currentVelocity.magnitude < 0.1f)
        currentVelocity = Vector3.zero;
}
```

This “safety brake” is important in VR because:
- it keeps interaction stable (hands and target don’t drift away),
- it reduces unexpected motion while the player is focused on grabbing,
- it helps prevent motion discomfort caused by sliding during close-range interaction.

---

## Testing

In this part, I mainly tested the placement of interactive objects and 2 parameters `maxBoostSpeed` and `boostDuration` which are most related to the feeling during motion.

The principle for placing interactive objects is to ensure that the player can collect every coin. Since movement cannot turn after releasing the object, each coin should be on a straight line formed by connecting two interactive objects.

The most direct impression `maxBoostSpeed` and `boostDuration` give is the speed and the distance they glide after release the interactive object. The higher these values, the faster the speed, the farther the gliding distance, and the more difficult the movement is to control. When their values ​​are too small, it will prevent the player from reaching the location of the next interactive object.

Here is the final parameter set that gives best experience during the testing:

`maxSlideDistance`: 1

`maxBoostSpeed`: 25

`boostDuration`: 1.36

`verticalAngleLimit`: 25

`minPullDistance`: 0.08

`movementDeadzone`: 0.01

The following screenshot shows placement of interactive object (each white point indicates an interactive object):

![Scene](scene.png)

---

## Conclusion

This locomotion implementation combines **hand-driven pulling**, **intent-based boost activation**, and **head-relative movement**. By exposing parameters such as deadzones, pull thresholds, boost speed, duration, and slide limits, the system can be tuned to balance responsiveness and VR comfort.

You can find the codes in the following address:
[GitHub Link](https://github.com/NolanZhuang/HCIforMR-Project.git)

You can also find a demo video here:
[Video Link](https://drive.google.com/file/d/1Q2BJi5lyBd-Z02vhqvaSzt-UrtpZypQe/view?usp=drive_link)
