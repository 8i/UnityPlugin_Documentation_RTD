MacOS
============================================================

Support
------------------------------------------------------------

==================   ======================================================================================================
Architecture         - Intel x64
Graphics API         - OpenGlCore
                     - Metal
==================   ======================================================================================================

Requirements
------------------------------------------------------------

* A Mac is required to generate the XCode project
* XCode 9.3 is the minimum required version

==================   ======================================================================================================
CPU                  - Intel
                     - AMD
                     - 64bit Architecture
GPU                  - ATi 
                     - Nvidia
                     - Support for OpenGL
RAM                  - Recommended >2GB
OS                   - El Capitan
                     - Sierra
                     - High Sierra
                     - Mojave
Min Spec             - El Capitan
                     - MacBook Pro (Retina, 13-inch, Mid 2014)
                     - 2.6GHz dual-core Intel Core i5 processor
                     - 8GB of 1600MHz DDR3L onboard memory
                     - Intel Iris Graphics
                     - https://support.apple.com/kb/sp703
==================   ======================================================================================================

Building
------------------------------------------------------------

DLL initialisation
~~~~~~~~~~~~~~~~~~
You need to put 8i/core/platforms/common/scenes/HvrPluginInit.scene as the first scene in your build. You can also use 8i->Project Tips to help you.
