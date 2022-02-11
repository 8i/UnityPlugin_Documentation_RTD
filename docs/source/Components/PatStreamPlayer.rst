PatStreamPlayer
============================================================

| This is an example script used by our sample scenes to instantiate a PatActor prefab and correctly initialize it to play.
| Note that it runs via Unity's Awake and Start functions, so in the case of download, the engine will be frozen until the download completes.

Parameters
------------------------------------------------------------

+----------------+-----------------------------------------------------------------------------------------------------------+
| AssetUrl           | URL to the cloud hosted manifest                                                                      |
+----------------+-----------------------------------------------------------------------------------------------------------+
| PatActorPrefab     | Should be set to the provided PatActor.prefab                                                         |
+----------------+-----------------------------------------------------------------------------------------------------------+
| DownloadAsset      | Controls whether the asset should first be downloaded, or streamed directly from the web              |
+----------------+-----------------------------------------------------------------------------------------------------------+
| OnTriggerSeek      | On touch or space key, trigger seek to half of current playout time                                   |
+----------------+-----------------------------------------------------------------------------------------------------------+
| OnTriggerRepSwitch | On touch or space key, trigger cycling to the next video representation (streaming only)              |
+----------------+-----------------------------------------------------------------------------------------------------------+

