---
source: https://documentation.chaos.com/space/VMAYA/111740387/VRayStochasticFlakesMtl
site: Chaos V-Ray for Maya Documentation
section: Materials > Common > VRayStochasticFlakesMtl
captured: 2026-04-09
tags: [vray, maya, material, shader, stochastic-flakes, car-paint, glitter, snow, raw]
---

# VRayStochasticFlakesMtl

VRayStochasticFlakesMtl simulates car paints, snow, and other glittery materials. Works by simulating at render time the aggregated effect of a large number of mirror-like flakes scattered over the surface. Similar to VRayFlakes2Mtl and VRayCarPaint2Mtl but uses less memory and avoids tiling issues. Term "stochastic" means the method uses a random variable.

---

## Base Parameters

**Enable Flakes** – Enables flake simulation. When disabled, renders only the specified BRDF type with the specified Hilight Glossiness (smooth non-flake appearance).

**Num Flakes** – Number of flakes expressed as the square root of the actual number in the unit texture square. Example: value of 3000 generates 9,000,000 flakes per unit square. Maximum useful value is 46340 (approx 2 billion flakes). To add more than 2 billion flakes, increase Flake Scale instead.

**Hilight Glossiness** – Controls distribution/orientation of flakes. Values close to 1.0 orient flake normals more perpendicular to the surface. Lower values randomize flake normals.

**Blur Angle** – Controls softening of the flakes effect. Higher = softer. Lower = sharper. Typical range: 0.5–8.

**Reflect Filter** – Reflection color of the flakes.

**Mapping Type** – How flakes are scattered on the surface.
- Explicit UVW – Flakes mapped according to the specified UV channel. Density depends on how UVs follow the surface.
- Triplanar from Object XYZ – Uses triplanar mapping in object space. Useful for objects without suitable UV mapping.

**Mapping Channel** – Which UV channel to use when Mapping Type is Explicit UVW.

**Flake Scale** – Controls the scale of the texture space. For Explicit UVW, value of 1.0 recommended. For Triplanar, lower values (0.05, 0.01, or less) needed, especially for large objects — otherwise square artifacts may appear. Note: Num Flakes and Flake Scale are inversely proportional. Doubling Num Flakes and halving Flake Scale gives the same flake density but a different pattern.

**BRDF Type** – BRDF used to guide the distribution of the flakes.
- GGX – Uses GGX distribution (longer tail compared to Beckmann).
- Beckmann – Uses Beckmann distribution.

**Seed** – Random seed for flake pattern. Changing produces a different pattern.

---

## Colored Flakes Parameters

**Colored Flakes** – Enables colored flakes.
- Off – No color variance applied to flakes.
- Random Hue – Randomizes hue for each flake.
- Random from Map – Uses a texture map for randomized colors. Only the bottom-most horizontal row of pixels (1 pixel tall along U-axis) is sampled. Rest of map is ignored.

**Saturation** – Saturation variation of colors across all flakes.

**Lightness** – Lightness variation of colors across all flakes.

**Random Color Map** – Available when Colored Flakes is set to Random from Map. Texture from which random colors are sampled per flake.
- U Ramp → multi-colored flakes.
- V Ramp → single-color flakes.

**White Average** – When enabled, renders colored flakes without the physical darkening effect. Not physically correct.

---

## Advanced Parameters

**Blend Min** – Number of flakes per pixel below which discrete flake computation begins. Above this value, material transitions toward a smooth BRDF.

**Blend Max** – Number of flakes per pixel above which only the smooth BRDF is computed. Below this value, material transitions toward discrete flakes.
