============================================================
HvrActor3DMask
============================================================

This components allows you to mask sections of an HvrActor.

It works by using HvrActor3DMaskObject to mark areas which should be affected by the masking.

This component stores an array of HvrActor3DMaskObject. Each HvrActor3DMaskObject is applied in the order within the array. For example, a head of an HvrActor can be isolated by creating a 'Subtractive' mask which covers the entire HvrActor, then creating a 'Additive' mask which only surrounds the head of the HvrActor. Placing the 'Subtractive' mask first, and the 'Additive' mask second will cause only the head to be visible.

.. note::
    This effect is done in 2D. This means masking out a hand in front of a face will remove the hand, but the face will not be visible. Rotate the camera within the included example scene to see a demonstration of this.

Parameters
------------------------------------------------------------

+-----------+-------+----------------------------------------------+
| Parameter | Type  | Function                                     |
+-----------+-------+----------------------------------------------+
| Objects   | Array | An array of HvrActor3DMaskObject components. |
+-----------+-------+----------------------------------------------+

============================================================
HvrActor3DMaskObject
============================================================

Used by HvrActor3DMask to mark areas to be affected when masking a HvrActor

The mask object can be either a sphere or a box. It can be additive or subtractive.

Parameters
------------------------------------------------------------

+----------+--------+---------------------------------------+
| Property | Type   | Function                              |
+----------+--------+---------------------------------------+
| Options  | Sphere | Mask using a sphere                   |
+----------+--------+---------------------------------------+
|          | Box    | Mask using a cube                     |
+----------+--------+---------------------------------------+
| Additive | Bool   | Is this mask additive or subtractive? |
+----------+--------+---------------------------------------+