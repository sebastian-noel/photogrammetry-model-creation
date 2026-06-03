# Unity Import Pipeline for Photogrammetry Models

## Overview

This document covers the complete pipeline for importing photogrammetry 3D models into Unity for VR applications — from choosing the right format to optimizing for performance.

---

## 1. Import Format Comparison

| Format | Materials/Textures | Rigging/Animation | Unity Support | Best For |
|--------|-------------------|-------------------|---------------|----------|
| **FBX** | Excellent | Full support | Native (best) | Everything — recommended default |
| **OBJ** | Basic (.mtl) | None | Native | Static models only |
| **glTF/GLB** | PBR native | Partial | Requires plugin | Web/AR — not ideal for Unity VR |

### Recommendation
**Use FBX for all Unity imports.** It's Unity's internal import chain, preserves materials, textures, rigs, and animations. Supports multiple UV channels and skeletal animation.

---

## 2. Unity Import Settings

### Model Tab

| Setting | Value | Notes |
|---------|-------|-------|
| Scale Factor | 1.0 | Assumes 1 unit = 1 meter (verify against your photogrammetry export) |
| Mesh Compression | Low or Medium | Reduces file size without visible artifacts |
| Read/Write Enabled | Off | Save memory (enable only if you need runtime mesh manipulation) |
| Normals | Import | Use "Calculate" if normals look wrong (smoothing angle 60–80°) |
| Generate Lightmap UVs | On | Needed for baked lighting (common in VR). Pack margin: 2–4 texels |

### Materials Tab

| Setting | Value | Notes |
|---------|-------|-------|
| Material Creation Mode | Import via MaterialDescription | For Unity 2022+ |
| Extract Materials | Yes | Extract to dedicated Materials folder for editing |
| Extract Textures | Yes | Extract to Textures subfolder |

After extraction, remap materials to **URP Lit** shader.

### Texture Import Settings

| Setting | PCVR | Quest/Mobile VR |
|---------|------|-----------------|
| Max Size | 4096 | 1024–2048 |
| Compression | BC7/DXT5 | ASTC 4x4 or 6x6 |
| Mipmaps | Enabled | Enabled |
| Crunch Compression | Optional | Recommended |
| sRGB | On for albedo/diffuse | Off for normal, roughness, metallic, AO |
| Filter Mode | Bilinear or Trilinear | Bilinear |
| Aniso Level | 2–4 for ground textures | 1–2 |

### Animation/Rig Tab
- Set **Animation Type** to "None" for static photogrammetry models
- Use **"Generic"** for rigged non-humanoid objects (doors, drawers, etc.)

---

## 3. Mesh Optimization for VR

### Polygon Budgets

| Platform | Total Scene Budget | Individual Object | Background Object |
|----------|-------------------|-------------------|-------------------|
| **Quest 2/3** (standalone) | ~100k triangles | 5k–50k | Under 5k |
| **PCVR** (Rift, Vive, Index) | 1–4M triangles | 10k–200k | Under 10k |

Raw photogrammetry meshes often have **millions** of polygons. They MUST be decimated before use.

### LOD (Level of Detail) Setup

Use Unity's **LOD Group** component:

| LOD Level | Distance | Polygon Count |
|-----------|----------|---------------|
| LOD0 (closest) | 0–5m | Full detail |
| LOD1 | 5–15m | 50% of LOD0 |
| LOD2 | 15–30m | 25% of LOD0 |
| Culled | 30m+ | Not rendered |

- Use **dithered cross-fade transitions** to avoid visible "popping" in VR
- Generate LOD meshes in Blender using the Decimate modifier

### Draw Call Optimization

| Technique | When to Use | Target |
|-----------|-------------|--------|
| SRP Batcher | Same shader variant (automatic in URP) | Always on |
| Static Batching | Non-moving environment objects (mark as "Static") | Always for environment |
| GPU Instancing | Many copies of same mesh-material | Repeated objects |
| Dynamic Batching | Meshes under 300 vertices | Rarely applies to photogrammetry |

**Targets:** Under 100 draw calls for Quest. Under 500 for PCVR.

### Occlusion Culling
- Bake via **Window > Rendering > Occlusion Culling**
- Especially important for indoor/architectural scenes
- Set cell sizes based on scene scale

---

## 4. Material & Texture Handling

### Render Pipeline

| Pipeline | Use When | VR Support |
|----------|----------|------------|
| **URP** (Universal) | Quest, cross-platform, most projects | Excellent — recommended |
| **HDRP** (High Definition) | High-end PCVR only, guaranteed powerful GPU | Good but heavy |
| **Built-in** | Legacy projects only | Avoid for new projects |

### PBR Material Setup (URP Lit Shader)

Photogrammetry typically produces these texture maps:

| Texture | URP Lit Slot | Import Setting |
|---------|-------------|----------------|
| Albedo / Diffuse | Base Map | sRGB: On |
| Normal Map | Normal Map | sRGB: Off, Type: Normal Map |
| Ambient Occlusion | Occlusion Map | sRGB: Off |
| Metallic | Metallic Map | sRGB: Off (usually 0 for scanned objects) |
| Roughness | Smoothness (inverted) | sRGB: Off |

### De-lighting
Photogrammetry albedo textures contain **baked-in lighting** from the capture environment. This causes double-shadowing under Unity's real-time lights.

**Solution:** Use Unity's Photogrammetry De-lighting Workflow to strip lighting from albedo maps, producing cleaner textures that respond correctly to scene lighting.

### Texture Atlasing
- Combine multiple objects' textures into a single atlas (2048x2048 or 4096x4096)
- Reduces draw calls significantly
- Ensure **8–16 pixel padding** between UV islands to prevent mipmap bleeding

