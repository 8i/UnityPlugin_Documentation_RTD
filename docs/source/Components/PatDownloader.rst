PatDownloader
============================================================

| This is a utility object used for the background download of Pat assets, signaling via its callback when complete or interrupted.
| It should be used once per asset download, as the parameters are specified at construction time.
| Fps and representations should be enumerated when using CUSTOM QualityType.

- DownloadParams:
    - Uri: The web hosted URL that would otherwise be used in direct streaming
    - LocalDir: Local OS folder path to store the downloaded asset. Where appropriate on mobile platforms, permissions may need to be requested and granted by the user.
    - QualityType: Toggle to download predefined (LOW, MEDIUM, HIGH) or CUSTOM quality level.
    - Fps: Chosen fps when using CUSTOM QualityType.
    - AudioBitrate: Chosen audio bitrate when using CUSTOM QualityType.
    - MeshBitrate: Chosen mesh bitrate when using CUSTOM QualityType.
    - VideoBitrate: Chosen video bitrate when using CUSTOM QualityType.
    - EncryptionKey: Set to encryption key as needed, otherwise should be null.
    - EncryptionKid: Set to encryption kid as needed, otherwise should be null.

- StartDownload:
    Begins the download, returns failure if the download is already in progress

- StopDownload:
    Interrupts an ongoing download. The callback will return failure 

- OnAssetDownloaded callback:
    The callback is executed on a background thread, so much of the Unity API is unavailable.
    The implementation should simply take the local device path and pass it off to be used for PatAsset creation on the main thread.

    - success: Denotes whether the download completed successfully
    - newUri: On successful download, the returned path to the local manifest file which can be used as the input to PatActor.SetAssetDataUrl()

- OnDownloadProgress callback:
    The callback is executed on a background thread, so much of the Unity API is unavailable.
    Returns the latest download progress percentage

    - progressPercentage: progress percentage value, 0-100

