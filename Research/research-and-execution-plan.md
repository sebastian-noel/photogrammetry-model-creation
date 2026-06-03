# Research & Execution Plan — Photogrammetry Model Creation

## What Are We Being Asked To Do?

**In plain terms:** Lauren Speer's team at KCNSC (nuclear, DOE-related) needs to train people on physical equipment using VR. Instead of manually 3D-modeling every piece of equipment (which takes forever), they want to photograph real objects and convert those photos into 3D models that can be interacted with in Unity — open doors, turn knobs, pull drawers, etc.

**We are NOT building a product.** We are building a **documented process/pipeline** that their XR developers can follow. Think of it as a train-the-trainer playbook.

### The 5 Concrete Deliverables

1. **Photography Guide** — How to properly photograph objects for photogrammetry (lighting, distance, angles, resolution, distortion avoidance)
2. **Photogrammetry Pipeline** — Step-by-step process to convert photos into a 3D model using desktop-based software (RealityScan preferred)
3. **Rigging Methodology** — How to take that static 3D model and add interactive parts (hinges for doors, rotation for knobs, sliding for drawers)
4. **Unity Import Pipeline** — How to get the rigged model into Unity for VR use
5. **Proof of Concept Models** — 3 demo models at different scales:
   - **Small** = pack of gum sized
   - **Medium** = shoe box sized
   - **Large** = computer desk sized

### Hard Constraints

- All processing must be **local** (no cloud-based tools)
- Photos taken with **DSLR/mirrorless camera** (phone OK for capturing images, but no LiDAR or sensor suites)
- Software must be **desktop-based** (RealityScan preferred, alternatives OK if approved)
- Documentation is the **primary deliverable** — the models are proof that the process works

---

## Timeline (5 Weeks)

| Week | Phase | Dates (approx) |
|------|-------|-----------------|
| W1 | Intro / Planning / Pre-production | June 3 – June 6 |
| W2 | Planning / Pre-production | June 9 – June 13 |
| W3–4 | Development / Production | June 16 – June 27 |
| W5 | Testing / Submission | June 30 – July 2 |

- **June 4th** — No lab
- **July 2** — Final Presentations
- **~20 hrs/week** per person

---

## Team Roles & Work Split

### Stevin George — Pipeline & Integration Lead
**Focus:** Unity import pipeline, project coordination, documentation assembly

| Week | Tasks |
|------|-------|
| W1 | Install Unity + RealityScan. Research Unity import formats (FBX, OBJ, glTF). Set up project repo structure. Send intro email to Lauren (CC Mike). |
| W2 | Test importing a sample photogrammetry model into Unity. Document import settings, scale issues, material/texture handling. Research mesh optimization (decimation, UV cleanup). |
| W3 | Import team's photogrammetry models into Unity. Troubleshoot materials, scale, performance. Document the full import pipeline step-by-step. |
| W4 | Help with rigging integration in Unity. Test interactive models in VR. Refine documentation with screenshots and troubleshooting tips. |
| W5 | Assemble final documentation package. Prepare demo/presentation. Final QA on all 3 models in Unity. |

### Sebastian Noel — Photogrammetry & Photography Lead
**Focus:** Photo capture process, photogrammetry software, 3D model generation

| Week | Tasks |
|------|-------|
| W1 | Install RealityScan (+ research alternatives: Meshroom, 3DF Zephyr, Agisoft Metashape — must be local/desktop). Research best practices for photogrammetry photo capture. |
| W2 | Conduct test shoots with small object. Document photography methodology (lighting setup, number of photos needed, overlap %, distance, backgrounds, camera settings). Test RealityScan with sample photos. |
| W3 | Photograph and process the **small** and **medium** objects. Iterate on capture technique. Document what works and what doesn't (lessons learned). |
| W4 | Photograph and process the **large** object. Refine all 3 models (clean up mesh, fix holes, optimize polygon count). Write photography guide. |
| W5 | Finalize photography documentation. Help with presentation. Polish any remaining model issues. |

