---
source: https://documentation.chaos.com/space/VMAYA/111742834/VRayLightMtl
site: Chaos V-Ray for Maya Documentation
section: Materials > Common > VRayLightMtl
captured: 2026-04-09
tags: [vray, maya, material, shader, emissive, self-illumination, light, GI, raw]
---

# VRayLightMtl

VRayLightMtl is a special material for producing self-illuminated surfaces. It can contribute to both indirect (GI) and direct illumination. Allows light sources of any shape, and can be assigned at object or face level to self-illuminate only portions of a mesh.

---

## Parameters

**Color Mode** – Choose how the light color is specified.
- Color – Direct color picker.
- Temperature – Kelvin temperature value (blackbody model used to derive color).

**Color** – Color of the light material when Color Mode is set to Color.

**Temperature** – Color of the light material when Color Mode is set to Temperature.

**Color Multiplier** – Multiplier for the light color. Increasing Value affects GI solution and produces more light. Note: overbright colors may look identical to white but produce different GI results.

**Opacity** – Texture used as opacity for the material. Note: making the material less opaque does NOT affect the self-illumination intensity. This allows perfectly transparent materials that still emit light.

**Emit on Back Side** – When enabled, object emits light from its back side too. When disabled, back sides render as black.

**Compensate Camera Exposure** – Adjusts material intensity to compensate for VRayPhysicalCamera exposure. Disabled when Direct Illumination is enabled.

**Multiply Color By Opacity** – When enabled, light color is multiplied by the opacity texture. When disabled, color and opacity act independently (additive transparency).

---

## Direct Illumination Settings

Turns objects with VRayLightMtl into actual direct mesh light sources. Equivalent to creating a VRayLightMesh for the same object.

**Direct Illum** – When checked, objects with this material are treated as mesh lights and emit direct light.

**Light Cut-off Threshold** – Threshold for light intensity below which the light is not computed. Useful in scenes with many lights to limit the effective range. 0.0 = calculated for all surfaces. Not available with CUDA renderer.

---

## Notes

- If you know the photometric power of a self-illuminated object in lumens (e.g. 1700 lm for a 100W bulb), you can calculate the multiplier by dividing lumens by the surface area of the object in square meters, when the self-illumination color is pure white.
- Direct Illumination only works properly when VRayLightMtl is the only material on the object. It will not work if the material is part of a VRayBlendMtl.
- Enabling Direct Illumination effectively turns the object into a mesh light. Camera and refraction visibility are linked — disabling primary (camera) visibility also disables refraction visibility, but reflection visibility is unaffected. For finer visibility control, use a light object instead.
