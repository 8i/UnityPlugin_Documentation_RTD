.. _QuickStart:

Quick Start
============================================================

Download and Installation
------------------------------------------------------------

Download the 8i Unity Plugin. You should be getting a link from 8i after the purchase of stage, or you can ask your 8i contact to get one.

Once downloaded extract the ‘8i’ folder from the zip file into your project's Asset directory.


Creating a HvrActor
------------------------------------------------------------

Before beginning, ensure that the HvrActor, HvrRender or HvrLight components are available through the Unity Component Menus. If they are not, check the installation instructions or the Troubleshooting section of this documentation.

1. Create a HvrActor by right clicking in the Hierachy and select '8i/Create HvrActor'
2. Drag and drop one of the folders contained under '8i/examples/assets/hvr/' onto the 'Reference' slot of the HvrActor
3. Select the Main Camera in the scene
4. Add the 'HvrRender' component
5. Optionally, if you need lighting at the expense of speed: Select the 'Directional Light' in the scene, then add the 'HvrLight' component

The HvrActor will now be rendering both the scene and game view.

Creating a PatActor
------------------------------------------------------------

The easiest method to create a PAT playback object is to instantiate the PatActor prefab located under 8i/examples/assets/prefabs. The prefab puts together the needed PatActor, PatRender, and PatAudioRender components, and is properly scaled to match the Unity expected unit measures. The prefab still requires some in-code linking of the components, an example of which is located as a full scene in 8i/examples/scenes/Example-PAT-streaming.unity

- The example scene uses a helper PatStreamPlayer script. The script takes in an input AssetUrl, and upon starting the scene, instantiates the PatActor prefab, links the renderers to the PatActor so they render its data, and then initializes the PatActor instance with the AssetUrl.
- It can pre-download or directly stream the content at the provided AssetUrl using the DownloadAsset flag. An example scene with the Download toggle enabled also exists as Example-PAT-download.
- Finally, it shows example usage of the IEightiAsset control interface (which can be used for both Hvr and Pat assets), by enabling looping and beginning playback of the content.

It is important to note that the PatStreamPlayer script is a good base example of the usage, but does not utilize every component of the PAT Unity API.
See the Components page for additional information on the Pat components and more advanced usage of the PatAsset interface for things like manual and automatic bitrate switching.

Creating a build
------------------------------------------------------------

1. Follow the 'Adding a HvrActor to your scene' steps above.
2. Save the scene.
3. Open Build Settings window under 'File/Build Settings...'.
4. Click the 'Add Open Scenes' button on the right of the window, or drag the scene that was just saved from the 'Project' window of the Unity Editor.
5. Click the 'Build and Run' and follow the onscreen prompts and select your build location.

Unity will now compile the project and create a build.

If it does not, check the Unity Editor console or the Troubleshooting section of this documentation. 


Building for VR
------------------------------------------------------------

The 8i Unity Plugin fully supports VR rendering.

To enable VR for your Unity Project

1. Open the 'Player Settings' window from 'Edit/Project Settings/Player'.
2. Tick the 'Virtual Reality Supported' checkbox.
3. From the new list, make sure the target headset you wish to use is listed. If it isn't, add it by clicking the + icon.
4. Ensure your main camera has a HvrRender component attached to it

If you encounter any issues getting VR working in your Unity Project, please consult the Unity Manual
`[Link to Unity Docs] <https://docs.unity3d.com/Manual/VROverview.html>`_

Note: Android-based VR headsets like Google Daydream and Oculus Go are also supported. You may want to consult their own document on how to build an app in Unity.

Building for AR
------------------------------------------------------------

To get started with ARKit or ARCore, we provide a set of tutorials here: :ref:`Tutorials`
