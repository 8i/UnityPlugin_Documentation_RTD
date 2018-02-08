HvrActor
===========

    This component provides the ability to create and play HVR data within Unity. It offers control over how the data is played and how it is rendered.

How to Create
-------------

    1. Right click in Unity Scene Hierarchy
    2. Select ‘8i/Create HVR Actor’

Parameters
-------------

    **Data**

        **Mode**
            - Auto
                - Drag and Drop a file or folder from the Project window onto this slot.
                - Any referenced data is included when a build is created.
            - Path
                - A direct path to a file, folder or network location.
                - Any data specified will not be included in a build. 

        **Play**
            Play any AssetInterface that is created by this HvrActor.

        **Loop**
            Set any AssetInterface created by this HvrActor to loop.

        **Seek Time**
            The time any created AssetInterface should seek to.

    **Renderer**
                
        **Material**
            The material the HvrActor will render with if using the 'Standard' RenderMethod.

        **Render Method**
                The RenderMethod affects how the HvrActor is rendered before any shaders or effects are applied.

                    Options
                        - FastCubes
                            - Renders the actor using cubes
                            - Optimized for performance
                            - Subjectively provides the best looking rendering
                            - On mobile platforms depth is based on cube center rather than per-fragment. 
                        - CorrectCubes
                            - Identical results to FastCubes, but has correct depth and z-sorting for cubes on all platforms
                            - Not as performant compared to FastCubes
                        - PointSprite
                            - Renders the actor with screen aligned squares
                        - PointSpriteDepth
                            - Only renders depth, color is ignored
                            - Similar performance to PointSprite
                        - PointBlend
                            - Renders the actor with smooth points which soften the look of the actor
                            - Most expensive RenderMethod by a factor of two compared to 

        **Use Lighting**
            Should this HvrActor be influenced by HvrLights?

        **Receive Shadows**
            Whether the HvrActor will receive shadows when used alongside the HvrShadowRender component. 
            This feature is still in preview and is not recommended for production use.
            Enabled by default.

        **Cast Shadows**
            Whether the HvrActor will cast shadows when used alongside the HvrShadowRender component.
            This feature is still in preview and is not recommended for production use.
            Enabled by default.

    **Occlusion Culling**

        Whether when rendering the HvrActor the HvrRender should use Unity’s Occlusion Culling system to check whether the object is visible. A wireframe sphere will be drawn in the Editor SceneView to show the size and location of the bounding sphere which is used to check the visibility of the HvrActor.

        Options
            - Occlusion Radius Offset
                - Allows you to offset the size of the bounding sphere radius.