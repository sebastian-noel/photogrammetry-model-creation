# Photography Guide for Photogrammetry

## Overview

This guide covers how to photograph objects for photogrammetry — the process of creating 3D models from 2D images. The goal is consistent, sharp, well-lit photos with high overlap between shots.

---

## 1. Camera Settings

| Setting | Recommendation | Why |
|---------|---------------|-----|
| **Mode** | Full Manual (M) | Prevents exposure/WB shifts between frames |
| **Aperture** | f/8 to f/11 | Maximizes depth of field without diffraction softening |
| **ISO** | 100 (max 200) | Minimizes noise — noise creates false surface detail |
| **Shutter Speed** | 1/80s minimum handheld | Motion blur is the #1 killer of photogrammetry scans |
| **Focal Length** | 35mm–50mm prime (fixed) | No zoom. Never go below 20mm (distortion ruins accuracy) |
| **White Balance** | Manual / Daylight | Never use auto WB — it shifts between frames |
| **Format** | RAW preferred, high-quality JPEG acceptable | RAW gives post-processing control for consistency |

### Critical Rules
- **Lock everything.** Aperture, shutter speed, ISO, white balance, and focal length must stay constant across ALL photos in a session.
- **Never zoom** during a capture session.
- **Use a tripod** whenever possible — especially for small and medium objects.
- **Use a remote shutter release** or 2-second timer to avoid camera shake.

---

## 2. Lighting Setup

### Goal
Flat, even, diffused illumination. No harsh shadows. No specular highlights. The object must look the same from every angle.

### Recommended Setup
- **2–4 diffused light sources** (softboxes, LED panels with diffusion fabric, or shoot-through umbrellas)
- Place lights symmetrically around the object
- Add **white foam board reflectors** to fill shadows on underside/back
- Total budget setup: ~$100 (2 LED panels + diffusion fabric + foam boards)

### Advanced: Cross-Polarization
- Place **linear polarizing film** over your lights
- Use a **circular polarizer (CPL)** on your camera lens
- Rotate the CPL to eliminate specular reflections
- This reveals true surface color (albedo) without reflections
- Best method for shiny objects without spraying them

### What to Avoid
- On-camera flash (inconsistent, harsh)
- Direct sunlight (hard shadows that shift as you move)
- Mixed color temperature light sources
- Windows or changing ambient light in the background
- Any light source visible in the frame

### Indoor vs Outdoor
- **Indoor is strongly preferred** — you control the light
- **Outdoor only on overcast days** — acts as a giant natural softbox
- Never shoot in direct sunlight

---

## 3. Photo Capture Technique

### Number of Photos by Object Size

| Object Size | Example | Photos Needed | Method |
|-------------|---------|---------------|--------|
| **Small** | Pack of gum | 100–200 | Turntable, 5–10° increments, 3–4 height tiers |
| **Medium** | Shoe box | 150–300 | Turntable, 10° increments, 3–4 height tiers |
| **Large** | Computer desk | 200–400+ | Walk around, photo every 1–2 steps, 3 height levels |

### Overlap
- **60–80% overlap** between consecutive images
- Every surface point must appear in **at least 3 images** from different angles
- More overlap = better reconstruction. When in doubt, take more photos.

### Angle Coverage (Tiers/Rings)

Capture the object in concentric rings at different elevation angles:

```
Ring 4: ~70° above (looking down)        ___
Ring 3: ~45° above                      /   \
Ring 2: ~20° above                     |  O  |  ← Object
Ring 1: 0° (eye level / equator)        \___/
Ring 0: below equator (if needed)
```

- Minimum 3 rings for small/medium objects
- 3–4 rings + detail passes for large objects
- For the **bottom of the object**: flip it over and capture separately, or elevate on a minimal support and shoot upward

### Distance from Object
- Fill **60–80% of the frame** with the object
- Stay at a **consistent distance** throughout each ring
- Too close = loses alignment context
- Too far = loses detail

### Turntable vs Walking Around
- **Turntable** (small/medium): More consistent data. Camera on tripod stays fixed. Rotate object 5–10° per shot. Wait for turntable to fully stop before shooting.
- **Walking around** (large): Maintain consistent orbit distance. Stop completely before each shot. Mark positions on the floor with tape for consistency.

### Background
- **Plain, matte, featureless** — solid white, gray, or black
- **Seamless paper backdrop** curved behind the object (for turntable setups)
- No patterns — the software may try to reconstruct the background
- Note: Some software (Meshroom) struggles with featureless backgrounds on turntable setups. RealityScan and Metashape handle masked backgrounds well.

---

## 4. Object Preparation

### Reflective / Shiny Surfaces
- **Best:** Scanning spray (AESUB, Attblime) — creates temporary matte coating that evaporates, no residue
- **Budget:** Light dusting of baby powder, talcum, or dry shampoo spray
- **Non-contact:** Cross-polarization (polarizing film on lights + CPL on camera)

