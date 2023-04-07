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
**What is PAT**

PAT is the latest codec developed by 8i. PAT is a mesh based codec, in which the final
asset output is represented as a sequence of textured meshes

**Output from PAT**

The PAT codec produces several outputs. It's important to understand that the outputs
are simply a different encapsulation around the same output data. The available outputs are:

    * MPD - This format extends the well known MPEG-DASH and HLS standards. This format should be used
      for all applications that require streaming and playback that is longer than a few seconds.
      More info about an MPD structure can be found in the `MPD structure <Mpd.html>`_ document

    * glTF - This output can be used in standard editors/players and social platforms. glTF is widely adopted format, particularly suitable for the web.
      However, this format performs poorly for longer content where progressive streaming is required.

    * FBX - This output is primarily used for cases where the output needs to be edited using
      tools like Maya. After editing, this format can be converted to any of the other formats.

**Difference from HVR**

The main difference between HVR and PAT is how the underlying 3D asset is represented.
HVR takes the approach of representing the 3D asset as a point cloud. However, PAT represents the asset as a textured mesh.
Effectively, PAT decouples the mesh(geometry) resolution from the texture(color) resolution. Allowing us to scale up the asset perceived resolution, with smaller increase in overall asset size.
To illustrate it, think of an actor with a very textured shirt. The underlying geometry of the shirt is fairly simple, allowing us to save a lot of geometry bandwidth. In this case most the complexity is on the texture side, which we can very effectively encode using standard video codecs.
The represent the high details with HVR, we will need a very high resolution of points, causing the file size to explode.

**PAT usage with Unity**

HVR is using a point cloud to represent the data. Point clouds are less standard and hence Unity's standard rendering will not produce the best output to the user.
As a result, to produce the best quality render, the HVR plugin takes over the rendering of the asset. This internal rendering takes away some of feature set that a developer would expect with a 3D asset in Unity.
In contrast, PAT simply delivers a mesh and a texture per frame, giving back the control over rendering and 3D asset manipulation and effects to the developer.

| The easiest way to instantiate a PAT playback object is via the example PatActor prefab.
| There are example PAT scenes in 8i/examples/scenes that provide the best starting point.

**PAT usage with Timeline**

| PAT playback supports usage with Unity's Timeline system starting with Unity 2020.
| See the example scene in 8i/examples/scenes/Example-PAT-Timeline.unity for a sample integration.

.. toctree::
   :titlesonly:

   PatTimelineProperties
   PatTrackRenderer
   PatActor_AssetBehavior
   PatActor_AssetTrack
   PatActor_ClipMixerBehavior
   PatActor_PlayableAsset

**Main Script Components**

.. toctree::
   :titlesonly:

   PatActor
   PatAsset
   PatAudioRender
   PatDownloader
   PatLiveManager
   PatPlayerRepresentation
   PatRender

**Examples**

.. toctree::
   :titlesonly:

   PatStreamPlayer
   PatLiveAsgardPlayer

**PAT with webplayer and 8thwall**

PAT MPD assets can be streamed and played on the browser. Additional information about usage of the web player can be found here:
https://8i.github.io/embeddable_webplayer/#/

