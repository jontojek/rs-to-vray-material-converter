---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Sprite+Node.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Sprite Node
captured: 2026-04-09
tags: [redshift, material, shader, sprite, opacity, cutout, transparency, raw]
---

Shaders > Material Shaders > Sprite Node

Sprite Node

Overview

The Sprite node can render transparencies much faster than standard Opacity cutouts and does not rely on Transparency Trace Depth. However, the Sprite node does not support semi-transparency and the stencil textures cannot go out-of-core.

Sprite vs Opacity

When a ray hits a polygon using opacity, Redshift has to execute operations to read the texture at that location, setup the next transparency or refraction ray and so on. These operations are wasteful if the ray hits an area that is completely transparent but the process can't be skipped because that part may be semi-transparent and Redshift cannot assume otherwise. Because of this, the transparency trace depth has to be increased in order to prevent rays from being terminated prematurely which introduces visual artifacts.

The Sprite node avoids this problem by using a stencil mask to immediately discard geometry in fully transparent regions before shading begins. This makes it significantly faster for hard-edged cutout opacity (e.g. foliage cards, decals, alphaclipped geometry) where semi-transparency is not required.

Limitations:
- Does not support semi-transparency (values between 0 and 1 are treated as fully opaque or fully transparent based on a threshold)
- Stencil textures cannot go out-of-core (must fit in GPU memory)
- Not suitable for glass, smoke or any partially transparent material

Parameters

Stencil
The black-and-white mask texture that controls which pixels are visible (white) and which are discarded (black).

Threshold
The cutoff value between transparent and opaque. Pixels above this value are rendered, pixels below are discarded.

Input Material
The material whose output is used for the visible (non-discarded) pixels.

Warnings and Errors

If the stencil texture is too large to fit in GPU VRAM, Redshift will report an error as the Sprite node does not support out-of-core textures.
