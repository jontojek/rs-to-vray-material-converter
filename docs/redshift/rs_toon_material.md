---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Material+Toon.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Toon Material
captured: 2026-04-09
tags: [redshift, material, shader, toon, NPR, cel-shading, raw]
---

Shaders > Material Shaders > Toon Material

Toon Material

Overview

The Toon Material is Redshift's non-photorealistic rendering shader. It allows for great flexibility and creative freedom in designing cel shaded and cartoon style looks. It is one of three shaders that make up Redshift's core offering of non-photorealistic tools. The Toon Material is used as the primary shading element to create stylized cel shaded looks, the Contour shader is used to create outlines around your objects, and the Tonemap Pattern texture adds a screen space pattern to your shading to mimic a halftone dot effect and others.

Basic Toon Setup

The Toon Material works by remapping lighting intensity values through a tonemap curve or ramp, producing distinct bands of flat color rather than smooth shading gradients.

Tone Mapping and Lighting

What is Tone Mapping?
Tone mapping in the context of the Toon shader is the process of converting continuous lighting values into discrete flat color regions. The tonemap curve controls how light intensity is quantized into the characteristic cel-shaded bands.

Light Type
The Toon material responds to all standard Redshift lights. The light type affects the shape and hardness of the shading bands produced.

Light Intensity
The intensity of lights in the scene directly affects the position of shading bands on the toon-shaded surface. Consistent light intensities are important for predictable toon results.

Connecting a Tonemap
A Tonemap curve or ramp node is connected to drive the band quantization. This is the primary artistic control for the toon look.

Troubleshooting
If shading bands appear noisy or inconsistent, check that GI is disabled or set to a low sample count, as GI can interfere with the clean flat shading bands expected in NPR rendering.

General Properties

Base

Base Color
The primary flat color of the toon-shaded surface.

Base Weight
Multiplier for the base color influence.

Tonemap
A ramp or curve node that remaps incoming lighting intensity to output shading values. This is what creates the characteristic banded cel-shaded look.

Shadow Color
The color of shaded/shadowed regions of the surface.

Reflection

Reflection Weight
Controls the intensity of specular highlights on the toon surface.

Reflection Color
The color of the toon specular highlight.

Reflection Roughness
Controls the size/spread of the specular highlight. Lower values produce a tighter, harder highlight.

Tonemap (Reflection)
A separate tonemap ramp controlling how the specular highlight is quantized.

Rim

Rim Weight
Controls the intensity of the rim/backlight effect.

Rim Color
The color of the rim highlight.

Rim Tonemap
A tonemap ramp controlling how the rim light is quantized.

Emission

Emission Color
Self-illumination color for the toon material.

Emission Weight
Multiplier on the emission.

Geometry

Opacity
Controls cutout opacity. Black = transparent, White = opaque.

Bump Map
Connects a bump or normal map for surface detail.

Optimizations

Reflection

Trace Depth Override / Max Trace Depth
Per-material override for reflection trace depth.

Advanced

Ray Type Intensity Multipliers
Per-component (Base, Reflection, Rim, Emission) intensity multipliers per ray type.
