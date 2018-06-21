Android
============================================================

Requirements
------------------------------------------------------------

**Supported Hardware**

For a list of supported device features and hardware requirements please see the `Hardware Requirements <https://drive.google.com/open?id=1kXDNg3hW7iKWFLR4SrQZykFQvrHJFYE-zu8xasTea3M>`_ 


**Including HVR Data with your Build**

Using the 8i Unity Plugin within an Android build requires that the HVR and/or HVRS frames are available on the device's local storage in a folder with read access.

When creating a build Unity will package any files that are placed within your project's StreamingAssets folder into a compressed file by default. This file is not able to be read by the 8i Unity Plugin. However the plugin provides support to extract HVR and HVRS data from this file onto the device's local storage.

This feature is available through the "HvrUnpackingScene" scene included with the plugin. This scene can be found at: "../8i/core/interface/platforms/android/scenes/".

"HvrUnpackingScene" uses the "LoadingSceneManager" component to unpack the data from the built OBB file. When opened this scene will scan the runing build and will extract any files that need to be exported. Once complete it will automatically load the next scene. This component can be easily modified for your project if you want to customize how the data is unpacked.

.. note::
    It is required to enable 'Split Application Binary' (`Read More <https://docs.unity3d.com/Manual/android-OBBsupport.html>`_) to use this feature.

If your project does not require it, this feature can be ignored by not using the "HvrUnpackingScene". In this case it assume that your HVR frames will already exist on the local storage or your application will download them.


**Google Play requirements**

The Google Play Store imposes a size limit of 100mb for APK files uploaded for distribution. To allow larger data to be shipped with an APK, Android supports OBB files, also known as Application Expansion Files (`Read More <https://developer.android.com/google/play/expansion-files>`_)

Unity also supports these files, via a player setting called "Split Application Binary". This option will export many of the project resources to an OBB, rather than packaging them with the APK. (`Read More <https://docs.unity3d.com/Manual/android-OBBsupport.html>`_)


Building
------------------------------------------------------------

If you are using the HvrUnpackingScene in your project a custom build step must be used. This step will scan the scenes in your project and copy any required HVR data into the project's StreamingAssets folder.

This menu can be found under the 8i/Android drop down menu at the top of the Unity Editor window.

If you are not using the "HvrUnpackingScene" feature, you can use the default Unity build menu.

Custom Build Menu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Build**

This step will copy any hvr data that is required by the project into the StreamingAssets directory and then build the project to a specified location.

Once the build step is complete, the files that were copied to the StreamingAssets directory will be cleared in order to reduce project bloat.


**Build and run**

Same as the 'Build' step, but will attempt to run the build on any attached devices once complete.


**Prepare Assets for Build**

This is a helper utility which will cpoy any required hvr data to the project's StreamingAssets folder, but will not build the project.

Once this step is complete, the project can be built again via the standard Unity build process. There is no need to run the "Prepare Assets for Build" option again unless any new hvr data is required or has been removed from the build.