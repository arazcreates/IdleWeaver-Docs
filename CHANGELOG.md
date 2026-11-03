# Changelog

## 1.8.1 (2026-11-03)

- Idle Weaver nodes in an Animation Blueprint now work in Play > Standalone Game. Before, the character showed the reference pose there.
- New **Follow Live** option on Gaze Target components and **Follow Tagged Actors Live** in Gaze Targeting, for targets that move. Both are off by default.
- Set Gaze Target Actor on a plain actor now aims at the center of its bounds, not 60 cm above its origin.
- MetaHuman eyes: the Eyes node goes at the end of the face's post-process Animation Blueprint, after RigLogic. See Path C.

## 1.8.0 (2026-10-14)

- A fixed seed now gives the same motion at any camera distance.
- Detail level changes fade over 0.4 seconds instead of popping.
- A Profile's Default Context now applies, and Set Idle Paused also stops the Pose Library.
- The Idle Pose Library node reads the component. Plain Skeletal Mesh Actors look where their mesh faces.
- Shoulder Offset now moves the right way, so check it if you tuned around the old direction.
- New: Set Motion LOD Override, plus Blueprint children of the Idle Weaver and Gaze Target components.

## 1.7.2 and 1.7.1 (2026-10-05, 2026-10-04)

Packaging for Fab. The code didn't change.

## 1.7.0 (2026-09-14)

- Head and eye aim fixed on turned heads, and Head Tilt no longer shifts the aim.
- Runtime changes to the Pose Library, Profile and Preset now take effect at once.
- Baking no longer resets a live NPC, and it works outside Play mode.
- All players count as gaze targets, and detail levels use the nearest camera.
- The main node no longer allocates memory each frame.

## 1.6.0 (2026-08-23)

MetaHuman and multi-mesh support: Target Mesh Component and the Idle Weaver Eyes node.

## 1.5.0 (2026-08-23)

Everything public now works from Blueprint and C++.

## 1.4.0 (2026-07-06)

Limb Swing gets Shoulder Offset and Limit Inward Swing.

## 1.3.0 (2026-07-06)

Four optional features: Head Tilt, Body Style, Hip Sway and Limb Swing.

## 1.2.0 (2026-07-06)

The Pose Library skips additive clips by default.

## 1.1.0 (2026-07-06)

Tag-based gaze targets and separate gaze ranges.

## 1.0.0 (2026-07-06)

First release.
