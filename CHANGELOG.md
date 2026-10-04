# Changelog

All notable changes to Idle Weaver are documented here.

## 1.7.2 — 2026-10-05

Packaging only. The code did not change.

- The plugin file now has a documentation link and a support address.
- The README has a new Support section.

## 1.7.1 — 2026-10-04

Packaging only. The code did not change.

- Each module now lists its supported platform (**Win64**) in the plugin file.
  Fab needs this to compile the plugin.
- The package now contains a `Content` folder, as Fab requires for code plugins.
  The folder is empty.

## 1.7.0 — 2026-09-14

A quality release after a full review of the code. It fixes aiming errors, makes
runtime changes take effect, and lowers the cost of large crowds. Nothing was
removed or renamed, and every optional feature is still off by default.

Fixed — aiming:

- **A turned head now looks up or down by the full angle.** Before, the pitch
  turned about the character's fixed side axis. A head turned 60 degrees toward
  a target 30 degrees below looked only about 15 degrees down.
- **Head Tilt no longer moves the aim.** The roll now turns about the direction
  the head faces. Before, a head that was turned and tilted aimed above or below
  its target.
- **The eyes land on the target.** The main node and the Idle Weaver Eyes node
  now pitch the eyes about the turned side axis.
- **Curiosity Tilt fires once for each new target.** It now reacts only when the
  NPC picks a different target. Before, a walking player or a turning NPC could
  fire it again on every frame.
- **Limb Swing no longer freezes.** With Sync To Hip Sway on, the arms stopped
  when distance LOD or a zero intensity paused Hip Sway. The arms now use their
  own rhythm while Hip Sway is not running.

Fixed — setup and runtime changes:

- **A Bone Mapping always applies.** If automatic detection found no pelvis and
  no head, the node stopped and never read the corrected mapping. It now reads
  the mapping on the next frame. Edits to a Bone Mapping also apply without a
  restart.
- **Runtime changes take effect.** On a mesh without an Animation Blueprint, a new
  Pose Library, Profile or Preset now applies at once. Before, the anim instance
  kept the values it got at Begin Play.
- **Target Mesh Component can change at runtime.** The component now finds the
  mesh again when the target changes.
- **The Pose Library node restarts cleanly.** When you swap the library or change
  a fixed seed, it starts a new anchor sequence. Before, it could play the wrong
  clip or hold the reference pose for several seconds. Looping anchors now blend
  from the last key back to the first key.
- The additive anchor warning now shows once for each clip, not once for each
  character.
- Other NPCs now aim at the head bone set in this NPC's Bone Mapping.
- Documentation for Crowd Mode and the LOD levels now matches what they do.

Fixed — baking:

- **Baking no longer breaks a live NPC.** In Play mode the bake re-created the
  anim instance, and the NPC lost its Pose Library and profile. The bake now
  samples from the current state and resets nothing.
- **Baking works outside Play mode.** On a mesh without an Animation Blueprint,
  the bake adds the idle anim instance for the duration of the bake. After the
  bake, the mesh gets its original settings back.
- Actor names with brackets or dots now make valid asset names.

Changed:

- **All human players count as gaze targets.** In split-screen and multiplayer,
  NPCs can look at any player, not only the first local player.
- **Distance LOD uses the nearest local camera.** In split-screen, each NPC uses
  the camera that is closest to it.
- **Lower crowd cost.** The micro-motion node no longer allocates memory on each
  frame. Bone names are now found on the game thread only.
- Bone detection now skips IK helper bones by word. A bone whose name only
  contains the letters "ik", such as "spike", is no longer skipped.
- All log messages now use the **LogIdleWeaver** category.
- **Load Preset** keeps Bone Mapping and the optional extras, and the
  documentation now says so. In the editor the action can be undone and marks
  the asset for a save.
- The README now covers every feature up to this version.

Added:

- **Get Gaze Target Serial.** A number that goes up each time the NPC picks a
  different gaze target. Compare it with the last value to find out that the NPC
  noticed something new.
- **Find Idle Weaver Component For Mesh.** Returns the component that drives a
  given mesh, or the first one on the actor.

## 1.6.0 — 2026-08-23

MetaHuman and multi-mesh character support. All three additions are optional and
change nothing for a single-mesh character.

Added:

- **Target Mesh Component** on the Idle Weaver component. Picks which skeletal
  mesh the component drives, from a dropdown. Leave it empty and the first
  skeletal mesh on the actor is used, exactly as before. Set it on characters
  built from several meshes — a MetaHuman, where you want Body rather than the
  face, clothing or hair that may be found first.
- **Idle Weaver Eyes** anim node. Aims the eyes at the current gaze target with
  saccades and micro-drift, for the case where the eyes are on a different mesh
  from the body. Put the normal node in the Body Animation Blueprint and this one
  in the Face Animation Blueprint; both read the same component, so there is one
  gaze decision and one seed and the eyes cannot disagree with the head. It reads
  the head's current facing from the pose, so it makes no assumption about which
  axis an eye bone points down.

Changed:

- Bone auto-detection now recognises **infix** side markers (`_L_`, `_R_`), as
  used by MetaHuman facial bones such as `FACIAL_L_Eye`. Suffix and prefix forms
  work as before.
- Auto-setup never installs an anim instance on a mesh driven by a **Leader Pose
  Component**, so it cannot disturb clothing that follows a body mesh. It logs
  which mesh it skipped.

## 1.5.0 — 2026-08-23

Blueprint and C++ parity pass. Every public feature is now reachable from
both. No behaviour changed, and nothing was removed or renamed.

