---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Material+Substance.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Substance 3D Material
captured: 2026-04-09
tags: [redshift, material, shader, substance, SBSAR, Adobe, procedural, raw]
---

Shaders > Material Shaders > Substance 3D Material

Substance 3D Material

Overview

The Substance 3D Material node can be used to quickly load Adobe Substance Designer SBSAR files directly into a Redshift shading graph, allowing you to easily render out high quality Substance textures and tweak their parameters. It is a single node that can be thought of as a bundle of procedurally generated images that can be routed anywhere in a Redshift shader.

Examples

Creating an automatic Substance 3D Material

A Substance 3D Material can be loaded and automatically set up using two methods. With each method a Redshift Standard Material is created and connected to a Substance node loaded with a SBSAR file. The Substance node outputs are automatically connected to the Standard material along with any necessary bump map and displacement nodes.

Method 1: Drag an SBSAR file directly from the OS file browser into the Redshift Node Editor. A Standard Material and Substance node are created and connected automatically.

Method 2: Use the Redshift Material Tools or Asset Manager to load an SBSAR file.

Parameters

File
The path to the SBSAR file to load. Changing this reloads the node with the new Substance's outputs and parameters.

Resolution
Controls the output resolution of the generated textures. Higher resolutions produce more detail but consume more GPU memory.

Randomize Seed
Randomizes the procedural seed of the Substance, generating a different variation of the material.

Substance Parameters
All parameters exposed by the Substance Designer graph are presented here and can be adjusted, driven by textures or animated. These vary per SBSAR file.

Outputs
The node exposes all outputs defined in the SBSAR file (typically: Base Color, Roughness, Metallic, Normal, Height, Ambient Occlusion, Emissive, Opacity). Each output can be connected to the corresponding input on a Standard Material or any other shader node.
