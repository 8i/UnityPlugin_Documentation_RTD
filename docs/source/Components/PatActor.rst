PatActor
============================================================

| This component provides the ability to create and play PAT data within Unity.
| It takes in the source asset URL and contains linkage to the PatAsset and the shared IEightiAsset interface.
| It is used as the source for PatRender and PatAudioRender scripts.
| NOTE: Changing the below parameters must happen before the asset URL is set. Otherwise, the changes are ignored.

- encryptionKey, encryptionKid: This pair should be set together when necessary. The fields should remain null when unused.
- enableTextureHwDecode: Controls hardware texture decode enablement (Android only), hardware decode is enabled by default.
- enableAudio: Controls audio playback enablement, enabled by default.
- playbackSpeed: Controls playout speed. No restrictions with audio disabled, but with audio enabled, the resampled audio frequency needs to be between 6k and 384k. With 48k audio output, that allows for 8x slowdown or speedup.

