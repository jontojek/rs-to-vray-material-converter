---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Material_Layer.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Material Layer
captured: 2026-04-09
tags: [redshift, material, shader, layering, material-layer, raw]
---

Shaders > Material Shaders > Material Layer

Material Layer

Introduction

The Material Layer node outputs a combination of two materials. This node is closely related to the Material Blender, but only offers a base layer and one additional material layer. The top layer material can use a Mask and a Blend Type.

Inputs

Base Material Color
This is the color of the base material. The material connected to the Layer 1 input is placed on top of this base material. If you are working with layered or blended materials, they must only be used at the Base Material input.

Layer Material Color
Here you can connect the Out Color of a material, that should be layered on top of the Base Material. By default this layer covers the base material completely, but you can also use the Mask input to cut out parts of the layered material.

Layer Material Mask
Brightness values can be connected here to control the opacity of the material layer. With black color, or the numerical value 0.0, the layer material is completely invisible. With white color, or the numerical value 1.0, the layer material is completely visible. Values between 0 and 1 blend between the two materials.

Blend Type
Controls the mathematical blending operation used to combine the layer material with the base material.
