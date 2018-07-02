HvrShaderSubroutine
============================================================

This component allows custom shaders to affect the HvrActor during the native plugin rendering step. This allows for complex effects to be written to affect the color, position and size of each voxel.

A HvrShaderSubroutine component can be though of like Unity's material system. Where you have a shader with some values that can be changed and this changes how a mesh renders.

In the case of HvrShaderSubroutines, the shader suborutine code is executed as a post process step during the native rendering of the voxels. 

Multiple HvrShaderSubroutine components can be added to a HvrActor in order to apply multiple post processing effects. The order which each subroutine executes is based on the order of the component as it is attached to the HvrActor's GameObject from top to bottom. This is known as a *stack*.



.. note::
    Not all examples in the below documentation have been written for all of the supported shader languages.

    You may be required to modify the shader code for your specific target platform.

Writing Shader Subroutines
------------------------------------------------------------

Unlike Unity's ShaderLab shaders, shader subroutines are not automatically converted to work for every BuildTarget. Shader subroutines must be written for each Graphics API that the effect needs to work on.

The current supported shader languages are GLSL, HLSL and Metal.



==================   =============================================   =============================================
Graphics API         Shader Language                                 Language Reference
==================   =============================================   =============================================
Direct3D11           HLSL                                            `Windows HLSL Shader Reference <https://docs.microsoft.com/en-us/windows/desktop/direct3dhlsl/dx-graphics-hlsl-reference>`_
OpenGLCore           GLSL                                            `OpenGL Reference <https://www.khronos.org/registry/OpenGL-Refpages/gl4/>`_
OpenGLES3            GLSL                                            `OpenGLES Reference <https://www.khronos.org/opengles/sdk/docs/manglsl/docbook4/>`_
Metal                Metal Shading Language                          `Apple Metal Shader Specification <https://developer.apple.com/metal/Metal-Shading-Language-Specification.pdf/>`_
==================   =============================================   =============================================

Code Blocks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For convenience, a single shader subroutine file can contain all of the different shader languages. When the file is loaded it will only compile the relevant sections.

BEGIN and END lines are used to specify a block of code for different languages.

In addition, each type of shader subroutine corresponds to one shader stage: either the vertex or fragment (pixel) shader stage.
A code block will have a ``_VERTEX`` or ``_FRAGMENT`` suffix depending on the types of shader subroutines it contains.
The available types of shader subroutines are discussed later in this page.

For example:

.. code-block:: none

    BEGIN_GLSL_VERTEX
        # Code
    END_GLSL_VERTEX

    BEGIN_GLSL_FRAGMENT
        # Code
    END_GLSL_FRAGMENT

    BEGIN_HLSL_VERTEX
        # Code
    END_HLSL_VERTEX

    BEGIN_METAL_VERTEX
        # Code
    END_METAL_VERTEX

Syntax and Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Shader subroutines can control several properties of HvrActor rendering.

A code block consists of a collection of subroutines. Each subroutine controls one feature of rendering,
such as the object-space position of the vertex, the vertex or fragment colour, or the scale factor applied to the voxel.

A subroutine is implemented as a function in the relevant shader language. The feature (position, colour, etc.) controlled by the
subroutine is declared using an **output semantic**. Each shader subroutine may have several input parameters, which have values provided
by the HVR Renderer, based on specified **input semantics**.

Input and output semantics are declared using an extended shader language syntax, which is similar to the way that HLSL uses semantics.
The HVR Renderer parses the extended syntax, processes the semantic declarations and outputs standard shader code.

An example is given below, demonstrating modification of the vertex colour, object-space position and voxel scale.
Note that the names of all subroutines need to be declared in a comma-separated list in parentheses after the code block BEGIN tag.

.. code-block:: none

    BEGIN_GLSL_VERTEX(CalcVertexColour, CalcVertexPosition, CalcVertexScale)

        // Control colour
        vec4 CalcVertexColour(vec4 colour : VERTEX_COLOUR, vec4 oPos : OPOS) : VERTEX_COLOUR
        {
            // Example: This makes the colour darker.
            // The 'oPos' parameter is not used in this example,
            // but could be included in the calculation, i.e. to modify
            // the colour based on the position.
            return vec4(0.5 * colour.rgb, colour.a);
        }

        // Control position
        vec4 CalcVertexPosition(vec4 oPos : OPOS) : OPOS
        {
            // Example: This moves the vertex vertically upwards.
            return vec4(oPos.x, oPos.y + 1.0, oPos.z, oPos.w);
        }

        // Control scale
        float CalcVertexScale(float scale : VOXEL_SCALE) : VOXEL_SCALE
        {
            // Example: This doubles the vertex size.
            return 2.0 * scale;
        }

    END_GLSL_VERTEX

