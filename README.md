# AI Forge MCP Package

**The first full-pipeline MCP orchestration layer for AAA game asset production.**

250 AI-callable tools across 10 MCP servers. One prompt builds a complete game-ready asset — from concept art to UE5-ready FBX with textures, rig, animations, LODs, and material setup.

94,000+ lines of production code. Built by [Hurtz Donut Studios](https://hurtzdonut.com).

---

## What Is the AI Forge MCP Package?

AI Forge is an MCP (Model Context Protocol) orchestration layer that connects your AI coding agent to five professional applications simultaneously: **Blender**, **Substance Painter**, **Substance Designer**, **Substance Sampler**, and **Unreal Engine 5**.

Instead of manually switching between apps, exporting, re-importing, and tweaking settings — you describe what you want, and the AI pipeline builds it. Every tool has been tested against AAA quality standards.

### Who Is This For?

- **Solo developers** who want AAA-quality assets without a 50-person art team
- **Small studios** looking to 10x their asset throughput
- **Hobbyists** who know what they want but not how to wrangle five DCC apps
- **Technical artists** who want to automate repetitive pipeline work

Works with **Claude Code**, **Cursor**, and **Windsurf**.

---

## The 10 MCP Servers

| Server | Tools | What It Controls |
|--------|-------|-----------------|
| **ForgeBlender** | 97 | Blender — mesh cleanup, UV unwrapping, materials, rigging, LOD generation |
| **GameForge** | 74 | Unreal Engine 5 — world building, material instances, VFX, PCG |
| **ForgeDesigner** | 25 | Substance Designer — procedural material graphs |
| **ForgePainter** | 17 | Substance Painter — texture painting, smart materials |
| **ForgeSampler** | 8 | Substance Sampler — photo-to-material scanning |
| **ForgeMotion** | 7 | Animation — AI locomotion and combat animation |
| **ForgeRig** | 6 | Rigging — AI auto-skeleton and skinning |
| **ForgeNPC** | 6 | NPC Systems — dialogue, personality, conversation trees |
| **ForgeVoice** | 6 | Lipsync — facial animation and emotion classification |
| **ForgeHunyuan** | 4 | 3D Generation — text and image to 3D mesh |

**Total: 250 tools.** Every tool is callable through MCP — your AI agent uses them automatically based on what the asset needs.

---

## How It Works — The Full Pipeline

You provide three things:

1. **A .glb file** — your 3D asset (or generate one from text/image)
2. **A reference image** — concept art, screenshot, or photo
3. **A description** — what it is, what it's for, any details to emphasize

The pipeline handles the rest: cleanup, UV optimization, cinematic texturing, rigging, weight optimization, animation, LOD generation, and UE5 export. The AI agent orchestrates all 10 servers, routes between tools based on what's needed, and delivers game-ready files.

The pipeline adapts to your art style and your game's specific needs.

---

## ForgeRoom — Mission Control

ForgeRoom is the dashboard that ships with AI Forge. It's where you manage everything.

### Dashboard
Real-time overview of your pipeline, connected tools, and recent activity.

### Import Asset
Drop a .glb file and reference image, describe the asset, and launch the pipeline.

### Asset Library
Browse, search, filter, and compare every asset the pipeline has produced.

### Stat Engine
Roll stats for weapons, armor, items — with rarity tiers, procedural generation, and UE5 DataTable export.

### Projects
Organize assets into game projects with tagging and filtering.

### Document Forge
Write and manage game design documents (GDD, GSDD, lore bibles) with an AI co-writer.

### 3D Viewer
Inspect assets in-browser with WebGPU rendering, annotation tools, and screenshot capture.

### Rig Inspector
Visualize skeletons, test bone deformation, and request AI-driven rig adjustments.

### ForgeAnimator
Preview and edit animations, blend between clips, and export to UE5 animation sequences.

### Server Forge
Configure and deploy dedicated game servers — UE5 networking, matchmaking, and hosting setup.

---

## The 6 AI Backends

### Grok by xAI — Concept Art Generation
Generate reference images and concept art from text descriptions to feed into the pipeline.

### Hunyuan3D by Tencent — Text/Image to 3D Mesh
Convert text prompts or 2D images directly into .glb meshes for pipeline processing.

### UniRig by VAST-AI Research — AI Auto-Rigging (SIGGRAPH 2025)
Automatic skeleton prediction and skin weight generation. Drop in a mesh, get a production-ready rig.

### HY-Motion by Tencent — AI Locomotion Animation
1-billion parameter DiT model generating physics-aware locomotion from text descriptions.

### AnimationGPT — AI Combat Animation
Generate attack, dodge, block, and combo sequences from text.

### Claude by Anthropic — Pipeline Orchestration
The AI agent that ties it all together — reads your intent, selects the right tools, and manages the full pipeline.

---

## Species-Aware Animation Profiles

16 built-in profiles that adjust physics, gait, and movement style per species:

**Playable Characters:** Human, Elf, Dwarf, Orc, Ogre, Troll, Goblin, Undead, Demon, Dragon-Kin

**Creatures:** Canines, Large Quadrupeds, Serpents, Avian, Arachnids, Elementals

Custom profiles can be created for any species in your game.

---

## 5 Asset Pipelines

### Characters (Playable)
Full humanoid pipeline — mesh, textures, rig, weight optimization, locomotion + combat animations, lipsync.

### Creatures & NPCs
Adaptive skeleton rigging, species-specific animation profiles, dialogue and personality systems.

### Weapons
Mesh cleanup, PBR texturing, attachment point setup, UE5 socket configuration.

### Armor
Multi-piece assembly, material layering, LOD generation, physics cloth setup.

### Environments
Modular building, terrain materials, foliage distribution, lighting setup.

---

## Key Stats

| Metric | Value |
|--------|-------|
| MCP Servers | 10 |
| Total Tools | 250 |
| Lines of Code | 94,000+ |
| Applications Controlled | 5 (Blender, Substance Painter, Designer, Sampler, UE5) |
| AI Backends | 6 |
| Species Animation Profiles | 16 |
| Asset Pipelines | 5 |
| ForgeRoom Dashboard Modules | 10 |
| Art Style Presets | 4 |
| Security | License validation, encrypted credentials, forensic watermarking |

---

## Technical Requirements

### Required (Free)

| Software | Version |
|----------|---------|
| Blender | 4.0+ |
| Unreal Engine | 5.3+ |
| Python | 3.10+ |
| Node.js | 18+ |
| AI Agent | Claude Code, Cursor, or Windsurf |

### Optional (Improves Quality)

Substance Painter, Substance Designer, and Substance Sampler improve texture and material quality but are **not required**. The pipeline works without them using Blender-native processing.

### Optional AI Backends (Free, Open Source)

| Backend | GPU Requirement |
|---------|----------------|
| UniRig | NVIDIA GPU, 8GB+ VRAM |
| HY-Motion | NVIDIA GPU, 24GB+ VRAM |
| AnimationGPT | NVIDIA CUDA GPU |

### Hardware Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| GPU | NVIDIA RTX 3060 (8GB) | NVIDIA RTX 4080+ (16GB+) |
| RAM | 32GB | 64GB+ |
| CPU | 8-core | 16-core (AMD 7950X3D / Intel 14900K+) |
| Storage | SSD, 50GB free | NVMe SSD, 100GB+ free |

---

## Pricing

### Early Access — Founder Pricing

| Tier | MSRP | Founder Price | Seats | What You Get |
|------|------|---------------|-------|-------------|
| **Solo** | $79/mo | **$35/mo** | 1 | Full pipeline — all 250 tools, all 10 servers |
| **Duo** | $139/mo | **$65/mo** | 2 | Everything in Solo + second seat |
| **Studio** | $249/mo | **$149/mo** | 5 | Everything in Duo + priority support + pipeline customization |
| **Enterprise** | Custom | Custom | Custom | Dedicated support, custom integrations, SLA |

**All tiers include the full MCP package.** No feature gating — every customer gets every tool. Founder pricing is locked forever at your signup rate.

Visit [hurtzdonut.com](https://hurtzdonut.com) to get started.

---

## The Proof of Work — AI Legends

AI Legends is the fantasy MMO being built entirely with AI Forge. It's our flagship game and the ultimate test of the pipeline — every asset, every animation, every material in the game is produced by the same tools available to AI Forge customers.

11 playable species. Realm management. AI agents as real players. Built in UE5 with Rust backend.

If the pipeline can build an MMO, it can build your game.

---

## Competitive Landscape

AI Forge is the only MCP package that orchestrates the full asset production pipeline across multiple DCC applications. Other tools handle individual steps — mesh generation, texturing, or rigging in isolation. AI Forge connects them all into a single automated workflow controlled by your AI agent.

---

## Attribution & Licenses

AI Forge MCP Package integrates with the following open-source projects:

- **UniRig** — VAST-AI Research (SIGGRAPH 2025)
- **HY-Motion** — Tencent
- **AnimationGPT** — Open source
- **Hunyuan3D** — Tencent

All AI backends are used under their respective open-source licenses. AI Forge does not modify or redistribute these projects — it connects to them via MCP when installed locally.

---

## Get Access

1. Visit [hurtzdonut.com](https://hurtzdonut.com)
2. Select your tier and complete checkout
3. Download the MCP package for your platform
4. Paste the included setup prompt into your AI agent
5. Start building

---

*AI Forge MCP Package — Hurtz Donut Studios*
*Built by Jeremy Fawcett*
