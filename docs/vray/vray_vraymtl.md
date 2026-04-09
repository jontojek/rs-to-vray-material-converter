---
source: https://documentation.chaos.com/space/VMAYA/111739405/VRayMtl
site: Chaos V-Ray for Maya Documentation
section: Materials > Common > VRayMtl
captured: 2026-04-09
tags: [vray, maya, material, shader, PBR, VRayMtl, raw]
---

# VRayMtl

The VRayMtl is a very versatile material that allows for better physically correct illumination (energy distribution) in the scene, faster rendering, and more convenient reflection and refraction parameters. This material can be easily set up to simulate a huge variety of surfaces from plastics to metals to glass and more by adjusting a handful of parameters.

Furthermore, with the VRayMtl you can apply different texture maps, control the reflections and refractions, add bump and displacement maps, force direct GI calculations, and choose the BRDF for how light interacts with the surface material.

---

## Basic Parameters

Source: https://documentation.chaos.com/space/VMAYA/111739013/VRayMtl+Basic+Parameters

**Shading Model** – Switch between the shading models: V-Ray and OpenPBR. When set to OpenPBR, some parameters are renamed. OpenPBR is not supported with V-Ray GPU.

**Diffuse Color** – The diffuse color of the material. The actual diffuse color also depends on the reflection and refraction colors.

**Amount** – A multiplier for the diffuse color.

**Opacity Map** – Assigns opacity to the material. White = fully opaque, black = fully transparent. Supports non-uniform opacity maps.

**Opacity Mode** – Controls how opacity is sampled. Not available with GPU renderer.
- Clip – Opacity texture is clipped to fully opaque or fully transparent at the mid-point. Very fast. Useful for leaves or many transparent surfaces layered together.
- Stochastic – Opacity texture is filtered and surface is randomly shaded as fully opaque or transparent for a correct average appearance. Optimal quality.

**Roughness Amount** – Simulates rough or dusty surfaces (e.g. skin, lunar surface). Not available with GPU renderer.

**Self-Illumination** – The self-illumination color of the material. A texture map can be used.

**Self-Illumination GI** – When enabled, self-illumination affects GI rays and the surface casts light on nearby objects. Using area lights or VRayLightMtl is generally more efficient.

**Compensate Exposure** – When enabled, adjusts self-illumination intensity to compensate for VRayPhysicalCamera exposure correction.

Note: When Shading Model is set to OpenPBR, Self-Illumination is renamed to Emission. Functionality is unchanged.

---

## Reflection

Source: https://documentation.chaos.com/space/VMAYA/111739261/VRayMtl+Reflection

**BRDF Type** – Determines the type of highlights and glossy reflections. Only has effect when reflection color is not black and reflection glossiness is not 1.0.
- Phong – Bright center with no falloff. Best for plastics.
- Blinn – Bright center with tight falloff. Multi-purpose.
- Ward – Broader center and falloff. Useful for cloth and chalk-like surfaces.
- GGX – Bright center with longer falloff. Most modern and flexible. Recommended for all materials. Supports anisotropy and the tail falloff control.

**Reflection Color** – The reflection color. Also dims the diffuse surface color (stronger reflections = darker diffuse).

**Amount** – Multiplier for the reflection color.

**Reflection Glossiness** – Controls sharpness of reflections. 1.0 = perfect mirror. Lower values = blurry/glossy reflections.

**Use Fresnel** – Makes reflection strength dependent on viewing angle. Physically correct for glass, liquids, dielectrics. Fresnel effect depends on IOR.

**Lock Fresnel IOR To Refraction IOR** – Unlocks the Fresnel IOR for independent control.

**Fresnel IOR** – IOR used for Fresnel reflection calculation. For metals (Metalness = 1.0), IOR has no effect — reflectance is derived from diffuse and reflection colors instead.

**GGX Tail Falloff** – Controls the transition from highlighted to non-highlighted areas when BRDF Type is GGX.

**Metalness** – Controls the reflection model from dielectric (0.0) to metallic (1.0). Intermediate values don't correspond to physical materials. Used for PBR workflows from other apps. For metals, reflectance is derived from diffuse and reflection colors.

**Use Roughness** – When enabled, Reflection Glossiness is interpreted inversely (roughness workflow). Glossiness 1.0 with Use Roughness = diffuse shading. Glossiness 0.0 with Use Roughness = sharp reflections.

Note: When Shading Model is OpenPBR, BRDF is always GGX, Use Roughness is always enabled, and tail falloff is hidden.

