PatLiveAsgardPlayer
============================================================

| This is an example script used by our sample scene to instantiate a PatActor, set up a PatLiveManager and correctly initialize it to play.
| This example demonstrates how to achieve continuous playback across multiple live stream sessions.
| It uses the StreamActive state and assetInterface properties to stop playback once all the data is played through.
| As long as the mLiveManager is kept Active, the example will continuously play across live stream sessions.

Parameters
------------------------------------------------------------
- AsgardUrl: The URL to monitor for live stream status changes, which is passed in to PatLiveManager
- PatActorPrefab: Should be set to the provided PatActor.prefab
