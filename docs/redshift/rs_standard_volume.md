---
source: https://help.maxon.net/r3d/cinema/en-us/#html/Material+Standard+Volume.html
site: Maxon Redshift Documentation (Cinema 4D)
section: Shaders > Material Shaders > Standard Volume
captured: 2026-04-09
tags: [redshift, material, shader, volume, OpenVDB, smoke, fire, clouds, raw]
---

Volume Topics > Standard Volume Shader

Standard Volume

Overview

The Standard Volume shader is a physically based shader designed to render heterogeneous volumes like clouds, smoke, fire, and explosions. It combines an easy to use interface and controls while enabling greater flexibility and artistic control with the introduction of programmable volume shading. The Standard Volume shader accepts external shader inputs allowing for the creation and control of procedural volumes or the modification and displacement of existing volume grids.

The shading components of a volume shader are mainly driven by grids of voxel data contained inside a volume object, like an OpenVDB file. Volume objects typically contain multiple grids, for example a smoke simulation may contain density, velocity and temperature grids. Which grids are used for which shading component is controlled by the grid name parameters.

Speed and Simplicity

The Standard Volume shader is designed to be fast and simple to use. The shader has a small number of parameters that control the most important aspects of volume shading. The shader is designed to work well with the default settings for most use cases.

Displacement

The Standard Volume shader supports displacement of volume grids. The displacement is applied to the volume grid before shading. The displacement is controlled by the Displacement section of the shader.

Volumetric Multiple Scattering

The Standard Volume shader supports volumetric multiple scattering via the Multiscatter section. Multiscattering simulates light bouncing multiple times within the volume, producing a more physically accurate and visually richer result, especially in dense volumes like clouds.

Parameters

Volume

Density Grid
The name of the OpenVDB grid to use for the volume density. Density controls the opacity of the volume — higher density means more light is absorbed or scattered.

Density Multiplier
A multiplier applied to the density grid values. Increasing this value makes the volume denser and more opaque.

Density Remap
A remapping curve or value applied to the raw density grid values before rendering.

Scatter

Scatter Color
The color of light scattered within the volume. For smoke and clouds this is typically grey or white. For fire/explosions this can be warmer tones.

Scatter Color Grid
The name of the OpenVDB grid to use for per-voxel scatter color.

Scatter Anisotropy (Phase)
Controls the directional bias of light scattering within the volume. Positive values produce forward scattering (light passes through the volume and illuminates from behind), negative values produce backward scattering. 0 produces isotropic (equal in all directions) scattering.

Transparency

Transparency Color
The color of the volume when looking through it. Affects the transmitted light color.

Transparency Grid
The OpenVDB grid used for per-voxel transparency values.

Emission

Emission Grid
The name of the OpenVDB grid used for emission (e.g. a temperature grid for fire).

Emission Color
The color of the emitted light from the volume.

Emission Multiplier
A multiplier on the emission intensity.

Emission Mode
Blackbody: Uses the emission grid as a temperature value to compute a physically plausible blackbody emission color.
Raw: Uses the emission grid value directly as an intensity.

Blackbody Intensity
Controls the overall brightness of the blackbody emission.

Blackbody Color Ramp
A color ramp used to remap the temperature values to colors for the blackbody emission mode.

Advanced

Step Size
Controls the marching step size used when ray-marching through the volume. Smaller values produce more accurate results at the cost of longer render times. Larger values are faster but can miss fine volume detail.

Multiscatter

Enable Multiscatter
Enables volumetric multiple scattering for this volume. Produces more physically accurate and visually richer results especially in dense volumes like clouds.

Multiscatter Bounces
The maximum number of scattering bounces to calculate inside the volume.

Displacement

Displacement Grid
The OpenVDB grid used to displace the volume during rendering.

Displacement Scale
Controls the magnitude of the displacement.
