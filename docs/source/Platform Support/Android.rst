Android
============================================================

Support
------------------------------------------------------------

==================   ======================================================================================================
Architecture         - ARMv7, ARM64
Graphics API         - OpenGLES3
==================   ======================================================================================================

Requirements
------------------------------------------------------------

==================   ======================================================================================================
CPU                  - Requires ARMv7 or ARM64
                     - ARMv7 Requires NEON (supported by almost all phones that are fast enough to run HVR content)
GPU                  - Requires OpenGLES3
RAM                  - Recommended >512MB ( Requirements vary based on application and data quality )
OS                   - KitKat              4.4 – 4.4.4
                     - Lollipop            5.0 – 5.1.1
                     - Marshmallow         6.0 – 6.0.1
                     - Nougat              7.0 – 7.1.2
                     - Oreo                8.0 – 8.1
                     - Newer Versions
Min Spec             - API Level 19 ( KitKat  )
==================   ======================================================================================================


Building
------------------------------------------------------------

In order to include HVR data with your build custom build step must be used. This step will scan the scenes in your project and copy any required HVR data into the project's StreamingAssets folder.

This menu can be found under the 8i/Android drop down menu at the top of the Unity Editor window.

Custom Build Menu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

====================================   ================================================================================================================================================================================
Build                                  This step will copy any hvr data that is required by the project into the StreamingAssets directory and then build the project to a specified location

                                       Once the build step is complete, the files that were copied to the StreamingAssets directory will be cleared in order to reduce project bloat
Build and Run                          Same as the 'Build' step, but will attempt to run the build on any attached devices once complete.
Prepare Assets for Build               This is a helper utility which will copy any required hvr data to the project's StreamingAssets folder, but will not build the project

                                       Once this step is complete, the project can be built again via the standard Unity build process.

                                       There is no need to run the "Prepare Assets for Build" option again unless any new hvr data is required or has been removed from the build.
====================================   ================================================================================================================================================================================

Unpacking Hvr Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to load HVR Data on Android, the data must be available on the device's local storage in a folder with read access.

This section can be ignored if your project does not need to load data off local storage, or you use another way of bundling and extracting HVR data.

When creating a build, Unity will package any files that are placed within your project's StreamingAssets folder into a compressed file by default. This compressed file is not able to be read by the 8i Unity Plugin. However the plugin provides support to extract HVR and HVRS data from this file onto the device's local storage.

This feature is available through the "HvrUnpackingScene" scene included with the plugin.

"HvrUnpackingScene" uses the "LoadingSceneManager" component to unpack the data from the built APK/OBB file. When opened this scene will scan the runing build and will extract any files that need to be exported. Once complete it will automatically load the next scene. This component can be easily modified for your project if you want to customize how the data is unpacked.

This scene can be found at: "../8i/core/interface/platforms/android/scenes/".

.. note::
    It is strongly recommended to enable 'Split Application Binary' (`Read More <https://docs.unity3d.com/Manual/android-OBBsupport.html>`_) to dodge the size limit placed by Google Play. Packing everything into one APK is allowed but not recommended.

Google Play requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Google Play Store imposes a size limit of 100mb for APK files uploaded for distribution. To allow larger data to be shipped with an APK, Android supports OBB files, also known as Application Expansion Files (`Expansion Files <https://developer.android.com/google/play/expansion-files>`_)

Unity also supports these files, via a player setting called "Split Application Binary". This option will export many of the project resources to an OBB, rather than packaging them with the APK. (`Split Application Binary <https://docs.unity3d.com/Manual/android-OBBsupport.html>`_)

Google Play on 64-bit apps
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Starting August 1, 2019, Google Play only allows apps have support of 64-bit architecture to be able to publish. That means developer can only choose Unity version that supports Android 64bit build. Only Unity 2018.3 and newer versions (as an exception, 2017.4 back-ported the ARM64 support)have good support of ARM64 so you want to stick with those versions.

To build 64-bit app, you also need to change Unity runtime from Mono to compiled IL2cpp. See `here <https://blogs.unity3d.com/2019/03/05/android-support-update-64-bit-and-app-bundles-backported-to-2017-4-lts/>`_ for more information.