---
source: https://documentation.chaos.com/space/VMAYA/111740335/VRayFastSSS2
site: Chaos V-Ray for Maya Documentation
section: Materials > Common > VRayFastSSS2
captured: 2026-04-09
tags: [vray, maya, material, shader, SSS, subsurface-scattering, translucent, skin, wax, marble, raw]
---

# VRayFastSSS2

VRayFastSSS2 is a material primarily designed for rendering translucent materials like skin, wax, marble, etc. Based on the BSSRDF concept (Jensen et al.). It is an approximation of subsurface scattering that is fast enough for production use.

VRayFastSSS2 is a complete material with diffuse, reflection, and SSS components — it can be used directly without needing a VRayBlendMtl. The material has three layers: a reflection layer, a diffuse layer, and an SSS layer. The SSS layer comprises single and multiple scattering components.

---

## General Parameters

**Preset** – Several built-in preset materials based on measured data (Jensen et al.). Presets include skin, marble, potato, etc. Scatter radius values are in cm — adjust Scale for your scene units.

**Scale** – Multiplies the Scatter radius. Use to correct for scene scale. Default 1.0 = use Scatter radius as-is. Example: 1:10 scale model = set Scale to 0.10.

**Index of Refraction (IOR)** – IOR of the material. Most water-based materials (skin, etc.) are approximately 1.3.

---

## Diffuse and Sub-Surface Scattering Layer Parameters

**Overall Color** – Overall color tint applied to both diffuse and SSS components. Pure white = neutral (no tinting).

**Diffuse Color** – Color of the diffuse portion. Requires Diffuse Amount > 0 to have effect.

**Diffuse Amount** – Blends between diffuse and SSS layers. 0.0 = no diffuse (pure SSS). 1.0 = no SSS (pure diffuse). A texture in this slot can mask SSS layers to simulate dust or paint on a surface.
Note: Procedural textures used here must have Alpha is Luminance enabled.

**Color Mode** – Controls which method is used for the SSS effect.
- Sub-surface color and scatter radius – Uses a general Sub-surface color and an inside Scatter color visible in backlit/thin parts of the object. Best for relatively opaque materials (skin, marble). Works best with Single Scatter set to Simple or Raytraced (Solid).
- Scatter coefficient and fog color – Uses a Scatter coefficient for the outside scatter layer and a Fog color for inside values. Better for translucent/refractive materials (juice, ice). Works best with Single Scatter set to Raytraced (Solid) or Raytraced (Refractive).

**Sub-surface Color** – General color for the SSS layer. Filtered/multiplied by Overall Color. Both filter the Scatter Color.

**Scatter Color** – Internal scattering color. Brighter = more translucent. Darker = more diffuse-like.

**Scatter Coefficient** – Available in Scatter coefficient mode. Outside SSS layer color and outer translucency. Brighter = frosted/less transparent. Darker = clearer.

**Fog Color** – Available in Scatter coefficient mode. Inside/backlit color. Brighter = more translucent. Darker = more diffuse-like. Filtered by Scatter Coefficient and Overall Color.

**Scatter Radius** – Depth of scattering inside the material. Always specified in cm regardless of Maya's working unit. Multiplied by Scale for effective depth. Smaller = shallower, more diffuse-like. Larger = deeper, more translucent.

**Phase Function** – Value -1.0 to 1.0. Controls general direction of light scatter inside the material.
- 0.0 = isotropic (uniform scatter in all directions).
- Positive = forward scatter. Most water-based materials (skin, milk) exhibit strong forward scattering.
- Negative = backward scatter. Hard materials like marble exhibit backward scattering.

---

## Specular Layer Parameters

**Specular Color** – Color of the specular reflection.

**Specular Amount** – Strength of the specular component. Automatic Fresnel falloff is applied based on IOR.

**Specular Glossiness** – Glossiness of highlights and reflections. 1.0 = sharp. Lower = blurrier.

**Cut-off Threshold** – Threshold below which reflections are not traced. Do not set to 0.0. Not available with CUDA renderer.

**Trace Reflections** – Enables glossy reflection calculations. When disabled, only highlights are calculated.

**Trace Depth** – Number of reflection bounces for this material.

---

## Options

**Single Scatter** – Controls how the single scattering component is calculated.
- None – No single scattering.
- Simple – Approximates single scatter from surface lighting. Fast. Good for opaque materials like skin where light penetration is limited.
- Raytraced (Solid) – Accurately calculates single scatter by sampling the volume. No refraction rays traced through the back side. Good for marble, milk.
- Raytraced (Refractive) – Like Raytraced (Solid) but also traces refraction rays. Produces transparent shadows. Good for water, glass.

**Refraction Depth** – Depth of refraction rays when Single Scatter is set to Raytraced (Refractive).

**Multiple Scattering** – Enables true volumetric raytracing inside the geometry for the SSS effect.

**Scatter GI** – When enabled, GI is included as part of the surface illumination map for multiple scattering. More accurate for highly translucent materials but slower.

**Consider All Objects** – When enabled, VRayFastSSS2 considers all intersecting objects with the same material when calculating SSS.

---

## Bump and Normal Mapping

**Map Type** – How the Map parameter is interpreted (Bump Map or various Normal Map types).

**Map** – Texture for the bump or normal map. Unconnected = no bump/normal mapping.

**Bump Mult** – Multiplier for the bump map effect.

**Bump Shadows** – When enabled, V-Ray considers bump maps when rendering shadows from objects with this material.
