HvrActorAudioSourceSync
===========

    This component has two slots, one for an Animation and one for an HvrActor. Filling both these slots will cause the AudioSource's playback to match the HvrActor.

.. note::
        The HvrActorAudioSourceSync does not take an audio clip itself as a value.
        It expects the audiosource to have an audioclip assigned. Once you have assigned a Audiosource and HvrActor, you will not need to manage this component - If the actor is playing, the audio source will be playing.
        If the AudioClip assigned to the AudioSource is shorter than the HvrActor's asset duration it will play as long as it can, if it is longer it will stop once the HvrActor stops playing.

How to Create
-------------

    1. Select (or create) a Unity GameObject
    2. Click on ‘Add Component’ in the inspector
    3. Go to ‘8i/HvrActor Audiosource sync’
    4. Slot the HvrActor and Audiosource into the component. From now on the audio source will match the playback time of the HvrActor.