Added — Blueprint access to the component's inspection API, which was C++ only:

- **Get Effective Profile.** The profile actually in effect: your assigned
  asset, or the transient one built from the preset.
- **Get Runtime Seed.** Read back the seed an NPC actually used, so you can
  reproduce motion you liked. Pairs with the existing `Reseed`.
- **Get Motion LOD / Set Motion LOD.** The camera-distance bucket, typed as
  `EIdleWeaverLOD` rather than the internal byte. Setting it pins an NPC for a
  frame or a cinematic; the subsystem reclaims it on its next LOD pass.
- **Get Gaze Target World**, **Get Head World Location**, **Resolve Mesh.**

Added — Blueprint access to the subsystem's spatial queries:

- **Get Idle Components Near**, **Get Gaze Targets Near**,
  **Get Actors With Tag Near.** The tag query keeps its per-tag cache, so it
  stays cheap from Blueprint too.

Added — profile authoring from Blueprint:

- **Load Preset** on `UIdleWeaverProfile`. Overwrites the profile in place
  with a preset's tuned values, as a starting point for hand-tuning or to
  build a profile at runtime. Also available as a button in the editor.

Changed:

- `BakeDuration` and `BakeFrameRate` are now `BlueprintReadWrite`, so a
  Blueprint batch-baking tool can set them per NPC.

## 1.4.0 — 2026-07-06

Added — two **optional** extras inside the (already optional) Limb Swing channel. Both default
to off, so enabling Limb Swing on its own behaves exactly as it did in 1.3.0. The existing arm
swing was not modified.

- **Shoulder pitch offset.** Carries the shoulders forward/back so the hands travel out of the
  plane of the legs. Five modes: **Opposed** (one forward, one back), **Both Forward**,
  **Both Back**, **Alternating** (swaps lead each cycle, reads like a gentle walk), and
  **Custom** (set each shoulder independently, any combination).
- **Inward swing limit.** Optionally caps how far the arms swing *inward* toward the body while
  leaving outward travel untouched — a tuning aid for wider meshes where the hands reach the
  thighs.

## 1.3.0 — 2026-07-06

Added — four new **optional** channels. Every one is OFF by default; with none of them enabled
the plugin behaves exactly as it did in 1.2.0. Nothing was replaced.

- **Head Tilt (roll).** A third head axis on top of the existing yaw/pitch aiming. Three
  independently selectable flavours: **Lean Into Gaze** (subtle roll toward what they're looking
  at), **Curiosity Tilt** (a bigger head-cant when locking onto a new point of interest), and
  **Idle Drift** (slow ambient cant). Enable any combination.
- **Body Style (Feminine / Masculine / Neutral).** Optional styling pass with a Strength slider.
  Neutral (default) changes nothing. Scales hip sway/roll, shoulder carriage, arm adduction,
  stance width and chest carriage — all fully tunable per style.
- **Hip Sway.** Rhythmic weight-shifting between the legs with lateral translation, roll and an
  optional hip **yaw**, plus a wobble control for the loose, drunk-like feel. Spine counter-rotation
  keeps the upper body settled.
- **Limb Swing.** Slight arm swing (and optional forearm follow-through) with a matching small
  **foot lift** on the unweighted leg, so the character rocks foot-to-foot. Can sync to the Hip
  Sway rhythm so hips, arms and feet move as one, or run on its own cycle.

## 1.2.0 — 2026-07-06

Added / Changed

- **Pose Library ignores additive animations by default.** Sampling an additive clip as a
  full-body pose collapses the skeleton, so additive anchors are now skipped and a warning is
  logged naming the clip. Power users who deliberately want additive clips can re-enable them
  with the new **Allow Additive Animations** toggle on the pose library asset.

## 1.1.0 — 2026-07-06

Added

- **Tag-based gaze targets.** NPCs now glance at any actor carrying a chosen tag when it comes
  within range — no component needed. Set `Look At Actors With Tag` on the Idle Weaver component's
  Gaze Targeting, then add that tag to a shop, banner, sign, fire, etc. (Actor Details -> Tags).
  They aim at the object's visual center. Cached per tag in the world subsystem, so it stays cheap
  with large crowds.
- **Per-type gaze ranges.** New `Player Search Radius` and `Tag Search Radius` let you set separate
  distances for looking at the player vs. tagged points of interest (0 = use the general Search Radius).

## 1.0.0 — 2026-07-06

Initial release.

- Layered micro-motion anim node: breathing, weight shifts, gaze/head tracking, hand fidgets, foot IK, and per-instance posture variation, each on its own seeded phase.
- Idle Pose Library anim node: blend and randomize transitions across your own anchor poses / idle loops.
- Drop-on `Idle Weaver` component with preset profiles (Villager, Guard, Merchant, Crowd, Exhausted, Nervous).
- Contextual modifiers: Tension / Energy / Temperature, plus automatic slope response from foot traces.
- Gaze targeting: player, other NPCs, points of interest, and ambient wander, with FOV limits, smooth spring-damped turns, and saccades.
- Foot IK ground conforming with rare reposition steps; pelvis slope adjustment.
- Performance: distance-based LOD buckets, crowd mode, and per-channel LOD caps.
- Any-humanoid-rig bone auto-detection (UE4/UE5 mannequin, Mixamo, Biped) with manual overrides and graceful degradation.
- Deterministic seeding for replays and cinematics.
- Bake to AnimSequence from the component.
- Verified compiling against Unreal Engine 5.8 (Win64, Development Editor).
