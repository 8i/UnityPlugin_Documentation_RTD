============================================================
HvrActorAudioSourceSync
============================================================
    
This component allows a Audiosource's AudioClip to be synced to the playback of a HvrActor's asset.

The HvrActorAudioSourceSync does not take an audio clip itself as a value.

It expects the audiosource to have an audioclip assigned. Once you have assigned a Audiosource and HvrActor, you will not need to manage this component - If the actor is playing, the audio source will be playing.

If the AudioClip assigned to the AudioSource is shorter than the HvrActor's asset duration it will play as long as it can, if it is longer it will stop once the HvrActor stops playing.


Parameters
------------------------------------------------------------

+--------------+-------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter    | Type        | Function                                                                                                                                                             |
+--------------+-------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Actor        | HvrActor    | A HvrActor which has an Asset                                                                                                                                        |
+--------------+-------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Audio Source | AudioSource | A AudioSource component which has a AudioClip assigned to it                                                                                                         |
+--------------+-------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Offse        | Float       | A time in seconds which this component will use to offset the sync time. This can be useful for situations where the audio clip start time does not match the Asset. |
+--------------+-------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+