### Transparent Objects
- **Must be coated** — photogrammetry fundamentally cannot reconstruct transparent surfaces
- Scanning spray or chalk spray is mandatory
- After coating, treat as a normal matte object

### Dark / Black Objects
- Increase lighting intensity significantly
- Lightly dust with scanning spray or powder for contrast
- Use a **light gray background** (not white) to avoid extreme contrast
- Slightly overexpose compared to meter reading, but don't clip highlights

### Scale Reference
- Place a **calibrated scale bar or ruler** next to (not on) the object
- Include a **color/gray card** for white balance reference
- Measure and record **at least 2 known distances** on/near the object for calibration
- Use **coded targets** (printed markers) if your software supports them for automatic alignment

---

## 5. Common Mistakes to Avoid

1. **Motion blur** — always check sharpness at 100% zoom
2. **Inconsistent exposure** — auto-exposure or auto-WB shifting between frames
3. **Insufficient overlap** — software can't align images without shared features
4. **Changing lighting** — different times of day, mixing flash with ambient
5. **Moving the object** between shots (or bumping the turntable)
6. **Featureless/reflective/transparent surfaces** without preparation
7. **Zooming** or changing focal length during a session
8. **Rushing** — uneven coverage, missed angles, duplicate positions
9. **Harsh shadows** — they appear as "features" that shift between viewpoints
10. **Vibration** — unstable tripods, nearby machinery, wind

### Quality Checklist Before Processing
- [ ] All images are sharp (spot-check at 100% zoom)
- [ ] Exposure is consistent across entire set
- [ ] White balance is consistent (no color shifts)
- [ ] Complete coverage — no missing angles or blind spots
- [ ] Overlap is at least 60% between adjacent images
- [ ] Every visible point appears in at least 3 images from different angles
- [ ] No moving elements in scene (people, pets, curtains)
- [ ] Scale reference visible in some images
- [ ] Background is clean and non-distracting
- [ ] No lens flare, light sources in frame, or extreme exposure issues

---

## 6. Size-Specific Tips

### Small Objects (pack of gum)
- Use a **turntable** on a stable table with camera on tripod
- **Macro lens** or extension tubes may be needed
- Depth of field is extremely shallow at macro distances — use **f/11 or higher**
- Consider **focus stacking** (multiple focus planes per position, merged)
- Cross-polarization is especially valuable at this scale
- Turntable increments: **5–10°**, 3–4 elevation tiers
- Use **remote shutter release** to avoid any camera shake
- Place small scale ruler and color card on turntable surface beside object
- Total: **100–200+ images** (more if focus stacking)

### Medium Objects (shoe box)
- Standard **tabletop turntable** (lazy Susan or motorized)
- **50mm prime at f/8–f/11** is typically perfect
- Camera on tripod, **0.5–1m from object**
- **10° turntable increments**, 3 elevation tiers = ~108 images minimum, 150–200 safer
- 2–4 softboxes/LED panels for even coverage
- White or gray seamless paper backdrop
- This is the **sweet spot** — most forgiving size category

### Large Objects (desk)
- **Walk around** the object (no turntable)
- Use **35mm lens** on full-frame. Avoid ultra-wide angles.
- Capture in **3 orbital rings** at different heights:
  - Knee level
  - Waist level
  - Eye level / standing
  - (Optional) Above — stand on step stool and shoot down
- Take a photo **every 1–2 steps**, consistent distance (1–2m)
- After orbits, do **detail passes** of complex areas (handles, joints, legs, undersides)
- For the **underside**: flip the object (capture separately and merge) or get low and shoot upward
- **Mark positions on floor with tape** for consistency
- Total: **200–400+ images**
- Consider **breaking into sections** with generous overlap between sections
- Place **multiple scale bars** around the object

---

## Sources

- [Agisoft Metashape — Best Photos for Photogrammetry](https://www.agisoftmetashape.com/how-to-capture-the-best-photos-for-photogrammetry-drone-and-dslr-tips/)
- [PhotoModeler — Recommended Camera Settings](https://www.photomodeler.com/pm-kb/recommended-camera-settings-photogrammetry/)
- [Knight Lab — 4 Key Components to Photogrammetry](https://studio.knightlab.com/results/photojournalism3D/the-4-key-components-to-photogrammetry-capture/)
- [PixPro — Cross Polarization Photogrammetry](https://www.pix-pro.com/blog/cross-polarization)
- [3D Scan Store — Scanning Reflective Objects](https://www.3dscanstore.com/blog/3d-scanning-reflective-objects)
- [PixPro — Photogrammetry Checklists](https://www.pix-pro.com/blog/checklist)
- [OpenScan — How Many Photos Do You Really Need](https://openscan.eu/blogs/news/optimizing-3d-scans-how-many-photos-do-you-really-need)
- [Peter Falkingham — Small Object Setup](https://peterfalkingham.com/2018/08/24/my-small-object-photogrammetry-setup/)
- [Hamilton College — Photogrammetry Start to Finish](https://libguides.hamilton.edu/c.php?g=1130779&p=8373067)
