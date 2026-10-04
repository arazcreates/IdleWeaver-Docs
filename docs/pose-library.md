# Make a Pose Library

[Back to the main page](../README.md)

Idle Weaver adds motion on top of a pose. A Pose Library gives it that pose. Without one, a character that has no Animation Blueprint stands in its reference pose (an A-pose or a T-pose).

A Pose Library holds one or more **anchors**. An anchor is an idle animation or a single pose. The character holds one anchor for a while, then blends smoothly to another one.

## Create the asset

1. In the Content Browser, right-click an empty area.
2. Select **Miscellaneous > Data Asset**.
3. In the class list, select **Idle Weaver Pose Library**.
4. Give the asset a name, for example `PL_Villager`.
5. Open the asset.

## Add an anchor

1. Click **+** next to **Anchors**.
2. Open the new entry.
3. Set **Animation** to an idle animation that uses the same skeleton as your character.
4. Save the asset.

One anchor is enough to start. Add two to four for a character that changes its stance from time to time.

## The anchor settings

| Setting | What it does |
|---|---|
| **Animation** | The idle loop or pose to use. It must use the same skeleton as the mesh. |
| **Mode** | **Play Looping** plays the animation as a loop. **Static Pose** holds one frame of it. |
| **Fixed Time** | For Static Pose only: the time in the animation to hold, in seconds. |
| **Selection Weight** | How often the plugin picks this anchor, compared with the others. The plugin picks a weight of 2 twice as often as a weight of 1. |
| **Min Hold Seconds / Max Hold Seconds** | How long the character stays on this anchor before it changes. The plugin picks a random time between the two. |
| **Play Rate Range** | Each character plays the loop at a slightly different speed, picked from this range. This keeps a crowd from moving in sync. |
| **Blend Time** | How long the blend into this anchor takes, in seconds. |
| **Min Tension / Max Tension** | The plugin only picks this anchor while the character's Tension is in this range. Example: an arms-crossed pose that only shows when the character is calm. |
| **Tags** | Free labels for your own tools. The plugin does not read them. |

## The library settings

| Setting | What it does |
|---|---|
| **Avoid Immediate Repeat** | The plugin does not pick the same anchor twice in a row when another one is available. |
| **Allow Additive Animations** | Off by default. See the note below. |

## Use the library

**On a mesh without an Animation Blueprint:**

1. Select the actor and then its **Idle Weaver** component.
2. In **Idle Weaver > Setup**, set **Pose Library** to your asset.

**Inside an Animation Blueprint:**

1. In the AnimGraph, add the **Idle Pose Library** node.
2. Select the node and set **Pose Library** to your asset.
3. Connect it to the **Idle Weaver (Micro-Motion)** node. Unreal adds the **Local To Component** node between them.

You can also change the library while the game runs. Set the **Pose Library** property on the component from Blueprint or C++. The character then starts a new sequence from the new library.

## Good to know

- **The plugin skips additive animations.** An additive clip (for example an aim offset or a lean) is not a full pose. If it plays as one, the body collapses. It writes one warning to the Output Log for each skipped clip. If every anchor in your library is additive, the character stays in the reference pose.
- **Use real idles.** Walk, run and jump clips make poor anchors.
- **Loops should loop.** If the first and last frame of a clip do not match, you see a small jump each time it repeats. Fix the clip, or use **Static Pose** mode.
- **One-frame poses work.** Set **Mode** to **Static Pose**.
- **Sitting works too.** Use a sit animation as the anchor. Then disable the Feet and Weight Shift channels in the profile. A sitting character does not stand on its feet, so those two channels do not fit.

## Problems

See [Troubleshooting](troubleshooting.md).
