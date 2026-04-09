# AI Forge MCP Package — Pipeline Documentation

## Overview

The AI Forge MCP Package processes 3D game assets through an 11-step pipeline that spans five professional applications — Blender, Substance Painter, Substance Designer, Substance Sampler, and Unreal Engine 5 — plus six AI backends. The entire pipeline is controlled by a single AI agent through the Model Context Protocol (MCP).

**Input Requirements:**
1. A `.glb` file — the 3D asset to be processed
2. A reference image — concept art, screenshot, or photo showing the target look
3. A plain-English description — what the asset is, its role in the game, any visual details to emphasize

**Output:**
A fully rigged, textured, animated, lip-synced, UE5-ready asset with LODs, collision, and proper material setup — delivered directly into your Unreal Engine 5 project.

---

## The 11 Pipeline Steps

### Step 1: Concept Art Generation
**Server:** External (Grok by xAI)
**What happens:** The AI generates high-quality reference images based on the customer's description. These images establish the visual target for every subsequent step. If the customer provides their own concept art or reference images, this step is skipped.
**Output:** Reference image(s) that define color palette, silhouette, material properties, and mood.

### Step 2: 3D Mesh Generation
**Server:** ForgeHunyuan (4 tools)
**What happens:** Hunyuan3D (Tencent) takes the concept art or a text prompt and generates raw 3D geometry. The system can produce single assets or batches. Output meshes are in .glb format, ready for the cleanup pipeline.
**Output:** Raw .glb mesh file with initial geometry and basic vertex colors.

### Step 3: Mesh Cleanup
**Server:** ForgeBlender (uses `clean_mesh` tool)
**What happens:** The mesh is imported into Blender and cleaned automatically. Loose geometry is removed, duplicate vertices are merged, normals are recalculated to face outward, and any non-manifold edges are fixed. The original mesh topology is preserved — nothing is remeshed or simplified at this stage.
**Output:** Clean, watertight mesh with consistent normals and no degenerate geometry.

### Step 4: UV Unwrapping
**Server:** ForgeBlender (uses `verify_uv_quality` → `smart_uv_unwrap` tools)
**What happens:** Existing UV maps are checked for quality — overlap detection, stretch analysis, coverage measurement. If UVs are missing or poor quality, the system generates optimized UV layouts using angle-based projection with island margin control. UV quality is verified before proceeding.
**Output:** Production-quality UV layout with minimal stretch, no overlap, and proper island margins.

### Step 5: Texture Enhancement
**Server:** ForgePainter (17 tools) + ForgeDesigner (25 tools) + ForgeBlender (fallback)
**What happens:** This is the most complex step and operates in three possible paths:

**Path A — Substance Painter (when connected):**
The mesh is exported as FBX and loaded into Substance Painter. Mesh maps are baked automatically — ambient occlusion, curvature, normal, position, thickness, and ID maps. A layer stack is built on top of the original textures, adding depth, wear, and material variation. Final textures are exported as BaseColor, Normal, and ORM (Occlusion/Roughness/Metallic) maps.

**Path B — Substance Designer (when connected):**
A procedural material graph is created in Designer with noise-driven roughness variation, height detail, ambient occlusion, and micro-normal generation. Style-specific parameters are applied automatically — horror_fantasy uses grunge noise with heavy wear, photorealistic uses clean perlin noise, stylized uses soft clouds. Textures are exported and available for blending with Painter output or standalone use.

**Path C — Blender-Native (fallback when Substance unavailable):**
The existing base color is preserved (baked to a high-resolution image as a safety backup), then five enhancement layers are composited on top: (1) preserved original colors, (2) ambient occlusion depth darkening, (3) curvature-based edge highlights, (4) cavity darkening for recesses, (5) style-specific cinematic color grade. The result is a preservation-first enhancement that never strips or replaces the original look.

**Output:** Production-quality PBR texture set — BaseColor, Normal, ORM — with cinematic enhancement applied.

### Step 6: Rigging
**Server:** ForgeRig (6 tools)
**What happens:** UniRig (VAST-AI, SIGGRAPH 2025) analyzes the mesh geometry and automatically predicts a skeleton hierarchy with proper joint placement. For humanoid characters, this produces a 32-bone skeleton with finger bones. For creatures, a 24-bone skeleton adapted to the body plan. The skeleton is generated, validated, and parented to the mesh — no manual bone placement required.
**Output:** Mesh with properly placed skeleton, ready for weight painting.

### Step 7: Weight Painting Optimization
**Server:** ForgeBlender (6-tool chain)
**What happens:** A full weight optimization pipeline runs in sequence:
1. `auto_weight_paint` — Initial automatic weight assignment based on bone proximity
2. `insert_edge_loops_at_joints` — Adds geometry at joints for cleaner deformation
3. `prune_weak_weights` — Removes bone influences below threshold to reduce artifacts
4. `limit_bone_influences` — Caps per-vertex bone count (typically 4) for game engine compatibility
5. `verify_weight_symmetry` — Checks left/right symmetry for bilateral characters
6. `test_bone_deformation` — Poses the mesh through key positions to verify clean deformation

**Output:** Game-ready weight painting with clean deformation at all major joints.

