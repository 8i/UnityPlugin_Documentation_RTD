PatDownloader
============================================================

| This is a utility object used for the background download of Pat assets, signaling via its callback when complete or interrupted.
| It should be used once per asset download, as the parameters are specified at construction time.

- DownloadParams:
    - Uri: The web hosted URL that would otherwise be used in direct streaming
    - LocalDir: Local OS folder path to store the downloaded asset. Where appropriate on mobile platforms, permissions may need to be requested and granted by the user.
    - Quality: Toggle to download the highest, medium or lowest quality content representation. Usually meaning 2048, 1024 and 512 texture resolutions respectively.
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

