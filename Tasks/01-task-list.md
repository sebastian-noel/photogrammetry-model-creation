# Task List — Photogrammetry Model Creation

## Week 1: Intro / Planning / Pre-production (June 3–6)

### All Team Members
- [ ] Install Unity (2022 LTS or later)
- [ ] Install RealityScan Desktop (formerly RealityCapture) — free for <$1M revenue
- [ ] Install Blender (latest stable)
- [ ] Send intro email to Lauren Speer (CC Mike Aiken) with team names + project
- [ ] Ask Lauren: Unity version they use, VR headset target, how to access software, DSLR availability
- [ ] Read through all research docs in this repo

### Stevin (Pipeline & Integration Lead)
- [ ] Research Unity import formats — FBX vs OBJ vs glTF (see `03-unity-import-pipeline.md`)
- [ ] Set up Unity project with proper folder structure
- [ ] Configure URP (Universal Render Pipeline) for VR
- [ ] Test importing a sample photogrammetry model (download one from Sketchfab)
- [ ] Document import settings that work

### Sebastian (Photogrammetry & Photography Lead)
- [ ] Research photography best practices (see `02-photography-guide.md`)
- [ ] Research photogrammetry software options (see `04-software-comparison.md`)
- [ ] Test RealityScan Desktop with a simple object (phone, cup, etc.)
- [ ] Document camera settings and lighting setup
- [ ] Identify 3 test objects: small (gum-sized), medium (shoe box), large (desk)

### Gavin (Rigging & Interaction Lead)
- [ ] Research rigging workflows for scanned meshes (see `05-rigging-and-interaction.md`)
- [ ] Learn Blender mesh cleanup basics (decimation, hole filling, artifact removal)
- [ ] Practice mesh separation in Blender (splitting parts from a single mesh)
- [ ] Research Unity XR Interaction Toolkit setup
- [ ] Test a simple hinge joint in Unity with a placeholder cube

---

## Week 2: Planning / Pre-production (June 9–13)

### Stevin
- [ ] Import Sebastian's test scan into Unity
- [ ] Document scale calibration process (1 Unity unit = 1 meter)
- [ ] Test material/texture import settings (URP Lit shader setup)
- [ ] Set up XR Interaction Toolkit in Unity project
- [ ] Create template prefab structure for photogrammetry assets
- [ ] Document Blender → Unity FBX export settings

### Sebastian
- [ ] Photograph small object (100-200 photos, turntable setup)
- [ ] Process small object in RealityScan Desktop
- [ ] Document photography methodology (lighting, angles, overlap, camera settings)
- [ ] Evaluate output quality — identify what works and what doesn't
- [ ] Start photographing medium object

### Gavin
- [ ] Clean up Sebastian's first scan in Blender (remove artifacts, fill holes)
- [ ] Practice decimation (target 10k-50k triangles for VR)
- [ ] Test mesh separation — isolate a movable part
- [ ] Set correct pivot points for separated parts
- [ ] Test texture baking from high-poly to low-poly
- [ ] Document rigging approach

---

## Week 3: Development / Production (June 16–20)

### Stevin
- [ ] Import cleaned/rigged small model into Unity
- [ ] Set up XR Grab Interactable on interactive parts
- [ ] Configure physics joints (HingeJoint, ConfigurableJoint)
- [ ] Test VR interaction (grab, rotate, open/close)
- [ ] Start importing medium model
- [ ] Document full import pipeline with screenshots

### Sebastian
- [ ] Process medium object scan
- [ ] Photograph large object (200-400+ photos, walk-around method)
- [ ] Start processing large object
- [ ] Iterate on capture technique based on lessons learned
- [ ] Write photography guide draft

### Gavin
- [ ] Rig small object for interaction (doors/knobs/drawers as applicable)
- [ ] Rig medium object
- [ ] Document step-by-step rigging process with screenshots
- [ ] Test rigged models in Unity with Stevin
- [ ] Fix texture seams and pivot point issues

---

## Week 4: Development / Production (June 23–27)

### Stevin
- [ ] Import and set up large model in Unity
- [ ] Test all 3 models for VR interaction
- [ ] Performance profiling (polygon count, draw calls, frame rate)
- [ ] Add LOD groups if needed
- [ ] Compile full Unity import pipeline documentation
- [ ] Set up demo scene with all 3 models

### Sebastian
- [ ] Finalize all 3 photogrammetry models (mesh cleanup, optimization)
- [ ] Finalize photography guide (lighting, distance, angles, camera settings per size)
- [ ] Document photogrammetry software pipeline (step-by-step from photos to 3D model)
- [ ] Add troubleshooting tips and lessons learned

### Gavin
- [ ] Rig large object for interaction
- [ ] Final interaction testing on all 3 models
- [ ] Finalize rigging methodology documentation
- [ ] Add troubleshooting section (common issues and fixes)
- [ ] Help Stevin with Unity interaction setup

---

## Week 5: Testing / Submission (June 30 – July 2)

### All Team Members
- [ ] Final QA on all 3 models in Unity VR
- [ ] Review and polish all documentation
- [ ] Ensure documentation is self-contained (train-the-trainer quality)
- [ ] Prepare final presentation for July 2
- [ ] Practice presentation
- [ ] Submit all deliverables

### Final Deliverables Checklist
- [ ] Photography Guide (`02-photography-guide.md`)
- [ ] Unity Import Pipeline Doc (`03-unity-import-pipeline.md`)
- [ ] Software Comparison (`04-software-comparison.md`)
- [ ] Rigging & Interaction Methodology (`05-rigging-and-interaction.md`)
- [ ] Small object — photographed, modeled, rigged, imported, interactive in Unity
- [ ] Medium object — photographed, modeled, rigged, imported, interactive in Unity
- [ ] Large object — photographed, modeled, rigged, imported, interactive in Unity
- [ ] Final presentation slides
- [ ] Unity project (clean, organized, documented)
