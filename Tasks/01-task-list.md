# MVP Task List — Photogrammetry Model Creation

> **Goal:** Get 3 objects (small, medium, large) photographed → 3D modeled → rigged → interactive in Unity. Document the process. Ship fast.

---

## Phase 1: Setup (Day 1)

**Everyone does this simultaneously:**

- [ ] Install Unity 2022 LTS + URP template
- [ ] Install RealityScan Desktop (free <$1M rev)
- [ ] Install Blender (latest)
- [ ] Send intro email to Lauren Speer (CC Mike)
- [ ] Pick 3 objects to scan:
  - Small (pack of gum sized) — e.g., stapler, tape dispenser
  - Medium (shoe box sized) — e.g., toolbox, small cabinet
  - Large (desk sized) — e.g., desk, filing cabinet

---

## Phase 2: First Object Sprint (Days 2–4)

Everyone works on the **small object** end-to-end together to learn the full pipeline.

### Sebastian — Capture & Process
- [ ] Photograph small object (100+ photos, phone or DSLR, good lighting, plain background)
- [ ] Process in RealityScan Desktop → export as FBX
- [ ] Note what worked / didn't work

### Gavin — Clean & Rig
- [ ] Import FBX into Blender
- [ ] Clean mesh (delete loose geometry, fill holes)
- [ ] Decimate to ~20k–50k triangles
- [ ] Separate interactive part (if applicable — a lid, door, button)
- [ ] Set pivot point at hinge/rotation center
- [ ] Export as FBX (FBX All, -Z Forward, Y Up, Apply Transform)

### Stevin — Unity Integration
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

Now that you know the pipeline, split and go fast.

### Sebastian — Capture Both Remaining Objects
- [ ] Photograph medium object (150+ photos)
- [ ] Process medium object in RealityScan → FBX
- [ ] Photograph large object (200+ photos, walk around method)
- [ ] Process large object in RealityScan → FBX

### Gavin — Clean & Rig Both
- [ ] Clean + decimate + separate + rig medium object in Blender
- [ ] Clean + decimate + separate + rig large object in Blender
- [ ] Export both as FBX

### Stevin — Import & Wire Up Both
- [ ] Import medium model into Unity, add interaction
- [ ] Import large model into Unity, add interaction
- [ ] Set up demo scene with all 3 objects
- [ ] Basic performance check (runs smooth in VR?)

### Checkpoint
- [ ] **All 3 objects interactive in Unity**

---

## Phase 4: Documentation (Days 9–10)

The docs are the real deliverable. Split and write.

### Sebastian — Photography & Software Docs
- [ ] Photography guide: camera settings, lighting, number of photos, tips per size
- [ ] Software guide: RealityScan step-by-step with screenshots
- [ ] Lessons learned: what worked, what failed, workarounds

### Gavin — Rigging & Blender Docs
- [ ] Blender cleanup guide: step-by-step with screenshots
- [ ] Mesh separation & pivot point guide
- [ ] Rigging guide: how to add interactive parts
- [ ] Export settings cheat sheet

### Stevin — Unity Pipeline Docs
- [ ] Unity import guide: settings, materials, scale
- [ ] XR interaction guide: joints, grab interactable, colliders
- [ ] Project structure & naming conventions
- [ ] Assemble all docs into final package

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
- [ ] Photography guide
- [ ] Photogrammetry software guide (RealityScan)
- [ ] Blender cleanup & rigging guide
- [ ] Unity import & interaction guide
- [ ] Presentation

---

## Quick Reference: The Pipeline

```
PHOTOS (DSLR/phone, 100-400 shots)
  ↓
REALITYSCAN DESKTOP (photos → 3D mesh, export FBX)
  ↓
BLENDER (clean mesh → decimate → separate parts → set pivots → export FBX)
  ↓
UNITY (import → materials → colliders → physics joints → XR Grab Interactable)
  ↓
DONE (interactive 3D model in VR)
```
