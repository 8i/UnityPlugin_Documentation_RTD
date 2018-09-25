ARKit Tutorial
============================================================

Prerequisites
------------------------------------------------------------
* iOS devices that support ARKit and Metal and run *iOS 11.3* or later, see `here, <https://developer.apple.com/library/archive/documentation/DeviceInformation/Reference/iOSDeviceCompatibility/DeviceCompatibilityMatrix/DeviceCompatibilityMatrix.html>`_

  * ARKit 2.0 requires a device with iOS 12 installed

* Mac installed latest macOS
* *Unity 2017.1* or later
* *Xcode 9.3* or later

  * Command line tools installed, see `here. <http://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/>`_
  * ARKit 2.0 requires Xcode 10 or later

* Get a high level idea of how AR works on iOS from `Apple's documentation. <https://developer.apple.com/documentation/arkit/understanding_augmented_reality>`_ 

Getting Unity ARKit plugin
------------------------------------------------------------
Go to `https://bitbucket.org/Unity-Technologies/unity-arkit-plugin <https://bitbucket.org/Unity-Technologies/unity-arkit-plugin>`_ and download the official Unity ARKit plugin. You might need to install Mercurial or SourceTree to grab the source.

Switch to *1.5.1* tag if you want it to run on iOS 11 devices.
Here's how you do it in SourceTree but could be different if you use other Mercurial client:

  .. image:: ../images/switch-to-1.5.1.png

Importing 8i Unity Plugin
------------------------------------------------------------
Within the downloaded project, extract 8i Unity Plugin into the **Asset** folder, as stated in :ref:`QuickStart` section.

You should have the directory structure like this: 

  .. image:: ../images/unity-arkit-plugin-with-8i.png

Configure the Unity Project
------------------------------------------------------------

Open the project in Unity

If you are prompted to upgrade the Unity version, click yes.

Select File > Build Settings, a build dialogue should come up. In *Platform* choose iOS and click *Switch Platform* button.

Make sure the *Platform* is switched to iOS, and choose one of the scene as into the build. In this tutorial, we checked the simplest scene *UnityARBallz*.

  .. image:: ../images/switch-to-platform-ios.png

Still in Build Settings dialogue, click *Player Settings...* button.

A PlayerSettings inspector should appear.

.. note::
  It is requried to disable *Metal Editor Support*. This is because the 8i Unity Plugin doesn't not yet support Metal on macOS.

Make sure Metal is listed as the first in *Graphics APIs* and disable *Metal Editor Support*

  .. image:: ../images/turn-off-metal-editor.png


Your First 8i Hologram
------------------------------------------------------------
For this tutorial, we will edit the *UnityARBallZ* scene from Unity ARKit plugin's example.

We will change the original AR object to 8i's hologram, so that you can place a human hologram onto the augmented world.

To open the scene, find the scene in project and double click the scene.

  .. image:: ../images/open-unityarballz.png

You should be able to see something like this in Scene view:

  .. image:: ../images/seeming-empty-scene.png

This scene is a barebone template of an AR app and all it does is to automatically detect the environment and track the movement of the device and tie it to the virtual *Camera* object.

Select menu GameObject > 8i > HvrActor. This will create an GameObject with a HvrActor component attached to it.

  .. image:: ../images/create-8i-hvractor.png

Select the newly created *HvrActor* object.

There are a few options to note but for now we will just focus on the Asset/Data/Reference field.

This is the data source that 8i's hologram engine will read from. As you can see, right now it's empty. To specify a valid file reference, we can go to folder 8i/examples/assets/hvr, and find "president" folder:

  .. image:: ../images/inspector-hvractor.png

  .. image:: ../images/where-is-president.png

Drag this "president" folder to Asset/Data/Reference field in Inspector panel. To make things even simpler, uncheck the Rendering/Lighting/Use Lighting checkbox:

  .. image:: ../images/inspector-hvractor-president.png

You should be able to see the hologram has already been shown in the Scene view:

  .. image:: ../images/sceneview-president.png

