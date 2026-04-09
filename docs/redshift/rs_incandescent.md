---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Incandescent.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Incandescent
captured: 2026-04-09
tags: [redshift, material, shader, incandescent, emission, GI, raw]
---

Shaders > Material Shaders > Incandescent

Incandescent

Overview

This material shader has been optimized for simple, 'emissive' meshes that act as Global Illumination lights. It is intended to have a similar look to an area light that has its shape defined by a mesh, the difference being that this will only contribute to Global Illumination, since it doesn't perform any actual direct lighting.

Incandescent shaders are also great for objects that need to appear flat at a constant color value and are completely unaffected by lights.

Incandescence will only give off light if Global Illumination is enabled in your scene and the Ray Type Intensity Multiplier for your Incandescent shader is set to a value greater than 0.

Parameters

Illumination

Color
Controls the color of the object and the emitted light.

Temperature
Describes the light temperature in Kelvin, as an alternative to specifying a color directly. Uses a blackbody radiation model to derive the emission color from the temperature value.

Mode
Color: Uses the Color parameter directly.
Temperature: Uses the Temperature parameter via blackbody model.

Intensity Multiplier
Controls the overall brightness of the emitted light.

Double Sided
When enabled, the incandescent shader emits light from both sides of the geometry.

Ray Type Intensity Multipliers
Controls the emission intensity per ray type. The GI multiplier must be greater than 0 for the shader to contribute to Global Illumination.
