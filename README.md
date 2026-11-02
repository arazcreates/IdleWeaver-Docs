# Idle Weaver

Idle Weaver is an Unreal Engine 5.8 plugin that makes standing NPCs look alive. It layers small movements on top of a pose or animation you already have, and every character gets its own rhythm.

<p align="center">
  <img src="docs/images/without-with.gif" width="640" alt="Two identical characters in the same pose. The one on the left stands frozen. The one on the right shifts its weight, moves its hands and looks around.">
</p>

Same mesh, same pose, same preset. The only difference is Master Intensity: 0 on the left, 1 on the right.

Idle Weaver is a layer. It won't make a character walk, sit or dance. It makes one that's standing, sitting or waiting feel like someone's in there.

Every clip on this page is the real plugin running on the default Unreal mannequin with stock presets. The only tweak: in the gaze clips, the red ball has a raised weight so the head keeps following it. The source code isn't in this repo. The plugin is sold on Fab.

## What it adds

| | |
|---|---|
| ![A character's chest rising and falling.](docs/images/breathing.gif)<br>**Breathing** | ![A character shifting its weight from leg to leg.](docs/images/weight-shift.gif)<br>**Weight shifts** |
| ![A character's hands fidgeting and clenching.](docs/images/hand-fidgets.gif)<br>**Hand fidgets** | ![A character turning its head to follow a red ball.](docs/images/gaze.gif)<br>**Head that follows targets** |
| ![A test head turning, with two eyes aiming at a target.](docs/images/eyes.gif)<br>**Eyes that lead the head** (test head with two eye bones) | ![Three characters standing with different moods.](docs/images/moods.gif)<br>**Cold, tired or tense, set from gameplay** |

Feet stay planted on uneven ground:

![Two pairs of feet on a slope. With the Feet channel off, both feet stay level. With it on, each foot sits on the ground at its own height.](docs/images/feet.gif)

And no two characters move alike, even with the same mesh and pose:

![Five identical characters. Each one moves on its own rhythm.](docs/images/crowd.gif)

## Start here

1. [Install the plugin](docs/installing.md)
2. [Give your character a pose](docs/pose-library.md)
3. [Pick a preset, or tune your own](docs/profiles-and-presets.md)

Stuck? [Troubleshooting](docs/troubleshooting.md) covers the A-pose, characters that don't move, gaze, feet, eyes and MetaHumans. Every setting, node and function is in the [reference](docs/reference.md).

## Good to know

- It needs Unreal Engine 5.8 on Windows. Other platforms aren't tested.
- The Fab install comes compiled, so it works in Blueprint-only projects.
- Everything works from both Blueprint and C++.
- It has six presets: Villager, Guard, Merchant, Crowd, Exhausted and Nervous.
- MetaHumans and other multi-mesh characters are supported. The setup is in the [reference](docs/reference.md#path-c-a-metahuman-or-any-character-built-from-several-meshes).
- You can bake the result to a normal Animation Sequence.

What changed in each version is in the [changelog](CHANGELOG.md).

## Support

Email arazcreates@gmail.com with your Unreal Engine version and the `LogIdleWeaver` lines from the Output Log.
