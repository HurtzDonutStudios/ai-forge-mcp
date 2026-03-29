# AI Forge MCP Package — Installation Guide

## How to Get Access

### Step 1: Purchase a Subscription

Visit [hurtzdonut.com](https://hurtzdonut.com) and select your tier:

| Tier | MSRP | Founder Price | Seats | Best For |
|------|------|---------------|-------|----------|
| **Solo** | $79/mo | **$35/mo** | 1 | Solo developers getting started with AI game asset production |
| **Duo** | $139/mo | **$65/mo** | 2 | Developers working with a partner or collaborator |
| **Studio** | $249/mo | **$149/mo** | 5 | Studios and teams who need multiple seats and priority support |
| **Enterprise** | Custom | Custom | Custom | Dedicated support, custom integrations, SLA |

All tiers include the full MCP package — all 250 tools across all 10 servers. **Founder pricing is locked forever** at your signup rate — prices go to MSRP at general availability.

### Step 2: Complete Checkout & Get Your License Key

After selecting your tier, you'll be taken to checkout. Once payment completes:

1. Your license key is **automatically generated** and displayed on the success page
2. You'll see download buttons for your platform (Windows, macOS, Linux)
3. **Copy your license key immediately** — you'll also receive it via email as a backup

### Step 3: Download & Install the MCP Package

Click the download button for your operating system. The package includes an `INSTALL_PROMPT.md` file — paste its contents into your AI agent (Claude Code, Cursor, or Windsurf) and the agent will walk you through the complete setup automatically.

**Supported platforms:**

| Platform | Size | Notes |
|----------|------|-------|
| Windows | ~22MB | Windows 10/11 |
| macOS | ~21MB | Apple Silicon (M1+) and Intel |
| Linux | ~38MB | Ubuntu 22.04+, Debian 12+ |

### Step 4: Install Required Software

Before running the MCP package, ensure you have the following installed:

#### Required (All Free)

| Software | Version | Download |
|----------|---------|----------|
| Blender | 4.0+ | [blender.org/download](https://blender.org/download) |
| Unreal Engine | 5.3+ | [unrealengine.com/download](https://unrealengine.com/download) |
| Python | 3.10+ | [python.org/downloads](https://python.org/downloads) |
| Node.js | 18+ | [nodejs.org](https://nodejs.org) |
| MCP-compatible AI agent | Latest | Claude Code, Cursor, or Windsurf |

#### Optional — Substance Suite (Adobe Subscription)

These improve texture and material quality but are **not required**. The pipeline works without them.

| Software | Purpose |
|----------|---------|
| Substance Painter | Texture painting, mesh map baking |
| Substance Designer | Procedural material graph authoring |
| Substance Sampler | Photo-to-material scanning |

#### Optional — AI Backends (All Free, Open Source)

These enable AI-powered rigging and animation. They require an NVIDIA GPU with CUDA support.

| Backend | What It Does | GPU Requirement |
|---------|-------------|-----------------|
| UniRig | AI auto-rigging (skeleton + skin weights) | 8GB+ VRAM |
| HY-Motion | AI locomotion animation | 24GB+ VRAM |
| AnimationGPT | AI combat animation | CUDA GPU |

### Step 5: Define Your Game

On first run, the AI will walk you through defining your game project — genre, art style, species, classes, world design, and quality targets. This configuration is saved and used to tailor every asset the pipeline produces to your specific game.

---

## Technical Requirements Checklist

Before your first session, verify:

- Blender 4.0+ installed and launchable
- Unreal Engine 5.3+ installed with a project created
- Python 3.10+ installed (`python --version` in terminal)
- Node.js 18+ installed (`node --version` in terminal)
- MCP-compatible AI agent installed (Claude Code, Cursor, or Windsurf)
- License key obtained from checkout success page
- MCP package downloaded and extracted
- (Optional) Substance apps installed with bridge plugins loaded
- (Optional) UniRig / HY-Motion / AnimationGPT installed for AI rigging and animation

---

## Recommended Hardware

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| GPU | NVIDIA RTX 3060 (8GB VRAM) | NVIDIA RTX 4080+ (16GB+ VRAM) |
| RAM | 32GB | 64GB+ |
| CPU | 8-core modern processor | 16-core (AMD 7950X3D or Intel 14900K+) |
| Storage | SSD, 50GB free | NVMe SSD, 100GB+ free |
| OS | Windows 10/11, macOS 12+, Ubuntu 22.04+ | Windows 11 or Ubuntu 22.04+ |

> **Note:** AI backends (UniRig, HY-Motion, AnimationGPT) require NVIDIA CUDA GPUs. AMD GPUs are not currently supported for AI rigging and animation. The core pipeline (Blender, Substance, UE5 automation) works on any GPU.

---

## Support

| Tier | Support Channel |
|------|----------------|
| Solo | Community Discord |
| Duo | Priority email support + community Discord |
| Studio | Direct Slack channel with the development team |
| Enterprise | Dedicated support contact + SLA |

For setup issues, check the troubleshooting section in the INSTALL_PROMPT.md included with your download, or reach out through your tier's support channel.

---

*AI Forge MCP Package — Hurtz Donut Studios*
*Built by Jeremy Fawcett*
