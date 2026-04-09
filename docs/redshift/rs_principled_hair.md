---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Principled+Hair.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Principled Hair
captured: 2026-04-09
tags: [redshift, material, shader, hair, fur, principled, raw]
---

Shaders > Material Shaders > Principled Hair

Principled Hair

Overview

The Redshift Principled Hair shader is a physically-based shader for hair and fur. You can quickly get up to speed with natural hair results by adjusting the melanin and melanin redness values, adding in some randomization by increasing the amount of variation for various color and roughness parameters.

Trace Depths

The look of hair is heavily affected by the reflection trace depth render setting. When hair is lighter in color a multi-scattering reflection effect becomes more pronounced, this means that light hair (lower melanin values) will generally require higher trace depth values than dark hair (higher melanin values). Hair that is driven by an albedo color behaves in the same way.

Render Requirements

Hair rendering in Redshift requires the use of hair/spline geometry or C4D Hair objects. Standard polygon geometry is not supported by the Principled Hair shader.

Examples

Usage with C4D Hair
The Principled Hair shader is assigned directly to a C4D Hair object via the Hair Material tag.

Hair color from root to tip
The color variation from root to tip can be driven by connecting a gradient texture to the Albedo Color input, using the hair UV coordinates along the V axis.

Hair color from a texture
A texture can be connected to the Albedo Color to drive per-strand color variation.

Mixing colors
Colors can be mixed between the melanin-based model and an albedo color using the Albedo Weight parameter.

Parameters

General

Melanin
Controls the darkness/pigmentation of the hair using a physically-based melanin model. 0 = blonde/white hair, 1 = very dark/black hair.

Melanin Redness
Controls the redness of the melanin pigment. Higher values shift the hair color towards red/auburn tones.

Albedo Color
An explicit color input that overrides or blends with the melanin-based color model.

Albedo Weight
Controls the blend between the melanin color model and the Albedo Color. At 0 the melanin model is used exclusively, at 1 the Albedo Color is used exclusively.

Color

Root Color
A color applied at the root of the hair strand.

Tip Color
A color applied at the tip of the hair strand.

Root-Tip Weight
Controls the blend between root and tip color along the strand length.

Variation

Color Variation
Adds per-strand randomization to the hair color, simulating natural variation in real hair.

Roughness Variation
Adds per-strand randomization to the roughness, simulating natural variation.

Diffuse Contribution

Diffuse Weight
Controls the contribution of a diffuse/Lambertian component mixed into the hair shading. Useful for achieving softer, less specular-dominated looks.
