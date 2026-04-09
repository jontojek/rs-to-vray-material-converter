---
source: https://documentation.chaos.com/space/VMAYA/111740574/VRayBlendMtl
site: Chaos V-Ray for Maya Documentation
section: Materials > Utility Materials > VRayBlendMtl
captured: 2026-04-09
tags: [vray, maya, material, shader, blend, layering, utility, raw]
---

# VRayBlendMtl

VRayBlendMtl layers several V-Ray compatible materials together in an efficient manner. Used for complex materials like car paints, human skin (with VRayFastSSS2 as base), etc. Supports the VRayMtlSelect render element to split sub-materials into separate render elements.

VRayBlendMtl takes a base material and applies coat materials on top of it in a stack. Each coat material blends between its own shading and the materials below it in the stack.

---

## Base Parameters

**Base Material** – The bottom-most material over which all coat materials are layered. If unspecified, the base is assumed to be a perfectly transparent material.

**Additive Mode** – When enabled, VRayBlendMtl behaves like a multi-layered Shellac material. This is often physically incorrect (material may reflect more light than it receives). Use with caution.

---

## Coat Materials

**Add New Item** – Adds a new coat material slot.

**Coat Material** – The material to use as a coating layer.

**Blend Amount** – Controls how much of the final result is contributed by the coat material vs. materials below it.
- White = coat material fully wins, blocks everything below.
- Black = coat material has no effect, materials below show through.
- Can be controlled by a texture map (e.g. dirt mask, AO map, curvature map).

**Opacity** – Defines the strength of the layer.

The arrows on the right reorder coat material slots. The bin icon deletes a coat material slot.

---

## Hardware Shading

**Viewport Color** – Color used to represent the material in the Maya viewport.

**Override Viewport Color** – When enabled, allows specifying a custom viewport color. Helps visualize complex shaders in the viewport.

---

## Notes

- If any Coat material is a VRayMtl with a Fog color different from white, the Fog color will be ignored. Fog color is only considered for the Base material.
- Common usage patterns:
  - Car paint: VRayStochasticFlakesMtl or VRayFlakes2Mtl as a coat over a VRayMtl base.
  - Skin: VRayFastSSS2 as base with a reflective VRayMtl as a coat.
  - Dirt/wear: Clean material as base with a dirt/dust material as coat, masked by AO or curvature texture.
