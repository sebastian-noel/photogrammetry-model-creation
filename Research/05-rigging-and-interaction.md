# Rigging & Interaction Guide for Photogrammetry Models

## Overview

This guide covers how to take a static photogrammetry 3D model and make it interactive — doors that open, knobs that turn, drawers that slide — for use in Unity VR applications.

**Tool chain:** Photogrammetry Software → **Blender** (mesh cleanup, separation, rigging) → **Unity** (physics joints, XR interaction)

---

## 1. Mesh Cleanup in Blender

Raw photogrammetry scans have millions of polygons, floating artifacts, holes, and non-manifold edges. They must be cleaned before rigging.

### Remove Floating Geometry
1. Enter **Edit Mode** (Tab)
2. Select all (A)
3. **Mesh > Clean Up > Delete Loose** — removes disconnected vertices, edges, and faces
4. Use **Select Linked** (Ctrl+L) to isolate and delete floating chunks

### Fill Holes
1. **Select > All by Trait > Non Manifold** — finds boundary edges (holes)
2. Select the boundary edges of a hole
3. **Face > Fill** (F) for simple holes
4. **Face > Grid Fill** for more controlled results on larger holes

### Smooth Scan Noise
- Apply **Smooth modifier** (low iterations, 1–3)
- Or use **Sculpt mode > Smooth brush** for targeted smoothing
- Be careful not to destroy surface detail

---

## 2. Decimation (Polygon Reduction)

VR requires dramatically fewer polygons than raw scans produce.

### Blender Decimate Modifier

| Mode | Best For | How It Works |
|------|----------|-------------|
| **Collapse** | General purpose (recommended) | Merges edge pairs. Set ratio (0.1 = 10% of original) |
| **Un-Subdivide** | Uniformly subdivided meshes | Reverses subdivision levels |
| **Planar** | Flat regions (architecture) | Dissolves coplanar faces |

### Target Polygon Counts for VR

| Object Role | Quest 2/3 | PCVR |
|-------------|-----------|------|
| Hero / close-up interactive | 20k–50k | 50k–100k |
| Secondary prop | 5k–20k | 10k–50k |
| Background / distant | Under 5k | Under 10k |

### Workflow
1. Duplicate the high-poly mesh (keep as reference for texture baking)
2. Add **Decimate modifier** (Collapse mode)
3. Adjust ratio until you hit target poly count
4. Check the result — if it looks bad, try a less aggressive ratio
5. Apply the modifier

---

## 3. Texture Baking (High-Poly to Low-Poly)

After decimation, the low-poly mesh needs new UVs and baked textures from the original.

### UV Unwrapping the Low-Poly Mesh
- **Smart UV Project** — fastest automatic option. Good for complex shapes.
- **Manual seam-based unwrapping** — more precise. Mark seams along natural edges, then unwrap.

### Baking Process (Blender Cycles)
1. Keep both high-poly (with original texture) and low-poly (with new UVs) in the scene
2. Create a new image texture on the low-poly mesh's material
3. Select the high-poly mesh, then **Shift+click** the low-poly mesh
4. In **Render Properties > Bake**:
   - Bake Type: **Diffuse** (Color only, uncheck Direct and Indirect)
   - Enable **Selected to Active**
   - Set **Ray Distance** appropriately (start with 0.01, increase if needed)
5. Click **Bake**

### Maps to Bake

| Map | Purpose | Bake Type |
|-----|---------|-----------|
| **Diffuse/Albedo** | Surface color | Diffuse (Color only) |
| **Normal** | Fine surface detail lost in decimation | Normal |
| **Ambient Occlusion** | Subtle shadow in crevices | Ambient Occlusion |
| **Roughness** | Surface roughness (if available) | Roughness |

### Tips
- Bake at **8K resolution**, then downscale to **4K** for maximum quality within VR budgets
- Ensure no UV overlaps on the low-poly mesh
- If baking artifacts appear, increase ray distance or adjust cage settings

---

## 4. Mesh Separation (Isolating Interactive Parts)

Photogrammetry captures everything as a single mesh. To make parts interactive, you must separate them.

### Methods in Blender (Edit Mode)

| Method | How | Best For |
|--------|-----|----------|
| **Separate by Selection** (P > Selection) | Manually select faces, then P > Selection | Most common — select the door, knob, etc. |
| **Separate by Loose Parts** (P > By Loose Parts) | Auto-separates disconnected geometry | When parts are already physically separate in the scan |
| **Boolean Modifier** | Cut geometry along precise planes | Clean cuts where a door meets a frame |

### Selection Tips
- **Box/Circle/Lasso Select** for large regions
- **Select Linked Flat** (Ctrl+Shift+Alt+F) — selects connected faces within an angle threshold (great for flat door surfaces)
- **Hide** already-selected geometry (H) to work on inner parts
- **Ctrl+L** (Select Linked) to grab connected geometry