### Anisotropy

**Anisotropy** – Determines the shape of the highlight. 0.0 = isotropic. Negative/positive values simulate brushed surfaces. Range: -0.999 to 0.999.

**Anisotropy Rotation** – Orientation of the anisotropic effect. Float 0.0–1.0 (0.0 = 0°, 1.0 = 360°).

**UV Vectors Derivation** – Method for deriving anisotropy axes.
- Local object axis – Uses a local axis.
- Specified UVW generator – Assign a UVW generator node.

**Local Axis** – Specifies the local object axis (X/Y/Z) for anisotropy direction.

**Anisotropy UV Coords** – Connects a placement texture node to control the anisotropy direction. To use object local axis: connect place3dTexture.worldInverseMatrix to VRayMtl.anisotropyUVWGen.

Note: When Shading Model is OpenPBR, Local Axis defaults to Y.

### Thin Film

**Enable Thin Film** – Enables iridescent thin film interference effect. Use cases: soap bubbles, oil spills, iridescent paint.

**Min Thickness (nm)** – Minimum thickness of the thin film. If no Thickness Blend is applied, only this value is used.

**Max Thickness (nm)** – Maximum thickness when a Thickness Blend map is applied.

**Thickness Blend** – Map blending between Min and Max thickness. Without a map, only Min Thickness is used.

**IOR** – Refractive index of the thin film. Accepts a map.

### Reflection Advanced

**Trace Reflections** – Global toggle for reflections on this material.

**Max Depth** – Number of times a ray can be reflected. Scenes with many reflective/refractive surfaces may need higher values.

**Dim Distance** – Stops tracing reflection rays after a specified distance.

**Dim Fall Off** – Falloff radius for the dim distance.

**Reflect On Back Side** – When enabled, calculates reflections for back faces of objects too.

**Affect Channels** – Which channels are affected by reflectivity.
- Color Only – RGB channel only.
- Color+Alpha – Transmits alpha of reflected objects.
- All Channels – All render elements affected. Useful for Cryptomatte/Matte ID in reflections. Note: Back to Beauty composition won't match RGB when this is selected.

---

## Coat Layer

Source: https://documentation.chaos.com/space/VMAYA/111746714/VRayMtl+Coat

**Coat Color** – Color of the coat layer. Tints all layers (reflection, sheen, diffuse, refraction) but NOT the coat specular highlights (always white).

**Amount** – Blending weight of the coat layer. 0 = no coat. Higher values blend coat gradually.

**Darkening** – Controls how the coat layer impacts the appearance of underlying layers, emulating how a clear coat slightly darkens the base (e.g. applying lacquer over wood).

**Coat Glossiness** – Sharpness of coat reflection. 1.0 = glass-like. Lower = blurry/glossy.
Note: When Shading Model is OpenPBR, this is renamed to Coat Roughness and values are inverted (0.0 = glass-like, higher = blurry).

**IOR** – Index of refraction for the coat layer.

**Lock Coat Bump to Base Bump** – When enabled, base bump map takes priority over coat bump map.

**Bump Map Type** – Bump map or normal map (tangent/object/screen/world space).

**Bump Map** – The bump/normal map for the coat layer.

**Coat Bump Mult** – Multiplier for the coat bump effect.

**Coat Anisotropy** – Shape of the coat highlight. 0.0 = isotropic. Range: -0.999 to 0.999.

**Coat Anisotropy Rotation** – Orientation of coat anisotropic effect. Float 0.0–1.0.

---

## Refraction

Source: https://documentation.chaos.com/space/VMAYA/111738896/VRayMtl+Refraction

**Refraction Color** – Specifies the refraction color. Any value above zero enables refraction. Actual refraction color also depends on Reflection Color.

**Amount** – Amount of the refraction color.

**Refraction Glossiness** – Sharpness of refractions. 1.0 = perfect glass. Lower = frosted/blurry glass.

**Refraction IOR** – Index of refraction. Describes how light bends crossing the material surface. 1.0 = no bending. Common values: water 1.33, glass 1.5, diamond 2.4.

**Affect Shadows** – Causes material to cast transparent shadows for a simple caustic-like effect dependent on refraction and fog colors. For accurate caustics, disable this and enable Caustics in GI settings instead.

**Thin-Walled** – For single-surface transparent materials only. When enabled with Translucency SSS mode, simulates thin translucent surfaces (soap bubbles, leaves, curtains). SSS color = backside color, SSS amount = translucency amount.

