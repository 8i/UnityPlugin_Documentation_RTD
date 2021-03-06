Troubleshooting
============================================================

Recommended Project Settings
------------------------------------------------------------

The 'Recommended Project Settings' window can found through the '8i' menu at the top of the Unity Editor.

This window will prompt you if it detects an issue with your project settings, it can also fix common problems with a single click.

Cannot create HVR components
------------------------------------------------------------

- Check that the plugin was fully extracted from the '8i Unity Plugin' zip into your Project's Asset folder
- Check the Recommended Project Settings window for help ( Found under the '8i/Recommended Project Settings' menu at the top of the Unity Editor )
- If you recently updated the plugin, make sure that you closed the Unity Editor adding the new plugin folder to your project. The Unity Editor can lock the native binaries included in the plugin and block you from writing over them.
- Make sure the Unity version is compatible with this version of the plugin.
- Check the console to see whether there are any errors blocking Unity from compiling the plugin.

Performance is low
------------------------------------------------------------

**Use lower resolution data**

It is recommended using this table when choosing which resolution to use for your application.

==================   ==   ======   ========================================
Resolution           PC   Mobile   About
==================   ==   ======   ========================================
1,500,000            Y    N        Not recommended for mobile
800,000              Y    Y        High end mobile device is required
600,000              Y    Y 
400,000              Y    Y 
==================   ==   ======   ========================================

The filename of the hvr file will tell you the resolution. This number represents the density of the data and the overall quality.

The naming convention is [NAME]_[Resolution]_[FrameNumber].[Extension]

Most files follow this naming convention. If you are not sure, please send an email to your contact at 8i.

Ie: BOXER_200_tc_v01_800000_001009.hvr will be:

==================   ================
Name                 BOXER_200_tc_v01
Resolution           800,000
Frame number         1009
==================   ================

**Change the HvrActor render method**

It is recommended to use the 'FastCubes' render method in order to improve performance.


**Change the HvrRender render mode**

The 'Direct' render mode provides the best performance and memory usage.

There are downsides of this method which are outlined in the HvrRender section of this documentation.


**Mobile Performance Tips**

- Point Count
    As mobile platforms perform much slower than desktop systems it is recommended that hvr frames with point counts of 600k or less are used, with the recommended point count being around 300k.

- Rendering Settings
    It is recommended to use the ‘Direct’ HvrRender render method on Android as it is the best performing renderer.

- Render Method
    It is recommended to use the 'Point Sprite' render method in all cases. It is the best performing render method provided.
    
    The current alternative, 'Point Blend' does not work on some older devices, and is around twice as expensive to render.


HVR Actors are not rendering
------------------------------------------------------------

**Common Problems**

- The Main Camera does not have a HvrRender component attached
    A common mistake is to not attach a HvrRender component to the main rendering camera in the scene

- My HvrActor Prefabs are not rendering
    Please see the `HvrDataBuildInclude <Components/HvrDataBuildInclude.html>`_ component page for more information about this problem.

**Android**

- The Graphics API may not be supported
    Make sure that under the PlayerSettings that the targeting GraphicsAPI is GLES3 and that your device supports GLES3.

- HvrActors using PointBlend are not rendering
    The PointBlend render method does not work on some older mobile devices.

- HvrRender fails to load Standard shaders
    There is a known issue that on some devices, that when the 'Split Application Binary' option is enabled, the HvrRender component may not be able to load the Standard shaders. Go to 'Edit/Project Settings/Player' and make sure that the option 'Split Application Binary' is not checked.

- Issues with Google Daydream builds
    The current release of the Unity Editor for DayDream ( 5.4.2f2-GVR13 ), will not use the AndroidManifest.xml file that is provided within the plugin. This means the hvr frames will not be extracted or read from the devices storage upon installing the build.
    
    It appears as though this build of the Unity Editor has a bug where it will not use and AndroidManifest.xml file that is not located at this specific location `project_name/Assets/Plugins/Android/AndroidManifest.xml`
    
    Until this is fixed within Unity, it is recommend to copy the AndroidManifest file from this location `8i/core/platform support/android/plugins/AndroidManifest.xml` to `project_name/Assets/Plugins/Android/AndroidManifest.xml`

- Black screen when loading the app
    - Project was not built using the Custom Build Menu
        If your project is using the "HvrUnpackingScene", it is required to create your build using the Custom Build Menu mentioned above.

    - Project using the "HvrUnpackingScene" and was built using the custom build menu
        Check the Editor Build Settings and ensure that there is a second scene directly after the "HvrUnpackingScene".
        
- Android failing to extract data from OBB file
    Some devices do correctly allow the OBB file to be copied to the device when using the "Build and Run" option in Unity, and in some cases will silently fail to update the OBB when the project is built. If this occurs, the OBB file will need to be manually copied to the development device.

    So far only the Samsung Galaxy Note 5 has been observed with this issue. 
