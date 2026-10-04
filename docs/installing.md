# Install Idle Weaver

[Back to the main page](../README.md)

There are two ways to install the plugin. Most buyers use the first one.

## Install from Fab (no compile needed)

1. Open the **Epic Games Launcher** and go to **Unreal Engine > Library**.
2. Find **Idle Weaver** in the **Fab Library** section. If you do not see it, click the refresh button.
3. Click **Install to Engine** and select engine version **5.8**.
4. Open your project.
5. Go to **Edit > Plugins**, search for **Idle Weaver**, and tick the box.
6. Restart the editor when it asks.

The plugin comes compiled. It works in a Blueprint-only project, and you do not need Visual Studio.

## Install from source (into one project)

Use this method if you want the plugin inside a single project, or if you want to change the code.

You need **Visual Studio 2022** with the *Game development with C++* workload. The free Community edition works.

1. Close the editor.
2. Copy the `IdleWeaver` folder into `YourProject/Plugins/`. Make the `Plugins` folder if it does not exist.
3. If the project has no C++ code, open it and use **Tools > New C++ Class > None** once. Then close the editor.
4. Open the `.uproject` file. When Unreal asks to rebuild the missing modules, click **Yes**.
5. Go to **Edit > Plugins** and make sure that **Idle Weaver** is enabled.

## Check that it works

1. Drag a Skeletal Mesh into the level. Do not give it an Animation Blueprint.
2. Select the actor, click **Add**, and add the **Idle Weaver** component.
3. Press Play.

The character breathes and shifts its weight. It stands in its reference pose (usually an A-pose or a T-pose), because it has no base pose yet. To give it one, see [Make a Pose Library](pose-library.md).

## Update to a new version

- **From Fab:** the launcher shows an **Update** button next to the plugin.
- **From source:** close the editor, delete the old `IdleWeaver` folder in `Plugins`, and copy the new one in. Your profiles and Pose Library assets stay in your project's `Content` folder, so you do not lose them.

## Problems

See [Troubleshooting](troubleshooting.md).