Note: When Shading Model is OpenPBR, this rollout is renamed to Transmission. Refraction Glossiness becomes Transmission Roughness with inverted values.

### Translucency

**Translucency Mode** – Algorithm for subsurface scattering. Requires refraction to be enabled.
- None – No SSS. Only Fog color and Fog depth available. Light is attenuated but not scattered.
- Volumetric – Works with Refraction color to scatter light inside the object. Good for liquids and transparent materials. Requires GI with min 16 bounces (brute force or light cache). Requires Affect Shadows enabled. Requires closed geometry.
- SSS – Works with or without refraction. Good for skin, wax, marble, relatively opaque materials. Requires GI with min 16 bounces. Requires closed geometry.

**Fog Color** – Attenuation of light passing through the material. Thick objects appear less transparent than thin ones. Scene-scale dependent.

**Depth (cm)** – Strength of the fog effect. Higher values = more transparent. Lower values = more opaque.

### Volumetric Parameters

**Illumination Method** – Uniform (scatters light uniformly, good for skin) or Directional (scatters more toward light source direction, requires Affect Shadows).

**SSS Amount** – Blends between full scattering and pure refraction.

**Scatter Color** – Controls the scattering color.

### SSS Parameters

**SSS Amount** – Blends between diffuse color and SSS effect.

**SSS Color** – Overall surface appearance color.

**Scatter Radius** – Distance each RGB component travels inside the volume.

**Scale (cm)** – Controls the strength of the SSS effect.

### Refraction Advanced

**Trace Refractions** – Enables refractions for this material.

**Max Depth** – Number of times a ray can be refracted.

**Affect Channels** – Color Only / Color+Alpha / All Channels.

**Dispersion** – Enables true light wavelength dispersion.

**Dispersion Abbe** – Controls dispersion amount. Lower values = wider dispersion.

Note: When Shading Model is OpenPBR, this section is renamed to Transmission - Advanced.

---

## Sheen

Source: https://documentation.chaos.com/space/VMAYA/111739549/VRayMtl+Sheen

The Sheen layer is used for cloth materials such as satin.

**Sheen Color** – Color of the sheen effect.

**Amount** – How much the sheen layer overlays the diffuse color. Higher = more sheen color.

**Sheen Glossiness** – Sharpness of sheen reflections. 1.0 = all light reaches diffuse. Lower values = glossier cloth appearance.

Note: When Shading Model is OpenPBR, this rollout is renamed to Fuzz. Sheen Glossiness becomes Fuzz Roughness with inverted behavior (0.0 = none of the light reaches diffuse, higher = glossier).

---

## Bump and Normal Mapping

Source: https://documentation.chaos.com/space/VMAYA/111741178/VRayMtl+Bump+and+Normal+Mapping

**Map Type** – How the connected map is interpreted.
- Bump Map – Standard greyscale height map.
- Normal map in tangent space – Standard for textures from Substance, Mari, etc.
- Normal map in object space – Baked object-space normals.
- Normal map in screen space – Screen-space normals (rare).
- Normal map in world space – World-space baked normals.
- Explicit Normal – Uses world-space normal as bump normal without conversion.

Note: V-Ray GPU only supports Bump Map, Normal map in tangent space, and Normal map in world space.

**Map** – Texture connection for bump/normal map. Leaving unconnected disables bump/normal mapping.

**Bump Mult** – Multiplier for the bump map effect.

**Bump Delta Scale** – Decrease to sharpen bump, increase to blur. Only available when Map Type is Bump Map.

**Resolution-Independent Bump** – Ensures consistent bump effect regardless of camera distance or render resolution. Requires File texture Filter type set to Off.

---

## Options and Hardware Shading

Source: https://documentation.chaos.com/space/VMAYA/111739264/VRayMtl+Options+and+Hardware+Shading

**Cutoff Threshold** – Threshold below which reflections/refractions are not traced. V-Ray estimates contribution and skips computation below this value. Do not set to 0.0 (can cause very long render times). Not available with GPU renderer.

### Viewport Shader Quality

**Viewport Shader Quality** – Controls VRayMtl quality in the viewport. Overrides global viewport setting for this material.
- Use Global Settings
- Low – Direct diffuse and specular (Fresnel, metalness, specular BRDFs).
- Medium – Low + environment sampling (reflections/refractions), sheen, coat.
- High – Medium + normal/bump mapping, diffuse roughness, GTR gamma ≠ 2.0.