### Step 8: Animation
**Server:** ForgeMotion (7 tools)
**What happens:** Two AI backends handle different movement types:

**Locomotion (HY-Motion by Tencent):** A 1-billion parameter diffusion transformer model generates natural movement from text descriptions. "Walk forward cautiously," "sprint at full speed," "jump over obstacle" — each prompt produces physically plausible motion capture-quality animation. Species animation profiles automatically adjust physics: an ogre's run is heavy and ground-shaking, an elf's run is light and agile.

**Combat (AnimationGPT):** A combat-specialized model trained on 8,700 annotated combat sequences generates contextual attack and defense animations. Prompts include weapon type, attack style, speed, and power: "two-handed sword overhead slash, heavy, slow" produces different animation than "dagger quick stab, light, fast."

**Output:** Animation clips (locomotion + combat) adapted to the character's species and weapon loadout.

### Step 9: NPC Dialogue & Lipsync
**Server:** ForgeNPC (6 tools) + ForgeVoice (6 tools)
**What happens:** ForgeNPC generates dialogue trees, personality profiles, and conversation systems for speaking characters. ForgeVoice takes the dialogue audio and generates facial animation — viseme sequences synchronized to speech, emotion-classified expressions, and UE5-compatible morph target data. Batch processing handles multiple characters efficiently.
**Output:** Dialogue system data + lipsync animation curves ready for UE5 import.

### Step 10: LOD Generation
**Server:** ForgeBlender (uses `generate_lod_chain` tool)
**What happens:** A multi-level-of-detail chain is generated from the high-poly mesh. Each LOD level reduces polygon count by a controlled ratio while preserving silhouette and key features. Typical chain: LOD0 (full detail), LOD1 (50%), LOD2 (25%), LOD3 (12.5%). Each LOD is validated for visual quality before export.
**Output:** LOD chain (4 levels) with proper screen-size transition distances for UE5.

### Step 11: UE5 Delivery
**Server:** GameForge (74 tools)
**What happens:** The finished asset — mesh, skeleton, textures, animations, LODs — is exported as FBX and imported into the customer's Unreal Engine 5 project. Materials are created and assigned using the exported texture maps. LOD settings are configured. Collision is generated. The asset is placed in the content browser with proper naming conventions, ready for use in the game world.
**Output:** A complete, game-ready asset inside UE5 with materials, LODs, collision, and animations.

---

## How the 6 AI Backends Connect

```
Customer prompt: "Create a gruesome undead berserker"
         │
         ▼
    ┌─────────┐
    │  Claude  │ ◄── Orchestrator: reads pipeline config, makes creative decisions
    └────┬────┘
         │ calls tools across all 10 MCP servers
         │
         ├──► Grok (xAI) ──────────► concept art / reference images
         │
         ├──► Hunyuan3D (Tencent) ──► raw 3D mesh from concept art
         │
         ├──► ForgeBlender ─────────► cleanup, UVs, materials, LODs, export
         │
         ├──► UniRig (VAST-AI) ────► skeleton + skin weights
         │
         ├──► HY-Motion (Tencent) ─► locomotion animations
         │    AnimationGPT ────────► combat animations
         │
         ├──► ForgePainter ────────► texture painting + mesh map baking
         │    ForgeDesigner ───────► procedural material graphs
         │    ForgeSampler ────────► photo-scanned materials
         │
         ├──► ForgeNPC ────────────► dialogue + personality
         │    ForgeVoice ──────────► lipsync animations
         │
         └──► GameForge ───────────► UE5 import + material setup + world placement
```

Each AI backend is called through its dedicated MCP server. Claude orchestrates the sequence, passing outputs from one server as inputs to the next. The customer sees a single conversation — the multi-tool orchestration happens automatically.

---

## Available Art Styles

The texture enhancement system supports multiple art styles, each with tuned parameters:

| Style | Description |
|-------|------------|
| `horror_fantasy` | Gore-soaked horror RPG. Deep desaturation, blood-red midtones, crushed blacks, sickly green shadows. Heavy grunge and wear. |
| `photorealistic` | Neutral color grade, physically accurate materials, clean surface detail. |
| `stylized` | Painterly quality, saturated colors, exaggerated features, soft surface detail. |
| `cel_shaded` | Hard edges, flat color regions, outline emphasis, minimal surface noise. |

Custom styles can be created for customers on the Obsidian tier.

---

## Sacred Rules

The pipeline operates under strict principles that protect asset quality:

1. **The .glb is sacred.** The original mesh, its colors, form, and character are never stripped, cleared, or replaced. Every operation adds quality on top of what exists.
2. **Use MCP tools, not inline code.** The 250 tools have been tested and validated. The AI agent calls tools — it does not write replacement scripts.
3. **Match the reference image.** The customer provides a visual target. The pipeline hits it.
4. **Route through Substance when available.** Painter and Designer produce superior results. If connected, they are used. If they crash or are unavailable, the Blender-native path produces excellent results as a fallback.
5. **Never guess.** If a parameter is unclear, the AI checks the tool documentation. If the customer's intent is unclear, the AI asks.

---

*AI Forge MCP Package — Hurtz Donut Studios*
*Built by Jeremy Fawcett*
