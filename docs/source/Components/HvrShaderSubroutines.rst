HvrShaderSubroutines
===============

    This component allows custom shaders to affect the HvrActor during the native plugin rendering step. This allows for complex effects to be written to affect the color, position and size of each voxel.
    
    This is an advanced feature.

    TODO: Update documentation


How to Create
-------------

    1. Select your HVRActor from the Hierachy panel
    2. Below the HVRActor component click the 'Add Component' and search for 'HvrShaderSubroutine_Simple'
    3. Add it by highlighting it in the 'Add Component' window and pressing Enter, or clicking it.


What is a ShaderSubroutine?
---------------------------

    Unlike Unity's ShaderLab shaders, ShaderSubroutines are not automatically converted to work for every BuildTarget. ShaderSubroutines must be written for each Grahpics API that the effect needs to work on. 

    The current supported shader languages are GLSL, HLSL and Metal.

    ==================   ===============
    Graphics API         Shader Language
    ==================   ===============
    Direct3D11           GLSL
    OpenGLCore           HLSL         
    OpenGLES3            HLSL        
    Metal                METAL
    ==================   ===============

    For convinience, a single ShaderSubroutine Shader can contain all of the different languages. When the shader is compiled it will.
    This is done by adding BEGIN and END lines to mark the block of shader code for each language.

    For example

    .. code-block:: none

        BEGIN_GLSL_VERTEX
            # Code
        END_GLSL_VERTEX

        BEGIN_HLSL_VERTEX
            # Code
        END_HLSL_VERTEX

        BEGIN_METAL_VERTEX
            # Code
        END_METAL_VERTEX

Examples
--------

    **Set all voxels to be blue**

        .. code-block:: none

            BEGIN_GLSL_VERTEX(SetBlue)
                vec4 SetBlue(vec4 colour : VERTEX_COLOUR, vec4 oPos : OPOS) : VERTEX_COLOUR
                {
                    colour.rgb = vec3(0, 0, 1);
                    return colour;
                }
            END_GLSL_VERTEX

            BEGIN_HLSL_VERTEX(SetBlue)
                float4 SetBlue(float4 colour : VERTEX_COLOUR, float4 oPos : OPOS) : VERTEX_COLOUR
                {
                    colour.rgb = float3(0, 0, 1);
                    return colour;
                }
            END_HLSL_VERTEX

            BEGIN_METAL_VERTEX(SetBlue)
                float4 SetBlue(float4 colour : VERTEX_COLOUR) : VERTEX_COLOUR
                {
                    colour.rgb = float3(0, 0, 1);
                    return colour;
                }
            END_METAL_VERTEX