### Fixing Separated Parts

**Single-Sided Geometry:**
After splitting, the back face of parts (e.g., inside of a door) may be missing. Add a **Solidify modifier** to give thickness.

**Texture Seams:**
Cut edges may show texture stretching. Re-UV the cut border area and re-bake, or touch up with **texture painting** in Blender.

---

## 5. Setting Pivot Points

Correct pivot placement is **critical** — it determines where parts rotate/slide in Unity.

### Rules

| Part | Pivot Location |
|------|---------------|
| **Door** | Hinge edge (where it attaches to the frame) |
| **Drawer** | Center of the front face or back center |
| **Knob/Dial** | Center of rotation |
| **Lid** | Hinge edge |
| **Lever** | Fulcrum point |

### How to Set in Blender
1. Place the **3D Cursor** at the desired pivot location (Shift+S > Cursor to Selected, or snap to an edge/vertex)
2. Select the object
3. **Right Click > Set Origin > Origin to 3D Cursor**

**Do this in Blender before export.** Unity inherits the pivot from the imported model, saving significant work.

---

## 6. Rigging Approach

### Simple Pivot (Recommended for Most Cases)

For rigid mechanical interactions (doors, drawers, knobs), you do NOT need armatures:

1. Set correct pivot point in Blender
2. Export as FBX
3. Handle rotation/translation in Unity via physics joints

**Best for:** Doors, drawers, buttons, levers, simple knobs

### Armature-Based Rigging (Only When Needed)

Use armatures only when parts need to **deform** (bend, flex):

1. Create an armature with bones at joint locations
2. **Weight paint** each mesh part:
   - Full weight (1.0 / red) on the moving part
   - Zero weight (0.0 / blue) on the static part
   - For mechanical parts, use **binary weights** (all-or-nothing)
3. Test in **Pose Mode** — move each bone through its expected range
4. Add **bone constraints** for limits:
   - **Limit Rotation:** Restrict axis and angle range
   - **Limit Location:** Restrict translation for sliders

**Best for:** Cables, flexible parts, organic elements, complex multi-joint mechanisms

### Weight Painting Tips
- Start with **Automatic Weights** (Ctrl+P > Armature Deform > With Automatic Weights) as a baseline
- For mechanical parts, manually paint with **full strength and hard brush** — you want binary weights
- Scanned meshes with irregular topology may produce unpredictable automatic weights — manual painting is often necessary

---

## 7. Exporting from Blender to Unity

### FBX Export Settings

| Setting | Value |
|---------|-------|
| Apply Scalings | FBX All |
| Forward | -Z Forward |
| Up | Y Up |
| Apply Transform | Enabled |
| Include: Armature | Yes (if rigged) |
| Include: Mesh | Yes |
| Include: Camera/Lamp | No |
| Apply Modifiers | Yes |

### Armature Export Tip
If using armatures, export an **empty object alongside the armature** to prevent Unity from merging the root armature into the prefab root (which breaks animation binding paths).

---

## 8. Unity Physics Joints Setup

### Door (HingeJoint)

```
Components needed:
├── Rigidbody (Use Gravity: depends on design)
├── HingeJoint
│   ├── Anchor: at hinge edge position
│   ├── Axis: along hinge direction (usually Y)
│   ├── Use Limits: true
│   ├── Min: 0°
│   └── Max: 90° (or 120°, etc.)
├── Box Collider (simplified)
└── XR Grab Interactable
    └── Movement Type: Velocity Tracking
```

Optional: Add **Spring** for self-closing doors. Add **Motor** for powered doors.

### Drawer (ConfigurableJoint)

```
Components needed:
├── Rigidbody
├── ConfigurableJoint
│   ├── X Motion: Locked
│   ├── Y Motion: Locked
│   ├── Z Motion: Limited (slide direction)
│   ├── Linear Limit: travel distance (e.g., 0.3m)
│   ├── All Angular Motion: Locked
├── Box Collider
└── XR Grab Interactable
    ├── Movement Type: Velocity Tracking
    └── Track Rotation: false
```

For a separate handle: Add **FixedJoint** between handle and drawer body.

### Knob / Dial (ConfigurableJoint)

```
Components needed:
├── Rigidbody
├── ConfigurableJoint
│   ├── All Linear Motion: Locked
│   ├── Angular X Motion: Free or Limited
│   ├── Angular Y Motion: Locked
│   ├── Angular Z Motion: Locked
│   ├── Angular X Limit: set range (e.g., -180° to 180°)
├── Capsule/Sphere Collider
└── XR Grab Interactable
    └── Movement Type: Velocity Tracking
```

---

## 9. Full Workflow Summary

