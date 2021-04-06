PatAsset
============================================================

| This is the main API for configuration and control of PAT playback.
| This is not an exhaustive API listing, but the following are of special note:

- EnableAudio
    | Controls audio playback enablement for the asset. This will automatically be called during PatActor.SetAssetDataUrl using the Unity project's output samplerate.
    | If used manually, it needs to be called prior to Create()

- Download
    This can be used to download a PAT asset for local playback with the following fields:

    - uri: The web hosted URL that would otherwise be used in direct streaming
    - localDir: Local OS folder path to store the downloaded asset. Where appropriate on mobile platforms, permissions may need to be requested and granted by the user.
    - newUri: On successful download, the returned path to the local manifest file which can be used as the input to PatActor.SetAssetDataUrl()
    - quality: Toggle to download the highest or lowest quality content representation (defaults to highest)

- GetRepresentations
    This allows for enumeration of available PatPlayerRepresentation objects per audio/video/mesh type. Primarily, video representation is used to provide different levels of bandwidth/quality.

- SelectRepresentation
    - Once enumerated, this API can be used on an initialized (Create() called) asset to switch to a particular representation.
    - If the switched representation is of the same fps, the switch will happen once already downloaded and cached data is used up (a few seconds). Otherwise, in the case of a different framerate, the switch happens immediately.
    - There is a special value of -1 for bitrate that can be used to set automatic adaptive bitrate switching on the specified type. This would currently only need to be set on the video representation.

