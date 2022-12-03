# Universal Windows Platform (UWP)

<center>
<p style="color:red; font-weight: bold">
UWP (Windows Store) platform has been deprecated and soon will be removed!
</p>
</center>

## Technical information

Flax is compiled for Universal Windows Platform using Microsoft Visual C++ compiler. It uses **v141** (VC\+\+ 2017) toolset and **Windows 10 SDK** with Multi-threaded DLL runtime. All dependent libraries are used via static linking by the Flax Engine binary.

## Build options

![Build Options](media/build-xbox-one.jpg)

| Property | Description |
|--------|--------|
| **Output** | The built game output folder (relative to the project). |
| **Show Output** | If checked, after building the output folder will be shown in an Explorer. |
| **Configuration Mode** | Game building mode. Possible options: <table><tbody><tr><th>Option</th><th>Description</th></tr><tr><td>**Release**</td><td>The release build ready for shipment.</td></tr><tr><td>**Debug**</td><td>The debug build for testing and profiling. Most of the code optimizations are disabled for the best debugging experience.</td></tr><tr><td>**Development**</td><td>The development build for testing and profiling but is more optimized for runtime than Debug build.</td></tr></tbody></table>|

## Platform settings

![Settings](media/settings-uwp.jpg)

| Property | Description |
|--------|--------|
| **Preferred Launch Windowing Mode** | The preferred launch windowing mode. See [WindowMode](https://docs.flaxengine.com/api/FlaxEditor.Content.Settings.UWPPlatformSettings.WindowMode.html) docs. |
| **Auto Rotation Preferences** | The display orientation modes. Can be combined as flags. See [DisplayOrientations](https://docs.flaxengine.com/api/FlaxEditor.Content.Settings.UWPPlatformSettings.DisplayOrientations.html) docs. |
| **Certificate Location** | The location of the package certificate (relative to the project). |