```
1. CAPTURE PHOTOS
   └── 100-400+ images per object (see Photography Guide)

2. PROCESS IN PHOTOGRAMMETRY SOFTWARE
   └── Generate dense mesh + texture (RealityScan / Metashape)

3. IMPORT INTO BLENDER
   ├── Clean up artifacts (delete loose, fill holes)
   ├── Identify interactive parts (doors, drawers, knobs)
   ├── Separate mesh (P > Selection for each part)
   ├── Set pivot points (origin to 3D cursor at hinge/center)
   ├── Decimate (target VR poly budget)
   ├── Re-UV unwrap low-poly mesh
   ├── Bake textures from high-poly to low-poly
   ├── De-light textures (remove baked lighting)
   ├── Add Solidify modifier to single-sided parts
   └── (Optional) Add armature for deformable parts

4. EXPORT AS FBX
   └── FBX All scaling, -Z Forward, Y Up, Apply Transform

5. IMPORT INTO UNITY
   ├── Extract materials and textures
   ├── Assign URP Lit shader
   ├── Set up texture import settings (compression, mipmaps)
   └── Verify scale (1 unit = 1 meter)

6. ADD PHYSICS & INTERACTION
   ├── Add Rigidbody to interactive parts
   ├── Add appropriate Joint (Hinge, Configurable, Fixed)
   ├── Set joint limits and properties
   ├── Add simplified Colliders (box/capsule, NOT mesh)
   └── Add XR Grab Interactable

7. TEST IN VR
   ├── Verify grab, rotate, open/close behavior
   ├── Adjust joint limits and physics properties
   ├── Profile performance (frame rate, draw calls)
   └── Add LOD groups if needed
```

---

## 10. Common Pitfalls

| Problem | Cause | Fix |
|---------|-------|-----|
| Double shadows on model | Baked lighting in photogrammetry textures | De-light the albedo textures |
| Door rotates around wrong point | Pivot point set incorrectly in Blender | Fix origin in Blender before export |
| Model is tiny/huge in Unity | Scale mismatch between tools | Use "FBX All" scaling; verify against 1m reference cube |
| Model looks bad after decimation | Over-aggressive polygon reduction | Use less aggressive ratio; bake normal map from high-poly |
| Back of door is invisible | Single-sided geometry from scan | Add Solidify modifier in Blender |
| Visible seam where mesh was cut | Texture stretching at cut edges | Re-UV and re-bake the cut area, or texture paint |
| Objects jitter or explode | Physics joint misconfigured | Lock all axes first, unlock one at a time |
| VR frame rate drops | Too many polygons / draw calls | Add LODs, use simplified colliders, enable static batching |
| Mesh collider kills performance | Using high-poly mesh as collider | Use simplified box/capsule colliders instead |
| Animation paths break in Unity | Armature root merging on FBX import | Export an empty object alongside the armature |

---

## Sources

- [Blender Retopology Guide](https://www.foxrenderfarm.com/share/blender-retopology-guide-clean-mesh-for-better-rendering/)
- [Cleaning Up a 3D Scan — 3D-Ace](https://3d-ace.com/blog/cleaning-up-a-3d-scan/)
- [Blender Separate Mesh Manual](https://docs.blender.org/manual/en/latest/modeling/meshes/editing/mesh/separate.html)
- [Unity Hinge Joint VR Tutorial](https://medium.com/@Brian_David/unity-hinge-joint-vr-tutorial-realistic-lid-physics-ceaa75208387)
- [Unity VR Doors and Drawers](https://fistfullofshrimp.com/unity-vr-doors-and-drawers/)
- [Creating Interactable Drawers in Unity VR](https://medium.com/@austinjy13/unityvr-creating-interactable-drawers-0728f56b3357)
- [XR Interaction Toolkit 3.1 Docs](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@3.1/manual/index.html)
- [Unity Hinge Joint Manual](https://docs.unity3d.com/Manual/class-HingeJoint.html)
- [Unity VR Optimization — Polycount](https://fistfullofshrimp.com/unity-vr-optimization-polycount/)
- [Unity Photogrammetry Workflow](https://unity3d.com/files/solutions/photogrammetry/Unity-Photogrammetry-Workflow_2017-07_v2.pdf)
- [Unity Photogrammetry De-lighting](https://www.sketchfab.com/blogs/community/unity-photogrammetry-de-lighting-workflow/)
- [How to Weight Paint in Blender](https://artisticrender.com/how-to-weight-paint-in-blender/)
- [Blender Render Baking Manual](https://docs.blender.org/manual/en/latest/render/cycles/baking.html)
- [Polynook — Blender to Unity Export](https://polynook.com/learn/lesson/how-to-export-models-from-blender-to-unity)
- [Codeless VR Door/Drawer with XRI (YouTube)](https://www.youtube.com/watch?v=e3HjICzrPvI)
