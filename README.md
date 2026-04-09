# RS → VRay Material Converter

A practical reference and (eventually) automated conversion tool for translating **Cinema 4D Redshift** materials into **Maya V-Ray** equivalents. Industrial design / automotive focus.

Built by a working VFX artist — not a generic parameter dump. Every mapping includes conversion notes, formulas where needed, and explicit flags for parameters that have no clean equivalent.

---

## Current Status

**Phase 1 — Complete** · Parameter Reference App  
**Phase 2 — Planned** · Python converter: `shader_map.json` + Maya pipeline scripts

---

## Phase 1 · Parameter Reference

`index.html` — open in any browser, no server needed.

An interactive side-by-side mapping of every RS Standard Material parameter to its VRayMtl equivalent. Includes:

- 52 parameters across 9 shader sections
- Conversion tags: **Exact** · **Invert** · **Manual** · **N/A**
- Inline formulas for roughness ↔ glossiness conversions
- Explicit documentation of parameters with no VRay equivalent (flagged for Phase 2 handling)
- Search and filter by conversion type
- Section nav with live scroll tracking

### Shader Sections Covered

| Section | Params | Notes |
|---|---|---|
| Base / Diffuse | 4 | Full coverage |
| Reflection / Specular | 11 | Includes BRDF, anisotropy, Fresnel type |
| Thin Film | 3 | Full coverage |
| Transmission / Refraction | 9 | Includes scatter phase flag (N/A) |
| Subsurface Scattering | 6 | Includes SSS mode + anisotropy flag (N/A) |
| Clear Coat | 7 | Includes coat-affect-roughness flag (N/A) |
| Sheen | 3 | Full coverage |
| Emission | 4 | Includes double-sided emission flag (N/A) |
| Geometry / Surface | 7 | Includes displacement with midpoint formula |
| Advanced / Ray Visibility | 5 | Object-level overrides documented |

---

## Phase 2 · Python Converter (Planned)

### Planned repo structure

```
converter/
├── __init__.py
├── parser.py       # Reads RS material data from export format TBD
├── mapper.py       # Applies shader_map.json rules
└── builder.py      # Constructs VRayMtl network in Maya

data/
└── shader_map.json # Data-driven mapping table extracted from Phase 1
```

### Design principles
- `shader_map.json` is the source of truth — non-coders can edit mappings without touching Python
- Parameters flagged `na` in Phase 1 are surfaced as warnings, never silently dropped
- Scripts run both as a Maya shelf tool and headless via `mayapy` CLI
- No external dependencies — Maya `cmds` and stdlib only

---

## Known Gaps (No VRay Equivalent)

Parameters documented in Phase 1 that have no clean VRayMtl mapping. Phase 2 will flag these at conversion time.

| RS Parameter | Reason |
|---|---|
| Transmission Scatter Phase | VRayMtl uses isotropic scattering only — use VRayVolumeMtl |
| SSS Anisotropy | VRayMtl SSS is isotropic — use VRayFastSSS2 |
| Coat Affect Roughness | No equivalent coat→base roughness bleed in VRay |
| Emission Double-Sided | Use VRayLightMtl or duplicate geo with flipped normals |

---

## Scope

This tool focuses on **RS Standard Material → VRayMtl** for production industrial design and automotive work. Additional shader pairs (Car Paint, Incandescent, Material Blender, SSS, OpenPBR) are planned for later phases.
