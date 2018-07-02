HvrRender
============================================================

In order to render HvrActors a HvrRender component must be attached to a Camera.

There are two different render modes that the HvrRender component can be set to. 

**Standard**

This mode renders using Unity's standard rendering loop and allows for custom materials, lighting and effects. This mode attempts to fit invisibly into Unity's render loop and work as expected and allow HvrActors to be customized like any other normal mesh rendering.

**Direct**

Renders directly into the Unity framebuffer. This mode is generally faster than Standard, but comes with the trade off that custom materials, lighting and post effects are not supported.
    

Parameters
------------------------------------------------------------

+-----------+----------+-----------------------------------------------------------------------------------------------------+
| Parameter | Type     | Function                                                                                            |
+-----------+----------+-----------------------------------------------------------------------------------------------------+
| Mode      | Standard | Renders HvrActor within Unity's render loop                                                         |
|           |          | This allows for custom materials and effects to affect how an HvrActor is rendered                  |
+-----------+----------+-----------------------------------------------------------------------------------------------------+
|           | Direct   | Renders directly into Unity's framebuffer                                                           |
|           |          | Using this option will ignore all custom materials and effects that are currently set on a HvrActor |
+-----------+----------+-----------------------------------------------------------------------------------------------------+

.. note::
    ShaderSubroutines effects are compatible with both Standard and 'Direct' mode.