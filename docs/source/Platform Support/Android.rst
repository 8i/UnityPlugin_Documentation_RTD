Android
=======


Requirements
------------

    Supported Hardware
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


    For a list of supported device features and hardware requirements please see the `Hardware Requirements <https://drive.google.com/open?id=1kXDNg3hW7iKWFLR4SrQZykFQvrHJFYE-zu8xasTea3M>`_

    Including HVR Data with your Build
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    Using the 8i Unity Plugin within an Android build requires that the HVR and/or HVRS frames are available on the device's local storage in a folder with read access.

    When creating a build Unity will package any files that are placed within your project's StreamingAssets folder into a compressed file by default. This file is not able to be read by the 8i Unity Plugin. However the plugin provides support to extract HVR and HVRS data from this file onto the device's local storage.

    This feature is available through the "HvrUnpackingScene" scene included with the plugin. This scene can be found at: "../8i/core/interface/platforms/android/scenes/".

    "HvrUnpackingScene" uses the "LoadingSceneManager" component to unpack the data from the built OBB file. When opened this scene will scan the runing build and will extract any files that need to be exported. Once complete it will automatically load the next scene. This component can be easily modified for your project if you want to customize how the data is unpacked.

    .. note::
        It is required to enable 'Split Application Binary' (`Read More <https://docs.unity3d.com/Manual/android-OBBsupport.html>`_) to use this feature.

    If your project does not require it, this feature can be ignored by not using the "HvrUnpackingScene". In this case it assume that your HVR frames will already exist on the local storage or your application will download them.


    Google Play requirements
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    The Google Play Store imposes a size limit of 100mb for APK files uploaded for distribution. To allow larger data to be shipped with an APK, Android supports OBB files, also known as Application Expansion Files (`Read More <https://developer.android.com/google/play/expansion-files>`_)

    Unity also supports these files, via a player setting called "Split Application Binary". This option will export many of the project resources to an OBB, rather than packaging them with the APK. (`Read More <https://docs.unity3d.com/Manual/android-OBBsupport.html>`_)


Building
--------

    If you are using the HvrUnpackingScene in your project a custom build step must be used. This step will scan the scenes in your project and copy any required HVR data into the project's StreamingAssets folder.

    This menu can be found under the 8i/Android drop down menu at the top of the Unity Editor window.

    If you are not using the "HvrUnpackingScene" feature, you can use the default Unity build menu.

    Custom Build Menu
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
        **Build**
            This step will copy any hvr data that is required by the project into the StreamingAssets directory and then build the project to a specified location.

            Once the build step is complete, the files that were copied to the StreamingAssets directory will be cleared in order to reduce project bloat.


        **Build and run**
            Same as the 'Build' step, but will attempt to run the build on any attached devices once complete.


        **Prepare Assets for Build**
            This is a helper utility which will cpoy any required hvr data to the project's StreamingAssets folder, but will not build the project.

            Once this step is complete, the project can be built again via the standard Unity build process. There is no need to run the "Prepare Assets for Build" option again unless any new hvr data is required or has been removed from the build.

Troubleshooting
---------------

    HvrActors are not rendering
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        *Main camera does not have a HvrRender component attached*
            A common mistake is to not attach a HvrRender component to the main rendering camera in the scene

        *The Graphics API may not be supported*
            Make sure that under the PlayerSettings that the targeting GraphicsAPI is GLES3 and that your device supports GLES3.

        *HvrActors using PointBlend are not rendering*
            The PointBlend render method does not work on some older mobile devices.

        *HvrRender fails to load Standard shaders*
            There is a known issue that on some devices, that when the 'Split Application Binary' option is enabled, the HvrRender component may not be able to load the Standard shaders. Go to 'Edit/Project Settings/Player' and make sure that the option 'Split Application Binary' is not checked.

        *Issues with Google Daydream builds*
            The current release of the Unity Editor for DayDream ( 5.4.2f2-GVR13 ), will not use the AndroidManifest.xml file that is provided within the plugin. This means the hvr frames will not be extracted or read from the devices storage upon installing the build.

            It appears as though this build of the Unity Editor has a bug where it will not use and AndroidManifest.xml file that is not located at this specific location `project_name/Assets/Plugins/Android/AndroidManifest.xml`

            Until this is fixed within Unity, it is recommend to copy the AndroidManifest file from this location `8i/core/platform support/android/plugins/AndroidManifest.xml` to `project_name/Assets/Plugins/Android/AndroidManifest.xml`

    Black screen when loading the app
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        *Project was not built using the Custom Build Menu*
            If your project is using the "HvrUnpackingScene", it is required to create your build using the Custom Build Menu mentioned above.

        *Project using the "HvrUnpackingScene" and was built using the custom build menu*
            Check the Editor Build Settings and ensure that there is a second scene directly after the "HvrUnpackingScene".

    For all other issues, please contact us for support.