HvrActorAnimationSync
============================================================

This component allows a Animation clip to be synced with a HvrActor's playback.

The Animation will match the HvrActor's current time. Syncing the HvrActor to the Animation's time is not supported.


Parameters
------------------------------------------------------------

+-----------------+-----------+--------------------------------------------------------------------+
| Parameter       | Type      | Function                                                           |
+-----------------+-----------+--------------------------------------------------------------------+
| HvrActor        | HvrActor  | The HvrActor which will be used to sync the animation              |
+-----------------+-----------+--------------------------------------------------------------------+
| TargetAnimation | Animation | A Animation component which will be synced to the HvrActor's Asset |
+-----------------+-----------+--------------------------------------------------------------------+