In the example above, the CalcVertexColour subroutine has VERTEX_COLOUR specified as its output semantic,
so the HVR Renderer uses its return value for the output vertex colour. Its input semantics are VERTEX_COLOUR and
OPOS, so the parameters corresponding to these semantics will be filled in by the HVR Renderer with the original vertex position and colour.

The other two shader subroutines (CalcVertexPosition and CalcVertexScale) work similarly.

A list of semantics and their functionality is given below. Each of these can be used as either input or output semantics.
Each subroutine must be declared in the appropriate code block (VERTEX or FRAGMENT) based on the shader stage of its output semantic.

==================   =============== =============== ===============
Semantic             Type            Shader Stage    Description
==================   =============== =============== ===============
OPOS                 vec4 / float4   Vertex          Object-space coordinates of the current vertex.
VERTEX_COLOUR        vec4 / float4   Vertex          The colour of the current vertex.
FRAGMENT_COLOUR      vec4 / float4   Fragment        The colour of the current fragment (pixel).
VOXEL_SCALE          float           Vertex          A scaling factor used to modify the size of the voxel (1.0 = original scale).
==================   =============== =============== ===============

**Important note:** Each subroutine **must** be declared after the BEGIN tag in the code block header.
This takes the form of a comma-separated list of function names in parentheses: for example, ``BEGIN_GLSL_VERTEX(CalcVertexColor, CalcVertexPosition, CalcVertexScale)`` in the example above. If a subroutine is not declared, it will be ignored by the HVR Renderer.

Helper or utility functions without input or output semantics should **not** be declared in the code block header.

Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most shader subroutines are likely to need parameters provided by the application; for example, the current time, in
effects that are dynamic or animated. These correspond to ``uniform`` variables in GLSL and constant buffers in HLSL.

The name of each variable, struct or cbuffer should be prefixed by <ID> (this is discussed in the 'Shader Subroutine Stacks' section).

In GLSL, shader parameters can be declared as global uniform variables:

.. code-block:: none

    uniform float _<ID>CurrentTime;

Similarly, in HLSL, global cbuffers can be declared:

.. code-block:: none

    cbuffer _<ID>ShaderParams
    {
        float _<ID>CurrentTime;
    }

In the Metal shading language, shader inputs cannot be declared as global variables. Instead, a ``struct`` of parameters must
be defined; this can then be declared as a parameter to a shader subroutine using the special semantic SHADER_UNIFORMS. For example:

.. code-block:: none

    struct _<ID>ShaderParams
    {
        float _<ID>CurrentTime;
    };

    float4 CalcVertexColour(float4 colour : VERTEX_COLOUR, _<ID>ShaderParams uniforms : SHADER_UNIFORMS) : VERTEX_COLOUR
    {
        return float4(colour.rgb * (sin(uniforms._<ID>CurrentTime) * 0.5 + 0.5), colour.a);
    }

For Metal, textures should be declared in a separate ``struct`` and used with the SHADER_TEXTURES semantic. For example:

.. code-block:: none

    struct _<ID>ShaderTextures
    {
        texture2d<float> _<ID>RGLookupTable;
    };

    float4 CalcVertexColour(float4 colour : VERTEX_COLOUR, _<ID>ShaderTextures textures : SHADER_TEXTURES) : VERTEX_COLOUR
    {
        // Uses the R and G components of the original colour as texture coordinates.
        constexpr sampler textureSampler(mag_filter::linear, min_filter::linear);
        return textures._<ID>RGLookupTable.sample(textureSampler, colour.rg);
    }

Stacks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In order to support shader subroutine stacks, it is required to prefix all custom parameters and methods with "<ID>" (without the quote marks).

This is necessary because when a shader subroutine stack is created, all of the shaders in the stack are compiled into one large shader. If more than one of those shaders has a parameter with the same name, the parameter's value will not be able to be set differently for each shader. For example, if two shaders had the parameter "colour" when you try to set each to a different value it would affect both paramters in the shader.

In order to address this, a unique ID is generated for each file and is used when the shader subroutine stack is created. This ID is used to replace the "<ID>" prefix and ensures that each shader has unique parameter and method names.

This example demonstrates how to write a shader which is compatible with shader subroutine stacks.

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

**Example 1**

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

**Example 2**

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


**Example 3**

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
