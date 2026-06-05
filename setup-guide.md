# QuickStart Guide
Getting started with HISPlayer consists of implementing the following steps:

1. Import and configure SDKs

      1.1. Integrate Meta XR All-in-One SDK
 
      1.2. Import package
 
      1.3. Configure Unity for Android
   
2. HISPlayer Meta Quest SDK Sample

      2.1 Import HISPlayer Meta Quest SDK Sample

      2.2 Sample Explanation

## 1.1 Integrate Meta XR All-in-One SDK

Integrate HISPlayer SDK with the **[Meta XR All-in-One SDK](https://developer.oculus.com/downloads/package/meta-xr-sdk-all-in-one-upm/)** or **Meta XR Core SDK** only for smaller package size.

First, please configure the Unity project for Oculus by following this [Tutorial](https://developer.oculus.com/documentation/unity/unity-tutorial-hello-vr/) and open **Window > Package Manager > Packages: In Project** to check Meta XR All-in-One SDK is installed properly.

<p align="center">
<img width="605" alt="image" src="https://github.com/HISPlayer/UnityAndroid-SDK/assets/47497948/b4e362ba-f3d1-4d07-a46b-7a76e73d30fb">
</p>

#### Meta XR Setup Tool

Open **Edit > Player Settings > MetaXR**, select the Android platform and clik "**Select All**" and "**Apply All**" in order to set up all the Meta XR settings. 

<p align="center">
<img width="90%" alt="image" src="https://github.com/HISPlayer/UnityAndroid-SDK/assets/47497948/691d9de5-3874-4b6a-bb1e-3b2981020590">
</p>

In XR Plug-in Management, please make sure that you have the **OpenXR** option checked (or Oculus for older Meta XR SDK version). Otherwise, when you run the application, it will show a 2D window without XR environment.
  
  - **Edit > Project Settings > XR Plug-in Management**

<p align="center">
<img width="60%" alt="image" src="https://github.com/user-attachments/assets/3d1372e8-ee40-41fd-8ddd-d8d360a47534">
</p>

## 1.2 Import HISPlayer SDK

Importing the SDK is the same as importing other normal packages in Unity. 
Select the package of _HISPlayer SDK_ and import it.

**Assets > Import Package > Custom Package > HISPlayer Meta Quest SDK unity package**

Select the package of _HISPlayer SDK_ and import it.

<p align="center">
<img width=90% src="https://github.com/user-attachments/assets/c6c6d488-2b2c-4b79-b775-dd9dffc14471">
</p>

## 1.3 Configure Unity for Android

Open the window **Tools > HISPlayer** located in the upper side of the screen > Click on Player Settings Configuration > Select **Build Target to Android** > Set all the required settings.

<p align="center">
<img width="450" src="assets/image-player-setting-configuration.png">
</p>

Setting **"Plugins folder"** will create **mainTemplate.gradle** and **gradleTemplate.properties** in your ProjectRoot\Assets\Plugins\Android. Please make sure you use the correct **mainTemplate.gradle** that is generated from our SDK. If you need to modify it, please make sure the dependencies and configurations from HISPlayer SDK's mainTemplate.gradle exist in your modified gradle file.

#### Android Target API Level
It is recommended to set Target API Level to 34 or higher. By selecting Android target 34, Unity is going to ask you to update (in the case you don't have the SDK installed). Please, press "Update Android SDK" button.

<p align="center">
<img width="250" alt="image" src="assets/image-android-sdk-update.png">
</p>

Alternatively, you may set the Target API level to 34 or higher in the Unity project settings.
 
## 2.1 Import HISPlayer Meta Quest SDK Sample

Please, download the sample here[DELETE THIS COMMENT, upload the sample after the review): [**HISPlayer Meta Quest SDK Sample**]() (no need to download it if you have received it in the email). 

Before using the sample, please make sure you have followed the above steps to set-up your Unity project for Oculus and HISPlayer SDK. To use the sample, please follow these steps:
  - Set up the Meta XR All-in-One environment
  - Import HISPlayer SDK
  - Import HISPlayer Meta Quest SDK Sample
  - Import TextMeshPro. Go to Unity Window > TextMeshPro > Import TMP Essential Resources.
  - If you received a license key from HISPlayer, input the license key through the Inspector Unity window: **StreamController GameObject > HISPlayerSample component > License Key**. This must be done for **each scene** while adding them to the Scene List. Open each scene located in `Assets/HISPlayerMetaQuestSample/Scenes/`, set the license key if needed, then go to **File > Build Settings > Add Open Scenes** to include it in the **Scene List** of the Build Profile.
  - Build and Run

To check how to set up the SDK and API usage, please refer to the sample scenes described below.

## 2.2 Sample Explanation

### Shared Elements

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

### Available Scenes
#### 360 Scene
This scene renders a 360° video.

Instead of a Quad, the Mesh Filter uses a **Sphere**, and the assigned material is **360_Mat**, which relies on the **HISPlayer360Shader**.
<p align="center">
  <img 
    alt="image" 
    src="https://github.com/user-attachments/assets/ca9214e3-242e-499e-b454-93bb6944337a"
    style="max-width: 100%; height: auto;"
  />
</p>

The `OVROverlay` **Overlay Shape** is set to `Equirect`.
<p align="center">
  <img 
    alt="image" 
    src="https://github.com/user-attachments/assets/467d5a7e-1932-4bae-8951-d54561bc9b35"
    style="max-width: 100%; height: auto;"
  />
</p>

#### Ambisonic Scene
This scene plays **audio-only** content; there is no video rendering surface. The default stream used is:  
`https://downloads.hisplayer.com/Unity/test-contents/Ambisonic_AmbiX_16Ch.mkv`  
with **Ambisonic Audio** configured as **AMBIX_16 Channels**.  

You can also test with these alternative streams:  
- `https://downloads.hisplayer.com/Unity/test-contents/Ambisonic_AmbiX_9Ch.mkv` with **Ambisonic Audio** configured as **AMBIX_9 Channels**.  
- `https://downloads.hisplayer.com/Unity/test-contents/Ambisonic_TBE_8_2.mkv` with **Ambisonic Audio** configured as **TBE_8 Channels_2 Head Locked Channels**.

For more information, please refer to the following [Ambisonic documentation](https://hisplayer.github.io/UnityMetaQuest-SDK/#/ambisonic).

#### HEVC_DRM Scene
This scene is designed for **DRM-protected HEVC** content.

For more information, please refer to the following [DRM documentation](https://hisplayer.github.io/UnityMetaQuest-SDK/#/drm).

#### MultiStream Scene
Here the sample uses the **HISPlayerVRMultiController** script, a variant of `HISPlayerVRController` that is adapted to handle **two video streams** simultaneously. You can activate the **Synchronize Streams** option to keep both streams in sync.

For more details, please refer to the following [Synchronize MultiStreams API documentation](https://hisplayer.github.io/UnityMetaQuest-SDK/#/hisplayer-api?id=void-synchronizemultistreamsint-primaryplayerindex-int-secondaryplayerindex-long-offsetms-0).

#### MV-HEVC Scene
This scene is configured to play **MV-HEVC** (Multiview High Efficiency Video Coding) content, enabling native 3D or multiview video playback.

For more information, please refer to the following [MV-HEVC documentation](https://hisplayer.github.io/UnityMetaQuest-SDK/#/stereoscopic?id=hisplayer-meta-quest-mv-hevc-sample).

#### Spatial Audio Scene
Two helper GameObjects are present in the scene: **FillAudioSourceGroup** and **GetAudioSourceGroup**. Activating or deactivating them switches between the corresponding audio retrieval APIs.

For more information, please refer to the following [Audio Retrieval guide](https://hisplayer.github.io/UnityMetaQuest-SDK/#/audio-retrieval).

#### Stereoscopic Scene
This scene is set up for **stereoscopic video** playback, rendering separate left/right eye views.

For more information, please refer to the following [Stereoscopic guide](https://hisplayer.github.io/UnityMetaQuest-SDK/#/stereoscopic).

### Controls
#### Scene Navigation Controls
Use the **right controller** to navigate between the sample scenes:
- Press **A** to move to the **next scene**.
- Press **B** to go back to the **previous scene**.

The order of the scenes is defined by the **Scene List** in the **Build Profile** (File > Build Settings).

#### Playback Controls
Each scene provides a unified control bar with the following interactive elements:

<p align="center">
  <img 
    alt="image" 
    src="https://github.com/user-attachments/assets/f36fb43b-c2b7-4161-81bd-9eac33ea735d"
    style="max-width: 100%; height: auto;"
  />
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

## More Information, Features and APIs
For more information about the supported features and APIs, please refer to the following [**HISPlayer API**](/hisplayer-api.md).
