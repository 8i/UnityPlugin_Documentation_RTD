.. _Components:

Components
============================================================

IEighti shared interface
------------------------------------------------------------

HVR and PAT codec playback can be controlled via the common IEighti interface, so that one set of controls can be used while supporting both codecs.
However, the instantiation of each of the codec Actors/Assets will differ.

.. toctree::
   :titlesonly:

   IEightiAsset
   IEightiActor

HVR Components
------------------------------------------------------------

All HVR components included in this plugin can be found within the 'Component' menu at the top of the Unity Editor window, or in the 'Add Component' menu on any GameObject.

Unity's manual demonstrates how components are used: https://docs.unity3d.com/Manual/UsingComponents.html

**Main Components**

.. toctree::
   :titlesonly:

   HvrActor
   HvrRender
   HvrLight

**Effects**

.. toctree::
   :titlesonly:

   HvrActor3DMask
   HvrColorGrading
   HvrShaderSubroutine

**Utilities**

.. toctree::
   :titlesonly:

   HvrActorTrigger
   HvrActorAnimationSync
   HvrActorAudioSourceSync
   HvrActorProjectorShadow
   HvrDataBuildInclude

PAT Components
------------------------------------------------------------

| The easiest way to instantiate a PAT playback object is via the example PatActor prefab.
| There are example PAT scenes in 8i/examples/scenes that provide the best starting point.

**Main Script Components**

.. toctree::
   :titlesonly:

   PatActor
   PatAsset
   PatAudioRender
   PatPlayerRepresentation
   PatRender

**Examples**

.. toctree::
   :titlesonly:

   PatStreamPlayer

