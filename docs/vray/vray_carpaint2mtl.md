---
source: https://documentation.chaos.com/space/VMAYA/111739547/VRayCarPaint2Mtl
site: Chaos V-Ray for Maya Documentation
section: Materials > Common > VRayCarPaint2Mtl
captured: 2026-04-09
tags: [vray, maya, material, shader, car-paint, flakes, automotive, raw]
---

# VRayCarPaint2Mtl

The VRayCarPaint2Mtl simulates metallic car paint. It is a complex material with three layers: a base diffuse layer, a flake layer, and a clear coat layer. Each layer is adjustable independently. Uses GGX BRDF type and offers a base glossiness tail falloff option.

Note: Some options are unavailable in the Attribute Editor when render engine is set to V-Ray GPU.

---

## Base Layer

**Base Color** – Diffuse color for the base layer.

**Base Reflection** – Reflectivity of the base layer. The reflection color is the same as Base Color.

**Base Glossiness** – Reflection glossiness for the base layer.

**Base Glossiness Tail** – Controls the transition from highlighted to non-highlighted areas. Higher values (default) = sharper highlight transition. Lower values = more diffuse tail.

**Reflections For Base Layer** – When disabled, base layer only produces specular highlights, no actual glossy reflections.

**Bump Type** – Bump map or normal map type for the base layer.
- Bump Map
- Normal map in tangent space
- Normal map in object space
- Normal map in screen space
- Normal map in world space
- From texture bump output
- Explicit normal

**Bump Map** – Bump/normal map for the base layer.

**Bump Amount** – Multiplier for the bump/normal effect.

---

## Flake Layer

**Flake Color** – Color or map of the metal flakes.

**Flake Random Color** – Sets colors from a map (e.g. File or Ramp) to flakes in a random pattern. Only the bottom row on the U-axis of the map is sampled. When used, Flake Color acts as a filter — set to white (255,255,255) to disable its effect.

**Flake Orientation** – Orientation of the metal flakes relative to the surface normal. 0.0 = all flakes perfectly aligned with surface. 1.0 = flakes rotated completely randomly. Values above 0.5 not recommended — can produce artifacts.

**Flake Orientation Tail** – Controls the transition from highlighted to non-highlighted areas in the flake reflection.

**Flake Glossiness** – Reflection glossiness of the flakes.

**Flake Density** – Number of flakes per area. Lower = fewer flakes, higher = more flakes. Set to 0.0 for no flakes.

**Flake Scale** – Scales the entire flake structure.

**Flake Scale Triplanar** – Active only when Mapping Type is set to Triplanar. Scales the entire flake structure.

**Flake Size** – Size of flakes relative to the distance between them. Higher = bigger flakes, lower = smaller flakes.

**Flake Map Size** – Internal bitmap resolution for storing generated flakes. Lower = less RAM but visible tiling. Higher = more RAM but less tiling.

**Flake Seed** – Random seed for flake pattern. Changing produces a different pattern.

**Flake UV Coords** – Connect a texture placement node. Inactive with V-Ray GPU.

**Mapping Type** – How flakes are mapped to the surface.
- Mapping Channel – Uses the specified UV channel.
- Triplanar – Automatically computes coordinates in object space from surface normals.

**Mapping Channel** – Which UV channel to use when Mapping Type is set to Mapping Channel. Inactive with V-Ray GPU.

**Reflections For Flake Layer** – Toggles actual reflections for the flake layer. Inactive with V-Ray GPU.

---

## Coat Layer

**Coat Color** – Color or map of the coat layer.

**Coat Amount** – Thickness/blend amount of the coat layer. 0 = no coat. Higher values blend coat gradually.

**Coat IOR** – Index of refraction for the coat layer.

**Coat Glossiness** – Glossiness of the coat reflections.

**Reflections for Coat Layer** – When disabled, coat produces only specular highlights, no actual reflections.

**Coat Bump Type** – Bump or normal map type for coat layer. Inactive with V-Ray GPU.

**Coat Bump Map** – Bump/normal map slot for coat layer. Inactive with V-Ray GPU.

**Coat Bump Amount** – Multiplier for coat bump/normal map. Inactive with V-Ray GPU.

---

## Options

Note: These options are inactive with V-Ray GPU engine.

**Trace Reflections** – Global switch to toggle reflections for all layers.

**Trace Depth** – Number of times a ray can be reflected.

**Double Sided** – When enabled, makes the material double-sided.

**Cutoff Threshold** – Cutoff threshold for reflections across all layers.
