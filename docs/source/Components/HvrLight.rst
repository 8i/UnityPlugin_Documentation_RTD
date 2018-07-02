HvrLight
============================================================

HvrLight enables HvrActors to be lit by and cast shadows from Unity Lights.

.. note::
    HvrLight only works when HvrRender's rendering mode is set to 'Standard'. In 'Direct' rendering mode, HvrActors will not be affected by this component.


Limitations
------------------------------------------------------------

* Directional Lights are only supported in Unity 2017.2 and greater
* Directional Lights shadow casting is not supported in the Unity Editor's Scene View
* HvrLights under point light will have shadow artifacts prior to Unity 5.6
* Some mobile devices will have limited shadow casting support
