PatRender
============================================================

| This component is responsible for the actual rendering within Unity. It is assigned a PatActor to use as its render source.
| Once assigned to a particular actor, this runs automatically based on frame availability coming from the PatAsset.
| If used outside of the PatAsset prefab, the component requires that a Unity MeshFilter and MeshRenderer are attached to the same object, along with the provided PatPlayerMaterial and PatPlayerShader. The latter can be modified to provide custom rendering of the underlying texture/mesh data if desired.