Making A Prefab
------------------------------------------------------------
Because we want our user be able to drop the hologram whenever he touches the ground, we need to wrap this HvrActor object into a called "prefab" and let our ARKit code know to use it.

.. note::
    Prefabs are an `important concept in Unity <https://docs.unity3d.com/Manual/Prefabs.html>`_, 

Making sure HvrActor is currently selected, drag the HvrActor object down to a folder in the Project window, Unity will automatically create a prefab for you, and you will see the name of HvrActor turns blue:

  .. image:: ../images/drag-to-make-prefab.png

To change the ARKit code to spawn *HvrActor*s instead of balls, find *BallMaker* object in the scene and select it.
Drag the newly created prefab *HvrActor* to *BallMaker*'s Inspector panel, replace *BallPrefab* with *HvrActor*:

  .. image:: ../images/replace-ballmaker-with-hvractor.png

Because we have stored the HvrActor in a prefab it is now safe to delete the HvrActor in the scene. Go to Hierarchy and right click on HvrActor, which should has its name in blue colour, and choose "Delete".

  .. image:: ../images/delete-template-hvractor.png

Save the scene by pressing Cmd+S.

Camera Configuration
------------------------------------------------------------
Next we need to configure the camera to let it render 8i's hologram.

.. note::
    This step is required or else you will only be able to view the hologram within the Unity Editor

Find the camera object in Hierarchy > CameraParent > Main Camera and select it.

  .. image:: ../images/hierarchy-camera.png

With *Main Camera* seleced, In menu choose Component > 8i > HvrRender, this should add a *HvrRender* component to the camera:

  .. image:: ../images/main-camera-hvrrender.png

Save the scene by pressing Cmd+S.

Include HVR Data
------------------------------------------------------------
Before we can build the project, there's an extra step to do. Because we are using a *prefab* which means it will be dynamically loaded. We need to explicitly tell Unity to include the data before exporting.

First, right click on the Project window and create an asset of type HvrDataReference. You do it through Create > 8i > HvrDataReference.

  .. image:: ../images/create-datareference-asset.png


After creation, select the asset. Drag the president folder to its data field.

  .. image:: ../images/drag-hvr-to-datareference.png

Now we have created and configured the asset on disk. Now we need to include this asset in our scene. Right click in Hierarchy window and create an empty GameObject.

  .. image:: ../images/create-empty.png

With the empty object selected, attach a component of type HvrDataBuildInclude. You can find it in Component > 8i > HvrDataBuildInclude.

  .. image:: ../images/attach-databuildinclude.png

Finally drag the configured HvrDataReference asset to Data Reference field.

  .. image:: ../images/assign-data-reference.png

Save the scene.


Export and Build
------------------------------------------------------------
That's it! It's time to export Xcode project and deploy it to the device.

- Menu File > Build Settings, click *Player Settings* and make sure Metal is the first listed in the Inspector window.
- Click Build, select a folder to export the project. If everything went smooth, a Finder window should pop up and shows the exported Xcode project.
- Double click *Unity-iPhone.xcodeproj* and this should bring up Xcode.
- Configure Xcode project as follows. You need to pay attention to code signing `if you are new to it <https://help.apple.com/xcode/mac/current/#/dev60b6fbbc7>`_.
- After configuration, hit run:

  .. image:: ../images/xcode-settings.png

- Once the build is deployed and running, pick up your phone and walk around until a magenta ground is shown, which means you can put your holograms on.
- Tap the magenta ground to see how hologram works within AR world.

Where to go from now on
------------------------------------------------------------
- Check out our documentation on all the :ref:`Components` and how they interact with each other.
- Take a look at Apple HIG on AR: `https://developer.apple.com/design/human-interface-guidelines/ios/system-capabilities/augmented-reality/ <https://developer.apple.com/design/human-interface-guidelines/ios/system-capabilities/augmented-reality/>`_.
- Download 8i holograms from `https://8i.com/developers/downloads/ <https://8i.com/developers/downloads/>`_.
