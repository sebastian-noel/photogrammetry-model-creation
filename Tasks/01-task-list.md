# MVP Task List — Photogrammetry Model Creation

> **Goal:** Get 3 objects (small, medium, large) photographed → 3D modeled → rigged → interactive in Unity. Document the process. Ship fast.

### Team Roles
- **Stevin** — Photography + Blender (cleanup, rigging, separation, export)
- **Sebastian** — RealityScan Desktop (only one who can install it — processes photos into 3D models)
- **Gavin** — Unity (import, materials, XR interaction, physics joints, demo scene)

---

## Phase 1: Setup (Day 1)

### Everyone
- [ ] Send intro email to Lauren Speer (CC Mike)
- [ ] Pick 3 objects to scan:
  - Small (pack of gum sized) — e.g., stapler, tape dispenser
  - Medium (shoe box sized) — e.g., toolbox, small cabinet
  - Large (desk sized) — e.g., desk, filing cabinet

### Stevin
- [ ] Install Blender (latest)
- [ ] Set up camera / phone for photography
- [ ] Read photography guide (`Research/02-photography-guide.md`)
- [ ] Read rigging guide (`Research/05-rigging-and-interaction.md`)

### Sebastian
- [ ] Install RealityScan Desktop (free <$1M rev)
- [ ] Read software comparison (`Research/04-software-comparison.md`)
- [ ] Familiarize with RealityScan interface

### Gavin
- [ ] Install Unity 2022 LTS + URP template
- [ ] Read Unity import pipeline guide (`Research/03-unity-import-pipeline.md`)
- [ ] Set up Unity project with folder structure
- [ ] Install XR Interaction Toolkit package

---

## Phase 2: First Object Sprint (Days 2–4)

Everyone works on the **small object** end-to-end together to learn the full pipeline.

### Stevin — Photograph
- [ ] Photograph small object (100+ photos, good lighting, plain background)
- [ ] Follow photography guide (manual mode, f/8-f/11, ISO 100, consistent WB)
- [ ] Include scale reference in some shots
- [ ] Hand off photos to Sebastian

### Sebastian — Process
- [ ] Import photos into RealityScan Desktop
- [ ] Generate 3D model
- [ ] Export as FBX
- [ ] Hand off FBX to Stevin
- [ ] Note what worked / didn't work

### Stevin — Clean & Rig in Blender
- [ ] Import FBX into Blender
- [ ] Clean mesh (delete loose geometry, fill holes)
- [ ] Decimate to ~20k–50k triangles
- [ ] Separate interactive part (if applicable — a lid, door, button)
- [ ] Set pivot point at hinge/rotation center
- [ ] Export as FBX (FBX All, -Z Forward, Y Up, Apply Transform)
- [ ] Hand off cleaned FBX to Gavin

### Gavin — Unity Integration
- [ ] Import FBX into Unity (URP project)
- [ ] Extract materials/textures, assign URP Lit shader
- [ ] Verify scale (1 unit = 1 meter)
- [ ] Add Rigidbody + Collider + XR Grab Interactable
- [ ] Add physics joint (HingeJoint or ConfigurableJoint) to interactive part
- [ ] Test interaction — does it grab/open/rotate?

### Checkpoint
- [ ] **Small object works in Unity with basic interaction**
- [ ] Team knows the full pipeline end-to-end

---

## Phase 3: Parallel Production (Days 5–8)

Pipeline is proven. Now go fast on the remaining 2 objects.

### Stevin — Photograph + Rig Both
- [ ] Photograph medium object (150+ photos)
- [ ] Hand photos to Sebastian → get back FBX → clean & rig in Blender
- [ ] Photograph large object (200+ photos, walk around method)
- [ ] Hand photos to Sebastian → get back FBX → clean & rig in Blender
- [ ] Export both rigged FBX files to Gavin

### Sebastian — Process Both
- [ ] Process medium object photos in RealityScan → export FBX
- [ ] Process large object photos in RealityScan → export FBX
- [ ] Hand off FBX files to Stevin for Blender work

### Gavin — Import & Wire Up Both
- [ ] Import medium model into Unity, add interaction
- [ ] Import large model into Unity, add interaction
- [ ] Set up demo scene with all 3 objects
- [ ] Basic performance check (runs smooth?)

### Checkpoint
- [ ] **All 3 objects interactive in Unity**

---

## Phase 4: Documentation (Days 9–10)

The docs are the real deliverable. Each person documents their part.

### Stevin — Photography & Blender Docs
- [ ] Photography guide: camera settings, lighting, number of photos, tips per size
- [ ] Blender cleanup guide: step-by-step with screenshots
- [ ] Mesh separation & pivot point guide
- [ ] Rigging guide: how to add interactive parts
- [ ] FBX export settings cheat sheet

### Sebastian — RealityScan Software Docs
- [ ] RealityScan step-by-step guide with screenshots
- [ ] Import settings, processing options, export settings
- [ ] Lessons learned: what worked, what failed, workarounds
- [ ] Tips for different object sizes

### Gavin — Unity Pipeline Docs
- [ ] Unity import guide: settings, materials, scale
- [ ] XR interaction guide: joints, grab interactable, colliders
- [ ] Project structure & naming conventions
- [ ] Performance tips for VR

### Checkpoint
- [ ] **Documentation is self-contained — someone else can follow it**

---

## Phase 5: Polish & Present (Days 11–12)

- [ ] Final QA on all 3 models
- [ ] Fix any remaining issues
- [ ] Prepare presentation slides (July 2)
- [ ] Practice presentation
- [ ] Submit everything

---

## Final Deliverables

- [ ] 3 interactive photogrammetry models in Unity (small, medium, large)
- [ ] Photography guide (Stevin)
- [ ] Blender cleanup & rigging guide (Stevin)
- [ ] RealityScan software guide (Sebastian)
- [ ] Unity import & interaction guide (Gavin)
- [ ] Presentation

---

## Quick Reference: The Pipeline

```
STEVIN: Photos (DSLR/phone, 100-400 shots)
  ↓
SEBASTIAN: RealityScan Desktop (photos → 3D mesh, export FBX)
  ↓
STEVIN: Blender (clean → decimate → separate parts → set pivots → export FBX)
  ↓
GAVIN: Unity (import → materials → colliders → joints → XR Grab Interactable)
  ↓
DONE (interactive 3D model in VR)
```
