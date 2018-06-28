============================================================
HvrDataBuildInclude and HvrDataReference
============================================================

The HvrDataBuildInclude component and HvrDataReference can be used to include files and folders from your Project which are not assigned to HvrActors.

This is useful in situations where your project is creating HvrActors at runtime and you do not want to manually copy data from your project to your build.

During the build process the 8i Unity Plugin will scan any scenes that are to be built and check the components to find any HvrActors which are using the 'Reference' Data Mode. It will also search for HvrDataBuildInclude components which have a HvrDataReference assigned. If any are found, the data that is referenced will be will be copied to the build folder so the built application can load them.

.. note::
    When building for Android the build process described above is not automatic and requires a custom build process. Please see the Android Platform page for more information about this.


HvrDataBuildInclude
------------------------------------------------------------

The HvrDataBuildInclude is a component which a HvrDataReference can be assigned to.

To use this component, attach it to a GameObject within your scene and assign a HvrDataReference to the 'Data Reference' slot.

+-----------------+-----------+-------------------------------------------------------------------------+
| Parameter       | Type      | Function                                                                |
+-----------------+-----------+-------------------------------------------------------------------------+
| Data Reference  | Object    | A Object slot which a HvrDataReference can be assigned to               |
+-----------------+-----------+-------------------------------------------------------------------------+

HvrDataReference
------------------------------------------------------------

The HvrDataReference contains an list of references to files or folders from your project.

It can be created by either opening the 'Assets' menu at the top of the screen, or in the 'Create' context menu when right clicking in your Project window and navigating to 'Create/8i/HvrDataReference'

To add a reference to the List

- Click the 'Plus' icon in the bottom right.
- Drag and Drop a file or folder from your project into the 'Data' slot OR click the circle icon to open a window to search your entire project.

Because the references are created using Unity's project GUID system moving any referenced files and folders will not break the reference.

+-----------------+-----------+-------------------------------------------------------------------------+
| Parameter       | Type      | Function                                                                |
+-----------------+-----------+-------------------------------------------------------------------------+
| Data            | List      | A expandable list of GUID references to files or folders in the project |
+-----------------+-----------+-------------------------------------------------------------------------+
