---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Standard_Material.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Standard Material
captured: 2026-04-09
tags: [redshift, material, shader, PBR, standard-material, raw]
---

Shaders > Material Shaders > Standard Material

Standard Material

Table Of Contents

Overview
Examples
Thin Walled Translucency
Base Properties
Base
Reflection
Transmission
Subsurface
Sheen
Thin Film
Coat
Emission
Geometry
Optimizations
Reflection
Refraction
Advanced
Diffuse
Reflection
Transmission
Sheen
Coat
Anisotropy


Overview

This Standard Material is the recommended all purpose material that is physically plausible, energy conserving and aligned with 'PBR' based principles. It is the successor to the Redshift Material but offers a cleaner interface that is more comparable to the standard material shaders of other render engines.

A Standard Material in the Node Editor

Examples
Thin Walled Translucency

The Standard material supports thin walled translucency in the form of diffuse transmission by interpreting an object's surface as an infinitely thin shell. This simulates light passing through thin objects and is a perfect effect for things like paper or leaves where a full subsurface scattering solution is overkill or not needed.

To enable thin walled translucency, simply enable Thin Walled under the Geometry sub-section, then adjust the Transmission Color and Transmission Weight in the Base section to control how much light passes through the object and what color it is tinted.

Base Properties

Base

Base Color
Controls the overall base color of the material. This is the color that the object will appear to be under neutral white lighting. The base color represents the surface albedo of non-metallic/dielectric materials, it represents the surface color of metallic materials.

Base Weight
Multiplier for the Base Color parameter. When a texture is connected to Base Color, the Base Weight acts as an overall opacity/influence multiplier for the base color. A value of 0 means the base color has no effect on the material.

Metalness
Controls how metallic the material appears. A value of 0 means the material is fully dielectric (non-metallic), and a value of 1 means the material is fully metallic. In the metallic regime, the reflectance is controlled entirely by the base color (F0 and F90 are derived from the base color) and a strong Fresnel effect exists.

Diffuse Roughness
Controls the roughness of the diffuse shading component. Higher values will give the diffuse layer a more retroreflective appearance.

Reflection

Reflection Weight
Controls the intensity of the reflection layer. At a value of 1.0, the reflection layer is fully active and the Fresnel equations determine how much light is reflected vs transmitted.

Reflection Color
Controls the color of the reflection. For dielectric materials, the reflection color should generally be kept at white. For metallic materials, a colored reflection can be useful to represent the actual reflective color of a metal.

Reflection Roughness
Controls the roughness of the reflection. Lower values produce sharper, mirror-like reflections while higher values produce more diffuse, blurry reflections.

Anisotropy
Controls the directional bias of the reflection roughness. A value of 0 means the reflection is isotropic, while values approaching 1 or -1 produce a very elongated, anisotropic reflection.

Anisotropy Rotation
Rotates the direction of the anisotropic reflection. A value of 0.5 rotates the anisotropy by 180 degrees.

Fresnel Type
Selects the Fresnel model used to calculate the reflection falloff.
Schlick - A fast approximation of the full Fresnel equations. Suitable for most materials.
Scientific - Uses the full Fresnel equations based on the Index of Refraction.

IOR (Index of Refraction)
When the Fresnel Type is set to Scientific, this parameter controls the index of refraction of the surface, which determines the strength of the Fresnel effect. Common values: water ~1.33, glass ~1.5, diamond ~2.4.

Reflection Weight affects how much of the incoming light is reflected. At low roughness values a sharp mirror-like reflection is visible, at high values the reflection becomes blurred.

Transmission

Transmission Weight
Controls the intensity of the transmission/refraction component. A value of 1 means the object is fully transmissive (like glass).

Transmission Color
Controls the color of transmitted light. This can be used to tint glass or other transparent materials.

Transmission Depth
Determines the depth at which the Transmission Color is fully absorbed. A short depth means the color is absorbed quickly (dense material), while a long depth means light travels further before being absorbed.

Depth Color (Absorption)
The color of light after it has traveled through Transmission Depth units of the material.

Scatter Color
The color of the volumetric scattering inside the material.

Scatter Anisotropy
Controls the directionality of volumetric scattering. Positive values scatter light forward, negative values scatter light backward.

IOR
Index of Refraction for the transmission/refraction calculation. Controls the amount of bending of light rays passing through the material.

Abbe Number
Controls the amount of chromatic dispersion (splitting of white light into spectral colors) in the transmitted light. A value of 0 disables chromatic dispersion.

Thin Walled
When enabled, the material treats the surface as an infinitely thin shell. Transmission behaves as diffuse translucency rather than full refraction. Good for leaves, paper, thin fabric.

Subsurface

Subsurface Weight
Controls the influence of subsurface scattering on the material. At 1.0 the SSS component is fully active.

Subsurface Color
Light scattered inside the object takes on this overall color and transports it back to the surface, giving the material its characteristic subsurface color.

Subsurface Radius
Controls the distance that light travels inside the material before being scattered or absorbed. The RGB channels can be set independently allowing for different scatter radii per color channel, producing a more realistic skin-like look where red light penetrates deeper than green or blue.

Subsurface Scale
A global scale factor applied to the Subsurface Radius. Allows you to scale the SSS effect without changing the relative RGB radii.

