PatActor
============================================================

| This component provides the ability to create and play PAT data within Unity.
| It takes in the source asset URL and contains linkage to the PatAsset and the shared IEightiAsset interface.
| NOTE: Changing the below parameters must happen before the asset URL is set. Otherwise, the changes are ignored.
| It can also take in the encryption key/kid as necessary. The fields should remain null when unused.
| It also allows disabling HW texture decode for testing (Android only), though HW decoding is enabled by default.
| It is used as the source for PatRender and PatAudioRender scripts.

