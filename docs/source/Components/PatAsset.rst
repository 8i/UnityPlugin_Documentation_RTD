PatAsset
============================================================

| This is the main API for configuration and control of PAT playback.
| It is a superset of the shared IEightiAsset interface, providing access to PAT specific API.
| This is not an exhaustive API listing, but the following are of special note:

- EnableAudio
    | Controls audio playback enablement for the asset. This will automatically be called during PatActor.SetAssetDataUrl using the Unity project's output samplerate.
    | If used manually, it needs to be called prior to Create()

- EnumerateFramerates
    This allows for enumeration of available fps variants in the content

- GetFramerate
    This returns the currently selected fps setting

- SelectFramerate
    Select the fps of the mesh and video streams. This will attempt to maintain an equivalent texture quality level.

- GetRepresentations
    This allows for enumeration of available PatPlayerRepresentation objects per audio/video/mesh type. Primarily, video representation is used to provide different levels of bandwidth/quality.

- SelectRepresentation
    - Once enumerated, this API can be used on an initialized (Create() called) asset to switch to a particular fps and representation.
    - If the switched representation is of the same fps, the switch will happen once already downloaded and cached data is used up (a few seconds). Otherwise, in the case of a different framerate, the switch happens immediately.
    - If the switched representation is a different fps, the fps is switched first, then the bitrate is selected.
    - There is a special value of -1 for bitrate that can be used to set automatic adaptive bitrate switching on the specified type. This would currently only need to be set on the video representation.

