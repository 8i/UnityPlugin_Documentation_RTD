HvrShaderSubroutine
============================================================

This component allows custom shaders to affect the HvrActor during the native plugin rendering step. This allows for complex effects to be written to affect the color, position and size of each voxel.

.. note::
    Not all examples in the below documentation have been written for all of the supported shader languages.

    You may be required to modify the shader code for your specific target platform.


Writing ShaderSubroutines
------------------------------------------------------------

Unlike Unity's ShaderLab shaders, ShaderSubroutines are not automatically converted to work for every BuildTarget. ShaderSubroutines must be written for each Graphics API that the effect needs to work on. 

The current supported shader languages are GLSL, HLSL and Metal.

==================   ===============
Graphics API         Shader Language
==================   ===============
Direct3D11           GLSL
OpenGLCore           HLSL         
OpenGLES3            HLSL        
Metal                METAL
==================   ===============

Code Blocks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For convenience, a single ShaderSubroutine Shader can contain all of the different languages. When the shader is loaded it will only compile the relevant sections.

BEGIN and END lines are used to specify a block of code for different languages

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

Control Functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Control Functions are the interface for how the HVR renderer enters a ShaderSubroutine and uses it to modify the rendering of a HvrActor.

The following code demonstrates how to write Control Functions for color, position and scale.

.. code-block:: none

    BEGIN_GLSL_VERTEX(VertexColor, VertexPosition, VertexScale)

        // Control  colour
        vec4 CalcVertexColour(vec4 colour : VERTEX_COLOUR, vec4 oPos : OPOS) : VERTEX_COLOUR
        {
            return colour;
        }

        // Control position
        vec4 VertexPosition(vec4 oPos : OPOS) : OPOS
        {
            return oPos;
        }

        // Control scale
        float VertexScale(float scale : VOXEL_SCALE, vec4 oPos : OPOS) : VOXEL_SCALE
        {
            return scale;
        }

    END_GLSL_VERTEX


Custom parameters and methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to support ShaderSubroutine Stacks, it is required to prefix all custom parameters and methods with "<ID>" (Without the quote marks).

This is necessary because when a ShaderSubroutine Stack is created all of the shaders in the stack are compiled into one large shader. If more than one of those shaders has a parameter with the same name, the parameter's value will not be able to be set differently for each shader. For example, if two shaders had the parameter "colour".

In order to address this, a unique ID is generated for each ShaderSubroutine and is used when the ShaderSubroutine Stack is created. This ID is used to replace the "<ID>" prefix and ensures that each shader has unique parameter and method names;

This example demonstrates how to write a shader which is compatible with ShaderSubroutine Stacks.

.. code-block:: none

    BEGIN_GLSL_VERTEX(VertexColor)

        uniform float _<ID>Saturation;

        float <ID>Luminance(vec3 c)
        {
            return dot(c, vec3(0.22, 0.707, 0.071));
        }

        vec4 CalcVertexColour(vec4 colour : VERTEX_COLOUR, vec4 oPos : OPOS) : VERTEX_COLOUR
        {
            float luminance = <ID>Luminance(colour.rgb);
            colour.r = lerp(colour.r, luminance, _<ID>Saturation);
            colour.g = lerp(colour.g, luminance, _<ID>Saturation);
            colour.b = lerp(colour.b, luminance, _<ID>Saturation);
            return colour;
        }

    END_GLSL_VERTEX

Examples
------------------------------------------------------------

Example 1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Set all voxels to be blue

.. code-block:: none

    BEGIN_GLSL_VERTEX(SetVertexColour)
        vec4 SetVertexColour(vec4 colour : VERTEX_COLOUR, vec4 oPos : OPOS) : VERTEX_COLOUR
        {
            colour.rgb = vec3(0, 0, 1);
            return colour;
        }
    END_GLSL_VERTEX

    BEGIN_HLSL_VERTEX(SetVertexColour)
        float4 SetVertexColour(float4 colour : VERTEX_COLOUR, float4 oPos : OPOS) : VERTEX_COLOUR
        {
            colour.rgb = float3(0, 0, 1);
            return colour;
        }
    END_HLSL_VERTEX

    BEGIN_METAL_VERTEX(SetVertexColour)
        float4 SetVertexColour(float4 colour : VERTEX_COLOUR) : VERTEX_COLOUR
        {
            colour.rgb = float3(0, 0, 1);
            return colour;
        }
    END_METAL_VERTEX

Example 2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Offset the position of all vertices vertically

.. code-block:: none

    BEGIN_GLSL_VERTEX(SetVertexPosition)
        vec4 SetVertexPosition(vec4 oPos : OPOS) : OPOS
        {
            if (oPos.y > 100)
                oPos.y += 30;
            return oPos;
        }
    END_GLSL_VERTEX

    BEGIN_HLSL_VERTEX(SetVertexPosition)
        float4 SetVertexPosition(float4 oPos : OPOS) : OPOS
        {
            if (oPos.y > 100)
                oPos.y += 30;
            return oPos;
        }
    END_HLSL_VERTEX

    BEGIN_METAL_VERTEX(SetVertexPosition)
        float4 SetVertexPosition(float4 oPos : OPOS) : OPOS
        {
            if (oPos.y > 100)
                oPos.y += 30;
            return oPos;
        }
    END_METAL_VERTEX


Example 3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following sets the color of all voxels to be blue, and sets their scale to 0 if they are below 1m in the data's object space.

.. code-block:: none

    BEGIN_GLSL_VERTEX(SetVertexColour, SetVertexScale)

        vec4 SetVertexScale(float scale : VOXEL_SCALE, vec4 oPos : OPOS) : VOXEL_SCALE
        {
            if (oPos.y < 100)
                return 0;
            return scale;
        }

        vec4 SetVertexColour(vec4 colour : VERTEX_COLOUR, vec4 oPos : OPOS) : VERTEX_COLOUR
        {
            colour.rgb = vec3(0, 0, 1);
            return colour;
        }
        END_GLSL_VERTEX

    BEGIN_HLSL_VERTEX(SetVertexColour, SetVertexScale)

        float4 SetVertexScale(float scale : VOXEL_SCALE, float4 oPos : OPOS) : VOXEL_SCALE
        {
            if (oPos.y < 100)
                return 0;
            return scale;
        }

        float4 SetVertexColour(float4 colour : VERTEX_COLOUR, float4 oPos : OPOS) : VERTEX_COLOUR
        {
            colour.rgb = float3(0, 0, 1);
            return colour;
        }

    END_HLSL_VERTEX

    BEGIN_METAL_VERTEX(SetVertexColour, SetVertexScale)

        float4 SetVertexScale(float scale : VOXEL_SCALE, float4 oPos : OPOS) : VOXEL_SCALE
        {
            if (oPos.y < 100)
                return 0;
            return scale;
        }

        float4 SetVertexColour(float4 colour : VERTEX_COLOUR) : VERTEX_COLOUR
        {
            colour.rgb = float3(0, 0, 1);
            return colour;
        }

    END_METAL_VERTEX
