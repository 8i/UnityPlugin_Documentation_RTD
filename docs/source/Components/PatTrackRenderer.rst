PatTrackRenderer
============================================================

| This component is used as a binding target for the PatActor_AssetTrack.
| It contains a set of PatRender and PatAudioRender components so that the track is able to render its data.
| It can be instantiated from the right-click menu in a scene's hierarchy under 8i/PatTrackRenderer.
| It must explicitly have the PatPlayerMaterial added to its MeshRenderer Materials list.

- SetActor() is used to set the current PatActor to be used in rendering. This switching is handled by the ClipMixer, it should not be used explicitly.
