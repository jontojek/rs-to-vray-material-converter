---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Car+Paint.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Car Paint
captured: 2026-04-09
tags: [redshift, material, shader, car-paint, flakes, automotive, raw]
---

Shaders > Material Shaders > Car Paint

Car Paint

Introduction

The car paint material shader simulates the physical properties of most types of car paint. For computer graphics, car paint is generally modeled as three separate layers:

1. Base pigment layer, with a diffuse color that can change depending on the viewing angle.
2. Metallic, reflective flakes that are embedded within the pigment layer.
3. A 'binder', which is a shiny/waxed coating exhibiting very glossy reflection.

The car paint material shader also exhibits a strong Fresnel effect, which can be controlled by the parameters below and helps with the paint's character.

Base Layer Diffuse

Base Color
The primary diffuse color of the car paint pigment layer.

Base Color 2
A second diffuse color used for the flop/flip color shift effect. The blend between Base Color and Base Color 2 is driven by the viewing angle.

Color Flip Amount
Controls how much the paint color shifts between Base Color and Base Color 2 as the viewing angle changes. This simulates the color flip characteristic of metallic and pearl paints.

Base Layer Specular

General

Specular Color
The color of the specular reflection in the base pigment layer.

Specular Weight
Controls the intensity of the base specular reflection.

Specular Roughness
Controls the roughness/glossiness of the base specular reflection.

Fresnel Control

Fresnel Type
Selects between Schlick approximation and full Fresnel equations based on IOR.

IOR
Index of refraction used for the base layer Fresnel calculation.

Metallic Flakes

Enable Flakes
Enables the metallic flake layer embedded within the pigment.

Flake Color
The color/reflectance of the metallic flakes.

Flake Weight
Controls the intensity/visibility of the flakes.

Flake Size
Controls the size of individual metallic flakes in UV space.

Flake Density
Controls the density/coverage of flakes on the surface.

Flake Roughness
Controls the roughness of individual flake reflections.

Flake Orientation
Controls the average tilt/orientation of flakes relative to the surface normal.

Flake Spread
Controls the variation in flake orientation, producing a more chaotic/realistic flake distribution.

Reflection General

Fresnel Reflection Control

Reflection Color
The color of the clear coat / binder layer reflection.

Reflection Weight
Controls the intensity of the clear coat reflection.

Reflection Roughness
Controls the roughness of the clear coat reflection. Very low values produce a mirror-like lacquer finish.

Definition

Controls the clarity/sharpness of the clear coat reflection.

Clear Coat Reflection

General

Coat Color
The color of the clear coat specular reflection.

Coat Weight
Controls the intensity of the clear coat layer.

Coat Roughness
Controls the roughness of the clear coat.

Fresnel Control

Coat IOR
Index of refraction for the clear coat Fresnel calculation.

Advanced

Enable Trace Depth Overrides
Enables per-material overrides for reflection trace depth.

Max Reflection Trace Depth
Maximum reflection bounces for this material.

Cut-off Override
Overrides the global reflection cut-off threshold for this material.

Bump

Bump Map
Connects a bump or normal map for surface detail on the base paint layer.
