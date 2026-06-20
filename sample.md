# Meta XR Sample

Please, download the sample here: [**HISPlayer Meta XR Sample**](https://downloads.hisplayer.com/Unity/Quest/HISPlayer_MetaXR_Sample_1.1.0.unitypackage) (no need to download it if you have received it in the email). 

## 1. Set Up HISPlayer Meta XR Sample

Before using the sample, please make sure you have followed the above steps to set-up your Unity project for Oculus and HISPlayer SDK. To use the sample, please follow these steps:
  - Set up the [Meta XR All-in-One environment](/setup-guide.md?id=_11-integrate-meta-xr-all-in-one-sdk).
  - Import HISPlayer SDK
  - Import HISPlayer Meta XR Sample
  - Import TextMeshPro. Go to Unity Window > TextMeshPro > Import TMP Essential Resources.
  - If you received a license key from HISPlayer, input the license key through the Inspector Unity window: **StreamController GameObject > HISPlayerSample component > License Key**. This must be done for **each scene** you want to test while adding them to the Scene List. Open each scene located in `Assets/HISPlayerMetaQuestSample/Scenes/`, set the license key if needed, then go to **File > Build Settings > Add Open Scenes** to include it in the **Scene List** of the Build Profile.
  - Build and Run

To check how to set up the SDK and API usage, please refer to the sample scenes described below.

## 2. Sample Explanation

### 2.1. Shared Elements

All sample scenes share a common foundation that you need to understand before looking at the specific configurations:

- A **HISPlayerSample** script (or a variant) that inherits from `HISPlayerManager` and requires the `using HISPlayerAPI;` dependency.
- An **OVROverlay** component attached to the `RenderScreen` GameObject. Its key properties are:
  - **Overlay Shape**: `Quad` for flat video, `Equirect` for 360°.
  - **Is External Surface**: `True`
  - **External Surface Width / Height**: set to the maximum resolution of your streams.
  - **Is Protected Content**: `True` when playing DRM-protected content.
- The `SetUpMetaQuest()` method finds the `OVROverlay` component, assigns it to `MultiStreamProperties.externalSurface`, and calls `SetUpPlayer()` to initialize the player.
- **MultiStreamProperties** must have **RenderMode** set to **External Surface** on the **StreamController** GameObject.

The typical video rendering GameObject is a Quad named **RenderScreen**. The 360 scene uses a Sphere (see details below). Every scene follows the same initialization flow.

Example script structure:

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using HISPlayerAPI;

public class HISPlayerSample : HISPlayerManager
{
    ...
}
```

With this shared baseline, each scene adds small variations that are explained in the following sections.

### 2.2. Available Scenes
#### 360 Scene
This scene renders a 360° video.

Instead of a Quad, the Mesh Filter uses a **Sphere**, and the assigned material is **360_Mat**, which relies on the **HISPlayer360Shader**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/ca9214e3-242e-499e-b454-93bb6944337a" alt="texto" width="50%" style="height: auto;" />
</p>

The `OVROverlay` **Overlay Shape** is set to `Equirect`.

<p align="center">
  <img src="https://github.com/user-attachments/assets/467d5a7e-1932-4bae-8951-d54561bc9b35" alt="texto" width="50%" style="height: auto;" />
</p>

#### 360 Stereoscopic Scene
This scene uses the same settings as the 360 ​​scene, but adds **stereoscopic video** playback, rendering separate left/right eye views.

For more information, please refer to the following [Stereoscopic guide](/stereoscopic.md).

#### Ambisonic Scene
This scene plays **audio-only** content; there is no video rendering surface. The default stream used is 3rd order ambisonics (16 channels) ambiX format configured as **AMBIX_16 Channels**.  

You can also test with these alternative streams:  
- `https://downloads.hisplayer.com/Unity/test-contents/Ambisonic_AmbiX_9Ch.mkv`: 2nd order ambisonics (9 channels) ambiX format configured as **AMBIX_9 Channels**.  
- `https://downloads.hisplayer.com/Unity/test-contents/Ambisonic_TBE_8_2.mkv`: 8 channels + 2 channels head-locked stereo TBE format configured as **TBE_8 Channels_2 Head Locked Channels**.

For more information, please refer to the following [Ambisonic documentation](/ambisonic.md).

#### DRM Scene
This scene is designed for **L1 DRM-protected HEVC** content with **External Surface** rendering mode.

For more information, please refer to the following [DRM documentation](drm.md).

#### MultiStream Scene
Here the sample uses the **HISPlayerVRMultiController** script, a variant of `HISPlayerVRController` that is adapted to handle **two video streams** simultaneously. You can activate the **Synchronize Streams** option to keep both streams in sync.

For more details, please refer to the following [Synchronize MultiStreams API documentation](/hisplayer-api.md?id=void-synchronizemultistreamsint-primaryplayerindex-int-secondaryplayerindex-long-offsetms-0).

#### MV-HEVC Scene
This scene is configured to play **MV-HEVC** (Multiview High Efficiency Video Coding) content, enabling native 3D or multiview video playback.

For more information, please refer to the following [MV-HEVC documentation](/stereoscopic.md?id=hisplayer-meta-quest-mv-hevc-sample).

#### Spatial Audio Scene
Two helper GameObjects are present in the scene: **FillAudioSourceGroup** and **GetAudioSourceGroup**. Activating or deactivating them switches between the corresponding audio retrieval APIs.

For more information, please refer to the following [Audio Retrieval guide](/audio-retrieval.md).

### 2.3. Controls
#### Scene Navigation Controls
Use the **right controller** to navigate between the sample scenes:
- Press **A** to move to the **next scene**.
- Press **B** to go back to the **previous scene**.

The order of the scenes is defined by the **Scene List** in the **Build Profile** (File > Build Settings).

#### Playback Controls
Each scene provides a unified control bar with the following interactive elements:

<p align="center">
  <img src="https://github.com/user-attachments/assets/f36fb43b-c2b7-4161-81bd-9eac33ea735d" alt="texto" width="50%" style="height: auto;" />
</p>

- **Video timeline**: a draggable seek bar that displays the current playback progress.
- **Stop** button
- **Mute** button
- **Volume control** slider
- **Previous Video** button
- **Backward** button
- **Play/Pause** button
- **Forward** button
- **Next Video** button
- **Speed Rate** button: cycles through the available playback speeds.
- **Subtitles** button: toggles subtitles when they are available.
- **Settings** button: opens a settings panel.

Inside the **Settings** panel, and depending on the video’s capabilities, you can change the **Quality**, **Language**, and **Captions**.
