---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Material+Blender.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Material Blender
captured: 2026-04-09
tags: [redshift, material, shader, blending, layering, material-blender, raw]
---

Shaders > Material Shaders > Material Blender

Material Blender

Introduction

Sometimes a material uber shader is not enough for effects that ultimately require the overlaying of several materials, like dirt or extra reflection layers for example. To achieve this efficiently with Redshift, you should use the Material Blender shader.

The Material Blender supports up to six 'coat' layers on top of a base material shader. Since it is important to preserve energy for 'realistic' materials (meaning, a material cannot reflect more light than it receives), by default layers are not simply added together, they are instead mixed based on the color of each successive layer.

The default mixing rule is such that a layer blend color of 1.0, 1.0, 1.0 (white) results in the layer material color winning, effectively replacing the previous layers, whereas a layer blend color of 0.0, 0.0, 0.0 (black) results in the previous layers winning and the current layer having no effect.

Base Material

The base material is the bottom-most layer. Any material shader can be connected here. This is the material that all subsequent layers are blended on top of.

Layer 1-6

Each layer slot accepts:

Layer Material
The material shader to blend on top of the layers below.

Layer Color / Mask
A color or texture mask that controls where and how much of the layer material is visible. White = layer material fully visible, Black = layer material invisible (previous layers show through).

Blend Type
Controls the mathematical blending operation used to combine the layer with layers below. Options typically include Normal (default), Additive, and others.

Material Blender Example

A common use case is a base material (e.g. clean metal) with a dirt layer on top driven by an ambient occlusion or curvature mask, and a water puddle layer driven by a procedural mask.
