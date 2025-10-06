# HISPlayer Unity Meta Quest SDK Release Notes

### Version 4.7.13
##### October 6, 2025
- [**Improvement**] Optimized the ordering of the displayed video frames with Vulkan material/RenderTexture/RawImage rendering.
- [**Improvement**] Optimized the playback performance when locking and unlocking the Quest device.
- [**Improvement**] Optimized the playback performance with Quest Dynamic Resolution Scaling enabled.

### Version 4.7.12
##### September 19, 2025
- [**Improvement**] Optimized performance when locking and unlocking Quest device.

### Version 4.7.11
##### August 27, 2025
- [**Improvement**] Removed the redundant release error log when the player is destroyed.

### Version 4.7.10
##### August 13, 2025
- [**Improvement**] Optimized player release with Vulkan rendering.

### Version 4.7.9
##### July 31, 2025
- [**Improvement**] Optimized HISPlayer component creation and removal.

### Version 4.7.8
##### June 26, 2025
- [**Added**] SetExternalSurface API to set the external surface of a certain player to be used.
- [**Added**] ReleaseExternalSurface API to release the external surface from a certain player.

### Version 4.7.7
##### June 16, 2025
- [**Added**] GetAvailableCodecs API to provide the available codecs list on the device.

### Version 4.7.6
##### June 5, 2025
- [**Improvement**] Optimized SynchronizeMultiStreams API to make the secondary stream will automatically seek following the main stream current time plus the offset.

### Version 4.7.5
##### May 30, 2025
- [**Added**] SynchronizeMultiStreams API with offset.
- [**Added**] FlipTextureVertically API to flip the texture of the stream vertically.
- [**Added**] SetLogLevel API to establishes the amount of logs to be shown.

### Version 4.7.4
##### May 6, 2025
- [**Improvement**] Optimized SetUpPlayer speed.

### Version 4.7.3
##### April 23, 2025
- [**Improvement**] Optimized macOS editor usage.

### Version 4.7.2
##### April 15, 2025
- [**Improvement**] Optimized video performance for material rendering with Vulkan.

### Version 4.6.6
##### March 13, 2025
- [**Added**] GetAudioSessionId API.

### Version 4.6.5
##### March 4, 2025
- [**Improvement**] Optimized rendering performance.

### Version 4.6.4
##### January 30, 2025
- [**Added**] unityAudio in class StreamProperties to output the audio data to Unity instead of using direct output to device speaker.
- [**Added**] GetAudioData API to return the audio PCM data of each channel in float array.
- [**Added**] FillAudioData API to fill the audio buffer with new audio PCM data.
- [**Added**] GetWidevineSecurityLevel API to return the security level of the loaded Widevine DRM protected content as a string.
- [**Added**] SynchronizeMultiStreams API to synchronize the playback of secondary stream following the primary stream.

### Version 4.6.3
##### January 10, 2025
- [**Added**] GetNativeTextureId API.
- [**Added**] nativeTextureId in the List<StreamProperties> multiStreamProperties.

### Version 4.6.2
##### January 9, 2025
- [**Added**] Multi streams support using external surfaces and materials.
- [**Added**] GetVolume API.
- [**Added**] IsMuted API.
- [**Added**] IsPlaying API.
- [**Added**] EventVolumeChange API for Windows editor.
- [**Improvement**] Removed multithreaded rendering restriction.

### Version 4.5.2
##### November 28, 2024
- Initial release of Unity Meta Quest SDK as an upgrade from Unity AllPlatforms SDK.
