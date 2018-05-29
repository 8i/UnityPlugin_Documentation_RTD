HvrLight
============================================================

HvrLight enables HvrActors to be lit by Unity Lights.

.. note::
    HvrLight only works when HvrRender's rendering mode is set to 'Standard'. In 'Direct' rendering mode, HvrActors will not be affected by this component.

Limitations
------------------------------------------------------------

* HvrLights under point light will have shadow artifacts prior to Unity 5.6
* Some mobile devices will have limited shadow casting abilities
