# Photogrammetry Software Comparison

## Overview

All options below are **local/desktop** — no cloud processing. This is a hard requirement from the stakeholder.

---

## Quick Comparison

| Software | Price | FBX | OBJ | glTF | GPU | Platforms | Quality | Ease |
|----------|-------|-----|-----|------|-----|-----------|---------|------|
| **RealityScan Desktop** | Free (<$1M rev) | Yes | Yes | No | NVIDIA required | Win, Linux (CLI) | Excellent | Moderate |
| **Agisoft Metashape** | $179–$3,499 | Yes | Yes | Yes | NVIDIA or AMD | Win, Mac, Linux | Excellent | Moderate |
| **3DF Zephyr** | Free–$4,200 | Yes | Yes | Yes | Any DirectX | Windows | Very Good | Easy |
| **Meshroom** | Free (open source) | No* | Yes | Partial | NVIDIA required | Win, Linux | Good | Moderate |
| **COLMAP** | Free (open source) | No | No | No | NVIDIA recommended | Win, Mac, Linux | Good (SfM only) | Hard |
| **Regard3D** | Free (open source) | No | Yes | No | None | Win, Mac, Linux | Basic | Easy |

*Requires conversion through Blender

---

## Detailed Breakdown

### 1. RealityScan Desktop (Recommended)

**Developer:** Capturing Reality (Epic Games)

> **WARNING:** There are TWO products called RealityScan:
> - **RealityScan Desktop** (formerly RealityCapture) — fully local. **This is the one we want.**
> - **RealityScan Mobile** — phone app that processes in the CLOUD. **Do NOT use.**

**Pricing:**
- **Free** for individuals/companies with annual gross revenue under $1M
- $1,250/year per seat for companies over $1M
- Perpetual license ~$3,750

**System Requirements:**
- Windows 10/11 (64-bit) or Linux (CLI only)
- NVIDIA GPU with CUDA 3.0+ and 4GB+ VRAM (RTX 3080+ with 10GB+ recommended)
- 16GB RAM minimum, 32GB+ recommended
- **No macOS support**

**Pros:**
- Fastest processing speed of any photogrammetry software
- Industry-leading output quality
- Free for most indie/academic teams
- Can combine photos + laser scans
- Handles very large datasets efficiently (out-of-core algorithms)
- Backed by Epic Games

**Cons:**
- NVIDIA GPU required (no AMD)
- No macOS support
- Steeper learning curve
- Revenue-gated pricing

**Export Formats:** OBJ, FBX, PLY, XYZ

---

### 2. Agisoft Metashape (Best Alternative)

**Developer:** Agisoft LLC

**Pricing:**
- Standard: $179 (perpetual)
- Professional: $3,499 (perpetual)
- **Educational: $59 (Standard), $549 (Professional)**

**System Requirements:**
- Windows, macOS, Linux
- NVIDIA or AMD GPU (OpenCL or CUDA)
- 16GB RAM for <200 photos, 32–64GB for medium projects

**Pros:**
- Cross-platform (Windows, macOS, Linux)
- Supports both NVIDIA and AMD GPUs
- All three export formats (FBX, OBJ, glTF)
- Specific **Unity export presets**
- Excellent documentation and community
- Perpetual license
- Very precise and controllable

**Cons:**
- Slower than RealityScan for large datasets
- Professional version is expensive

**Export Formats:** OBJ, FBX, glTF/GLB, PLY, COLLADA, 3DS, DXF, PDF 3D, and more

---

### 3. 3DF Zephyr (Easiest to Use)

**Developer:** 3Dflow SRL

**Pricing:**
- Free version (limited to 50 photos per project)
- Lite: ~$149–199 (500 photo limit)
- Pro: ~$3,200 (unlimited)

**System Requirements:**
- Windows only (64-bit)
- Any DirectX 9.0c compatible GPU with 1GB+ VRAM
- 16GB RAM minimum

**Pros:**
- Free version for evaluation
- All three export formats
- Works with NVIDIA and AMD GPUs
- AI-powered classification and masking
- Video input support (extract frames from video)
- Available on Steam
- Most beginner-friendly

**Cons:**
- Windows only
- Free version limited to 50 photos (insufficient for quality results)
- Photo limits on Lite version (500)

**Export Formats:** OBJ, FBX, glTF/GLB, COLLADA, PLY, USD, 3MF, and more

---

### 4. Meshroom (Best Free Option)

**Developer:** AliceVision Association (open source)

**Pricing:** Completely free (MPLv2 license)

**System Requirements:**
- Windows and Linux (no macOS)
- NVIDIA GPU with CUDA 3.0+ required for quality results
- CPU-only "draft" mode available but quality is significantly reduced
- 32GB RAM recommended

**Pros:**
- Completely free and open source
- Node-based visual pipeline (highly customizable)
- Good quality for a free tool
- Active development community

**Cons:**
- NVIDIA GPU required for quality results
- No macOS support
- No native FBX export (convert through Blender)
- Slower than commercial alternatives
- Documentation is sparse

**Export Formats:** OBJ, STL, PLY (recent versions added glTF/GLB)

---

### 5. COLMAP (Research Tool)

**Developer:** Johannes Schoenberger (ETH Zurich / Microsoft)

**Not recommended as standalone solution.** Excellent SfM (Structure from Motion) engine but lacks complete meshing, texturing, and export pipeline. Only consider if building a custom pipeline.

---

### 6. Regard3D (Learning Only)

**Not recommended for production.** Single developer, slow updates, known texture bugs. Only suitable for learning photogrammetry concepts on hardware without a GPU.

---

## Our Recommendation

### Primary: RealityScan Desktop
If team has Windows + NVIDIA GPUs. Free, fastest, best quality. This is the stakeholder's preferred tool.

### Backup: Agisoft Metashape (Standard — $179 or $59 educational)
If anyone uses macOS or AMD GPUs. Has direct Unity export presets and all three required formats.

### Evaluation: Meshroom
Free option for prototyping. Pair with Blender for FBX/glTF conversion.

---

## Sources

- [RealityScan Official](https://www.realityscan.com/)
- [RealityScan 2.1 Release](https://www.cgchannel.com/2025/11/epic-games-releases-realityscan-2-1/)
- [RealityScan Hardware Recommendations (Puget Systems)](https://www.pugetsystems.com/solutions/photogrammetry-workstations/realityscan/hardware-recommendations/)
- [AliceVision / Meshroom](https://alicevision.org/)
- [3DF Zephyr Official](https://www.3dflow.net/3df-zephyr-photogrammetry-software/)
- [Agisoft Metashape System Requirements](https://www.agisoft.com/downloads/system-requirements/)
- [Agisoft Metashape File Formats](https://www.agisoftmetashape.com/what-file-formats-does-agisoft-metashape-support-a-complete-guide/)
- [Agisoft Unity/Unreal Export Settings](https://www.agisoftmetashape.com/best-export-settings-in-metashape-for-unity-unreal-engine-and-cesium/)
- [COLMAP Official](https://colmap.github.io/)
- [Regard3D Official](https://www.regard3d.org/)
- [Best Photogrammetry Software 2026 (SkyeBrowse)](https://www.skyebrowse.com/news/posts/best-photogrammetry-software)
