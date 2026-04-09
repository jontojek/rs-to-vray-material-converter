---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Material+OpenPBR.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > OpenPBR Material
captured: 2026-04-09
tags: [redshift, material, shader, PBR, openPBR, ASWF, MaterialX, raw]
---

Shaders > Material Shaders > OpenPBR Material

OpenPBR Material

Table Of Contents

Overview
Parameters
Base
Specular
Transmission
Subsurface
Fuzz
Coat
Thin Film
Emission
Geometry
Redshift Optimizations
Reflection
Refraction
Redshift Advanced
Diffuse
Reflection
Transmission
Subsurface
Fuzz
Coat

Overview

The OpenPBR material is a physically based über-shader that presents as a standardized combination of the Autodesk Standard Surface and the Adobe Standard Material models. It is hosted by the Academy Software Foundation (ASWF) and organized as a subproject of MaterialX.

More information about the history and design can be found on this page detailing the OpenPBR Surface specification.

The OpenPBR material is made up of several layers.

Base: The base layer sits at the bottom and can be configured to simulate many material types. It can represent a dielectric or metallic material and is responsible for the primary reflection layer. This is controlled by the Metalness parameter. At metalness 0 the base is fully dielectric (non-metallic) and at metalness 1 the base is fully metallic.

Specular: The specular layer sits on top of the base layer and adds a specular/reflection lobe with independent IOR and roughness.

Transmission: The transmission layer controls refraction and transparent/translucent behaviour.

Subsurface: The subsurface layer controls subsurface scattering, simulating light penetrating below the surface and scattering back out.

Fuzz: A fuzzy/cloth-like scattering layer on top of the material stack.

Coat: A hard clear-coat layer on top of the stack.

Thin Film: An interference coating layer that simulates iridescent thin film effects.

Emission: Self-illumination of the material.

Geometry: Opacity, bump, normal and displacement inputs.

Parameters

Base

Weight
The overall weight/influence of the base layer. At 0 the base makes no contribution.

Color
The base color (albedo) of the material. For dielectrics this is the surface color. For metals, this is the F0 reflectance color.

Diffuse Roughness
Controls the surface roughness of the diffuse component. Higher values produce a more retroreflective Oren-Nayar-like appearance.

Metalness
Controls whether the base is dielectric (0) or metallic (1). Metallic surfaces derive their reflectance from the base color and exhibit a strong Fresnel effect.

Specular

Weight
The overall weight/influence of the specular (reflection) layer.

Color
The color of the specular reflection. For physically plausible dielectrics this should be white.

Roughness
The roughness of the specular lobe. At 0 the surface is a perfect mirror. At 1 the reflection is fully diffuse.

IOR
The index of refraction used to calculate the Fresnel reflectance of the specular layer. Typical values: 1.5 (plastic/glass), 1.33 (water), 2.4 (diamond).

Anisotropy
Controls the directional stretch of the specular reflection. At 0 the reflection is isotropic. Values approaching 1 or -1 produce elongated anisotropic highlights.

Rotation
Rotates the anisotropy direction.

Transmission

Weight
The overall weight/influence of the transmission/refraction layer. At 1 the surface is fully transmissive like glass.

Color
The color of the transmitted light. Used to tint transparent surfaces.

Depth
The distance (in scene units) over which the transmission color is fully absorbed. Controls the effective density of the material.

Scatter
The amount of volumetric scattering inside the transmissive volume.

Scatter Anisotropy
Controls the directionality of the volumetric scatter. Positive values scatter forward, negative values scatter backward.

Dispersion Abbe Number
Controls chromatic dispersion (splitting of light into spectral colors). 0 disables dispersion.

Extra Roughness
An additional roughness added on top of the specular roughness for the transmission lobe specifically.

Subsurface

Weight
The overall weight/influence of the subsurface scattering layer.

Color
The color of the subsurface scattering effect — the tint of scattered light emerging from below the surface.

Radius
Controls the mean free path (scatter distance) of light within the material per RGB channel. Allows independent control of red, green and blue scatter distances for realistic skin-like results.

Scale
A global scale multiplier applied to the Radius, allowing the SSS extent to be scaled uniformly without changing the relative RGB channel ratios.

Anisotropy
Controls the directionality of the subsurface scattering. Positive values scatter forward (glassy), negative values scatter backward (frosted).

Fuzz

Weight
Controls the coverage and density of the fuzz scattering layer that simulates cloth or dusty surfaces on top of all other layers. At 0 the fuzz effect is disabled.

Color
Controls the color of the fuzz layer.

Roughness
Controls the shape of the simulated fuzz microflakes. High roughness produces spherical microflakes (soft, isotropic look). Low values produce elongated fiber-like microflakes (silkier look).

Coat

Weight
Controls the intensity of the hard clear coat layer.

Color
Controls the color of the clear coat reflection.

Roughness
Controls the roughness of the clear coat. Low values produce a glossy lacquer-like look.

IOR
The index of refraction of the clear coat layer.

Anisotropy
Controls the anisotropy of the coat reflection.

Rotation
Controls the rotation of the coat anisotropy direction.

Affect Color
Controls how much the coat layer tints the underlying material layers.

Affect Roughness
Controls how much the coat layer affects the roughness of the underlying material layers.

Normal
Allows connecting a separate normal map for the coat layer, independent from the base normal.

Thin Film

Weight
Blends between no thin film effect (0) and full thin film effect (1).

Thickness
The thickness of the thin film layer in nanometers. Controls which wavelengths of light are reinforced or cancelled by interference, producing the iridescent color shift.

IOR
The index of refraction of the thin film layer.

Emission

Luminance
The luminance/brightness of the emitted light in the chosen unit.

Color
The color of the emitted light.

Geometry

Thin Walled
Treats the surface as an infinitely thin shell. Disables volumetric effects and makes transmission behave as simple two-sided transparency.

Opacity
Controls the cutout opacity of the material. Black = fully transparent, White = fully opaque.

Normal
Connects a tangent-space or object-space normal map to perturb the surface normals.

Bump
Connects a bump/height map for surface detail.

Displacement
Connects a displacement map to offset the surface geometry.

Redshift Optimizations

Reflection

Trace Depth Override
Enables a per-material override of the global reflection trace depth.

Max Trace Depth
Maximum reflection bounces allowed for this material.

Refraction

Trace Depth Override
Enables a per-material override of the global refraction trace depth.

Max Trace Depth
Maximum refraction bounces allowed for this material.

Redshift Advanced

Diffuse / Reflection / Transmission / Subsurface / Fuzz / Coat

Ray Type Intensity Multipliers
Allows independent intensity multipliers per ray type (Primary, Reflection, Refraction, GI, Shadow) for each shading component. Useful for faking or artistic overrides.