---

## 5. Scale & Positioning

### Getting Real-World Scale Correct
- Unity: **1 unit = 1 meter**
- Set scale in your photogrammetry software using known reference distances BEFORE export
- In Unity, create a **1x1x1 reference cube** (= 1 meter) to visually verify
- Player camera height in VR is typically **1.7m** — use as a sanity check

### Coordinate System Conversion (Blender → Unity)

| Setting | Value |
|---------|-------|
| Apply Scalings | FBX All |
| Forward | -Z Forward |
| Up | Y Up |
| Apply Transform | Enabled |

This ensures the model appears correctly oriented in Unity without manual rotation.

Other photogrammetry tools (Metashape, RealityScan) typically have **Unity-compatible export presets**.

---

## 6. XR Interaction Setup

### Required Packages
- `com.unity.xr.interaction.toolkit` (XRI 3.x)
- `com.unity.xr.management`
- `com.unity.xr.openxr` (for Quest/cross-platform)
- `com.unity.xr.hands` (for hand tracking)
- Import **Starter Assets** sample from XRI

### Making Objects Grabbable

Add these components to any photogrammetry model:

| Component | Purpose |
|-----------|---------|
| **Rigidbody** | Physics simulation (set mass to real-world weight) |
| **Collider** | Interaction detection (use simplified box/capsule, NOT mesh collider) |
| **XR Grab Interactable** | Makes object grabbable in VR |

Settings:
- **Movement Type:** Velocity Tracking (smoothest for constrained objects)
- **Collision Detection:** Continuous (for fast-moving grabbed objects)
- Enable **Add Default Grab Transformers** for automatic grab handling

### Physics Joints for Interactive Parts

| Interaction | Joint Type | Setup |
|-------------|-----------|-------|
| **Door** | HingeJoint | Anchor at hinge edge. Set angle limits (0–90°). Optional spring for self-closing. |
| **Drawer** | ConfigurableJoint | Lock all axes except slide direction. Set linear limits for travel distance. |
| **Knob/Dial** | ConfigurableJoint | Lock all linear motion + 2 rotation axes. Free 1 rotation axis with optional limits. |
| **Handle** | FixedJoint | Fuse handle to parent object so grabbing handle moves the whole part. |

### Hand Tracking vs Controllers
- **Controllers:** More reliable, lower latency. Default choice.
- **Hand tracking:** Enable in Project Settings > XR Plug-in Management > OpenXR. Requires OpenXR Plugin 1.11.0+, XR Hands 1.3.0+.
- XRI 3.x supports **both simultaneously**.

### Performance Targets

| Metric | Quest 2/3 | PCVR |
|--------|-----------|------|
| Frame Rate | 72–120 Hz | 90 Hz |
| Frame Budget | 8.3–13.8ms | 11.1ms |
| Draw Calls | Under 100 | Under 500 |
| Stereo Rendering | Single Pass Instanced | Single Pass Instanced |

**Enable Single Pass Instanced Rendering** (Project Settings > XR > OpenXR > Render Mode) — halves draw calls by rendering both eyes in one pass.

---

## 7. Recommended Project Structure

```
Assets/
  _Project/
    Scenes/
    Scripts/
    Prefabs/
      Environment/
      Props/
      Interactables/
    Materials/
      Environment/
      Props/
    Textures/
      Environment/
      Props/
    Models/
      Raw/              ← Original high-poly imports
      Optimized/        ← Decimated, game-ready meshes
    Animations/
    Settings/           ← URP asset, quality settings, XR settings
  Plugins/
  XRI/                  ← XR Interaction Toolkit samples
```

### Naming Conventions
- **PascalCase**, no spaces
- Models: `SM_DeskLarge_LOD0.fbx`
- Textures: `T_DeskLarge_Albedo.png`, `T_DeskLarge_Normal.png`
- Materials: `M_DeskLarge.mat`
- Prefabs: `PFB_DeskLarge.prefab`
- LODs: append `_LOD0`, `_LOD1`, `_LOD2`

### Prefab Workflow
- Create a **prefab** for each photogrammetry asset with all LODs, materials, colliders, and interaction components
- Use **nested prefabs** to compose complex scenes
- Make changes to **prefabs** (not scene instances) — changes propagate everywhere
- Create **prefab variants** for different interaction configurations

---

## Sources

- [Unity Manual: Model File Formats](https://docs.unity3d.com/6000.3/Documentation/Manual/3D-formats.html)
- [Unity Manual: Model Import Settings](https://docs.unity3d.com/Manual/FBXImporter-Model.html)
- [Unity VR Optimization — Polycount](https://fistfullofshrimp.com/unity-vr-optimization-polycount/)
- [Unity VR Optimization — Draw Calls](https://fistfullofshrimp.com/unity-vr-optimization-draw-calls/)
- [Meta Quest Development Tips](https://developers.meta.com/horizon/blog/vr-unity-sample-for-developing-high-quality-visuals-on-quest-how-to-get-started-tips-from-arabian-art-studios/)
- [XR Grab Interactable Docs (XRI 3.0)](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.0/manual/xr-grab-interactable.html)
- [Unity Render Pipelines Strategy 2026](https://unity.com/topics/render-pipelines-strategy-for-2026)
- [Unity Photogrammetry Workflow](https://unity3d.com/files/solutions/photogrammetry/Unity-Photogrammetry-Workflow_2017-07_v2.pdf)
- [Unity Photogrammetry De-lighting](https://www.sketchfab.com/blogs/community/unity-photogrammetry-de-lighting-workflow/)
- [Blender to Unity Export — Polynook](https://polynook.com/learn/lesson/how-to-export-models-from-blender-to-unity)
