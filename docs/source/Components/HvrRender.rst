============================================================
HvrRender
============================================================

In order to render HvrActors a HvrRender component must be attached to a Camera.

There are three different render modes that the HvrRender component can be set to. While Standard is the default and recommended mode, there are two others which each have different properties and performance costs.
    

Parameters
------------------------------------------------------------

+-----------+----------+-----------------------------------------------------------------------------------------------------+
| Parameter | Type     | Function                                                                                            |
+-----------+----------+-----------------------------------------------------------------------------------------------------+
| Mode      | Standard | Renders each HvrActor individually within Unity's render loop                                       |
|           |          | This allows for custom materials and effects to affect how an HvrActor is rendered                  |
+-----------+----------+-----------------------------------------------------------------------------------------------------+
|           | Direct   | Renders directly into Unity's framebuffer                                                           |
|           |          | Using this option will ignore all custom materials and effects that are currently set on a HvrActor |
+-----------+----------+-----------------------------------------------------------------------------------------------------+

.. note::
    ShaderSubroutines effects are compatible with both Standard and 'Direct' mode.