For example, in human skin a skin tone would be appropriate for subsurface color, a generally reddish color for subsurface radius to emulate the blood vessels underneath the skin, and a relatively low scale so that the skin does not appear too thin.

The Subsurface parameters are also used to control a back-lighting/translucency effect when Thin Walled is enabled in the Geometry subsection.

If you encounter GI flickering due to SSS when using Irradiance Point Cloud, try increasing the Retrace Threshold to 3 or higher.

Mode
The subsurface calculation offers the following methods:

Point-Based Diffusion - The fastest and cleanest but least accurate method, not good for detailed geometry and may be unstable during animation.
Ray-Traced Diffusion - Visually similar to Point-Based Diffusion but more accurate and stable at the cost of increased render times.
Random Walk (default) - The most accurate method, the best choice for detailed and thin geometry but can be slower than Ray-Traced Diffusion.

Point-Based Diffusion:
Faster and smoother
Less detailed / accurate
Does not work in progressive rendering mode
Requires a "prepass" stage

Random Walk:
Realistic results for detailed and thin geometries
Calculates scattering in a volume without using preliminary estimates or simplifications of the geometry
Can be slower than other methods
Works in progressive rendering mode
Overlapping geometry can cause artifacts
Not available in Redshift Material (Legacy)

Samples
Only relevant for Ray-Traced Diffusion and Random Walk subsurface scattering modes. Controls the amount of noise or grain in the Subsurface calculation. Higher numbers will reduce potential grain issues but will take longer to render.

Include Mode
Only relevant for Ray-Traced Diffusion and Random Walk subsurface scattering modes. Controls which objects are seen by the Scattering calculation.
All Objects: All other objects participate in the SSS effect.
Only Self: Contain the SSS effect in the same object only.

Sheen

The Sheen effect can be used to simulate a soft backscattering effect seen in cloth and fabric-like materials. It adds a soft, velvety layer on top of the base material.

Sheen Weight
Controls the influence of the Sheen layer. At 1.0 the Sheen layer is fully active.

Sheen Color
Controls the color of the Sheen reflection.

Sheen Roughness
Controls the roughness/spread of the Sheen effect. Lower values produce a tighter sheen while higher values produce a more diffuse sheen.

Thin Film

Thin Film Weight
Blends between no thin film effect (0) and full thin film effect (1).

Thin Film Thickness
The thickness of the thin film in nanometers. This directly affects the interference pattern and the colors produced by the thin film.

Thin Film IOR
The index of refraction of the thin film layer. This affects the interference colors produced.

Coat

Coat Weight
Controls the intensity of the clear coat layer. At 1.0 the coat layer is fully active.

Coat Color
Controls the color of the clear coat reflection.

Coat Roughness
Controls the roughness/glossiness of the clear coat layer.

Coat IOR
The index of refraction of the clear coat layer.

Coat Affect Color
Controls how much the coat layer tints the underlying base material color.

Coat Affect Roughness
Controls how much the coat layer affects the roughness of the underlying base material.

Coat Normal
Allows connecting a separate normal map for the coat layer, independently from the base layer normal.

Emission

Emission Color
Controls the color and brightness of the emitted light.

Emission Weight
Controls the intensity/weight of the emission. Multiplied against the Emission Color.

Geometry

Thin Walled
When enabled treats the surface as an infinitely thin shell. Useful for single-sided geometry representing thin objects. Affects transmission and subsurface calculations.

Opacity
Controls the overall opacity of the material. Black is fully transparent, white is fully opaque. Supports texture connections for cutout opacity.

Bump Map
Connects a bump or normal map to perturb the surface normal for added surface detail.

Normal Type
Selects the coordinate space of the connected normal map.
Tangent Space (default) - Standard for most textures from Substance, Mari, etc.
Object Space - Used for baked object-space normals.
World Space - Rarely used, for world-space baked normals.

Displacement
Connects a displacement map to physically offset the surface geometry. Note: Displacement is handled at the object level in Redshift, not directly in this slot for most workflows.

Optimizations

Reflection

Trace Depth Override
Enables a custom reflection trace depth for this specific material, overriding the global render setting.

Max Trace Depth
The maximum number of reflection bounces for this material.

Refraction

Trace Depth Override
Enables a custom refraction trace depth for this specific material, overriding the global render setting.

Max Trace Depth
The maximum number of refraction bounces for this material.

Advanced

Diffuse

Ray Type Intensity Multipliers
Allows control of the diffuse contribution per ray type (Primary, Reflection, Refraction, GI, Shadow).

Reflection

Ray Type Intensity Multipliers
Allows control of the reflection contribution per ray type.

Transmission

Ray Type Intensity Multipliers
Allows control of the transmission contribution per ray type.

Sheen

Ray Type Intensity Multipliers
Allows control of the sheen contribution per ray type.

Coat

Ray Type Intensity Multipliers
Allows control of the coat reflection contribution per ray type.

Anisotropy

Orientation
Controls the reference space used for anisotropy direction.
UV - Uses the UV tangent direction.
World Space - Uses a world-space reference vector.
Reference Vector - Uses a custom reference vector.

Reference Vector
A custom world-space reference vector used when Orientation is set to Reference Vector.

Rotation
Controls the rotation of the anisotropy direction.
