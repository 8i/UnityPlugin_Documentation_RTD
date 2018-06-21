============================================================
HvrActorProjectorShadow
============================================================

Can be used in conjunction with a Projector component to project a texture onto a surface based on the bounds of an HvrActor. This is useful for creating blob shadows.

Parameters
------------------------------------------------------------

+-----------------+-----------+---------------------------------------------------------------------------------------------------------------+
| Parameter       | Type      | Function                                                                                                      |
+-----------------+-----------+---------------------------------------------------------------------------------------------------------------+
| Actor           | HvrActor  | The HvrActor which has an Asset. The bounds of this Asset will be used to drive the Projector components size |
+-----------------+-----------+---------------------------------------------------------------------------------------------------------------+
| Projector       | Projector | The Projector Component which will cast a blob shadow texture                                                 |
+-----------------+-----------+---------------------------------------------------------------------------------------------------------------+
| Size Multiplier | Float     | Used to increase or decrease the scale of the blob shadow texture                                             |
+-----------------+-----------+---------------------------------------------------------------------------------------------------------------+