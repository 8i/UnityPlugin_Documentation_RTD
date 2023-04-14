PatActor_AssetBehavior
============================================================

| Implements Unity's PlayableBehaviour interface and is responsible for rendering data from PatActor_PlayableAsset on the associated PatActor_AssetTrack.
| A PlayableAsset will have a PlayableBehaviour attached to it.

- assetPath: Path to the asset to load. This is automatically set during the associated PatActor_PlayableAsset's creation.
- patTrackRenderer: The rendering object used by the asset when it's active. Set by the PatActor_ClipMixer.
- preloadTime: Amount of time in seconds specifying how much earlier to load a PatAsset that will be played.