### Gavin Heaver — Rigging & Interaction Lead
**Focus:** Making static models interactive (rigging, joints, animations)

| Week | Tasks |
|------|-------|
| W1 | Install Unity + Blender (or equivalent rigging tool). Research rigging workflows for photogrammetry meshes. Understand how rigging differs for scanned vs. modeled objects. |
| W2 | Research and test: How to separate parts of a photogrammetry mesh (e.g., isolate a door from a cabinet). Test rigging a simple model with a hinge joint. Document rigging approach. |
| W3 | Rig the **small** object for basic interaction. Rig the **medium** object (doors, drawers, knobs as applicable). Document the step-by-step rigging process. |
| W4 | Rig the **large** object. Test all rigged models for interaction in Unity (grab, rotate, open/close). Troubleshoot and iterate. |
| W5 | Finalize rigging documentation with screenshots/video. Help with presentation. Final interaction testing. |

---

## Research Plan (Weeks 1–2)

### Questions to Investigate

#### Photography & Capture
- [ ] How many photos are needed per object at each size?
- [ ] What camera settings produce the best results (aperture, ISO, focal length)?
- [ ] What lighting setup minimizes shadows and reflections?
- [ ] What background works best (turntable? plain backdrop?)?
- [ ] How does object material affect results (shiny, transparent, dark)?

#### Photogrammetry Software
- [ ] Does RealityScan work fully offline/desktop? (It has a cloud component — verify)
- [ ] What are the best local/desktop alternatives? (Meshroom is free + open source, 3DF Zephyr has a free tier, Agisoft Metashape is paid)
- [ ] What export formats does each support? (FBX, OBJ, glTF needed for Unity)
- [ ] What are the polygon count / texture resolution tradeoffs?

#### Rigging
- [ ] Can you rig directly in Unity, or do you need Blender/Maya first?
- [ ] How do you cleanly separate parts of a scanned mesh for independent movement?
- [ ] What joint types are needed? (hinge for doors, slider for drawers, rotary for knobs)
- [ ] How do you handle texture seams when splitting a mesh?

#### Unity Integration
- [ ] What import format gives the best results? (FBX vs OBJ vs glTF)
- [ ] How do you handle scale consistency across different-sized objects?
- [ ] What's the polygon budget for VR performance?
- [ ] How do you set up basic XR interaction (grab, rotate, open)?

### Research Sources
- Epic/RealityScan official documentation
- Unity photogrammetry import guides
- Blender rigging tutorials for scanned meshes
- Academic papers on photogrammetry best practices
- YouTube tutorials (Meshroom, RealityScan workflows)

---

## Communication Plan

- **Initial email to Lauren Speer** — Team names + project, CC Mike Aiken
- **Periodic check-ins** — Mini sprint updates via Teams or email
- **Preferred channels:** Teams or Email (no Discord)
- **Format:** "Here's what we did. Is this still what you want?"

---

## Things to Ask Lauren / Mike ASAP

1. How do we access RealityScan (license/download)?
2. Do they have a preferred list of approved alternative software?
3. Can they provide example objects or should we source our own?
4. What Unity version are they using?
5. Any specific VR headset/platform we should target?
6. What does "exact deliverables" look like — do they want a written doc, video walkthrough, or both?
7. Do they have a DSLR we can borrow, or do we use our own equipment?

---

## Final Deliverables Checklist

- [ ] Photography Guide (lighting, distance, angles, camera settings, tips per object size)
- [ ] Photogrammetry Pipeline Doc (software setup, photo import, model generation, mesh cleanup)
- [ ] Rigging Methodology Doc (mesh separation, joint setup, interaction configuration)
- [ ] Unity Import Pipeline Doc (format, import settings, materials, scale, VR interaction setup)
- [ ] Small object — photographed, modeled, rigged, imported into Unity
- [ ] Medium object — photographed, modeled, rigged, imported into Unity
- [ ] Large object — photographed, modeled, rigged, imported into Unity
- [ ] Final presentation (July 2)
