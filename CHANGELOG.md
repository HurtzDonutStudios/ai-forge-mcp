# AI Forge MCP Package — Changelog

All notable updates to the AI Forge MCP Package are documented here.

---

## v1.4.0 — April 8, 2026

**ForgeRoom UI Overhaul & Security Audit**

- **10 Theme Color System** — ForgeRoom now ships with 10 complete UI themes (Default Forge, Midnight Ember, Arctic Steel, Solar Flare, Deep Ocean, Neon Cyber, Forest Sage, Royal Amethyst, Blood Moon, Obsidian Gold). Theme picker in Account Settings with instant swap and localStorage persistence.
- **Demo Data Elimination** — Removed all hardcoded fake data from ForgeRoom: fake pipeline activity (Goblin Warrior, Iron Longsword), fake rig skeleton (66-line humanoid stub), and demo deployment alerts. Replaced with proper empty states and API-first patterns with graceful fallbacks.
- **Real GLB Skeleton Parser** — Rig Inspector now parses actual bone hierarchies from uploaded .glb files using Three.js GLTFLoader. Detects bone count, IK chains, max influences, and vertex groups from real meshes.
- **Security: Auth Token Fix** — Moved authentication tokens from URL query parameters to Authorization headers across all API calls. Tokens in URLs leak via server logs, browser history, and referrer headers.
- **Alert-to-Toast Migration** — Converted all 25+ browser alert() calls to the themed toast notification system with proper 3-argument signature (type, title, message).
- **Rig Inspector Activation** — Removed "Coming Soon" label, connected to real file upload and pipeline API endpoints.
- **Asset Detail Actions** — Added Resume Pipeline, Re-Export FBX, and Duplicate Asset functions with proper async API calls and fallback handling.

---

## v1.3.0 — March 29, 2026

**5 New MCP Servers & Massive Tool Expansion**

- **ForgeMaya** (20 tools) — Full Autodesk Maya automation: scene management, mesh cleanup, UV unwrapping, materials, joint chains, skin binding, animation, FBX/OBJ export
- **ForgeHoudini** (20 tools) — SideFX Houdini automation: procedural generation, heightfields, VEX wrangling, simulations (RBD, FLIP, Pyro, Vellum), terrain erosion, HDA creation
- **ForgeAI** (6 tools) — Pipeline guidance via locally-hosted Ollama model: troubleshooting, code review, asset spec generation
- **ForgeKnowledge** (6 tools) — TF-IDF knowledge base: search across 166 training documents, agent profiles, pipeline references
- **ForgePool** (5 tools) — DCC Pool Manager: instance acquisition/release, pool scaling, health monitoring across all DCC application pools
- **Forge Daemon** — Background service managing all MCP servers and up to 50 concurrent AI agent sessions with multi-port allocation (Layer 2: Job Queue, Layer 3: Background Service, Layer 4: 50-Agent Studio)
- **50 Agent Prompt Files** — All 50 specialized AI agents fully defined with identity, responsibilities, tool access, quality standards, and collaboration patterns
- **Server Storage Security** — Text-only VPS storage, 50MB per-customer quota, 100KB doc limit, binary file rejection at nginx + FastAPI, data retention policy with 7-email notification sequence
- **ForgeAnimHelper C++ Plugin** (1,169 lines) — UE5 Editor plugin enabling full AI automation of Animation Blueprints: state machines, blend spaces, transition conditions, sync groups
- **9 Workflow Knowledge Documents** (~260KB) — AI Enemy Pipeline, Advanced Asset Pipeline, Horror VFX, Game Systems, Multiplayer Setup, Cinematic Pipeline, Optimization Guide, Blender Simulation, Animation Blueprint
- **Total: 565 tools across 16 servers** (up from 278 tools across 11 servers)

---

## v1.2.0 — March 26, 2026

**Tier Rename & Pricing Update**

- Renamed subscription tiers to **Solo / Duo / Studio / Enterprise**
- Updated pricing: Solo $79/mo ($35 founder), Duo $139/mo ($65 founder), Studio $249/mo ($149 founder)
- Founder pricing locked forever at signup rate
- Seat limits: Solo 1, Duo 2, Studio 5, Enterprise custom
- Updated Stripe webhook tier detection to match new price thresholds
- Legacy tier names (Ember, Magma, Obsidian) mapped to new tiers for backward compatibility
- Updated admin console tier CSS and chart colors

---

## v1.1.0 — March 25, 2026

**Infrastructure & Security**

- **Stripe Integration** — Full checkout-to-license pipeline: Stripe webhook receives `checkout.session.completed`, auto-generates license key, determines tier from payment amount, creates customer record
- **License Heartbeat System** — Revalidation cycle; expired licenses are automatically revoked and users are booted from active sessions
- **Download System** — 3-OS auto-detection download modal (Windows 22MB, macOS 21MB, Linux 38MB); customer binary zips with INSTALL_PROMPT.md for auto-install
- **Stripe Success Modal** — Post-checkout success page with license key display, download buttons, and getting-started instructions
- **Admin Console Security** — 2FA (TOTP) with QR code setup and backup codes, password change, email change, account lockout after 5 failed attempts (15-minute cooldown), IP tracking on login, security status dashboard
- **ForgeRoom UI Polish** — SVG social links (Discord, X, Website, GitHub) with color-coded hover states, engine status bar with real-time connection indicators
- **Version Endpoint** — License server exposes `/version` for deployment verification
- **Database Cleanup** — Purged all test data from production database for accurate analytics

---

## v1.0.0 — March 25, 2026

**Initial Release**

- 250 MCP tools across 10 servers
- Full asset pipeline: Import → Clean → UV → Texture → Rig → Weight → Animate → LOD → Export
- Three texture enhancement paths (Substance Painter, Substance Designer, Blender-native)
- 4 art style presets: horror_fantasy, photorealistic, stylized, cel_shaded
- Cinematic color grading per style
- UE5-ready FBX export with proper settings
- AI-assisted rigging via UniRig integration
- AI locomotion via HY-Motion integration
- Hunyuan3D text/image-to-3D generation support
- License validation and binary distribution
- macOS (Apple Silicon + Intel) and Linux binaries

---

## Upcoming

- ForgeRoom Electron desktop app (Windows, macOS, Linux)
- Full pipeline end-to-end testing through ForgeRoom UI
- NVIDIA Kimodo text-to-motion integration (700+ hours training data)
- ForgeTexture engine (standalone Substance Designer + Painter replacement)
- Enhanced procedural wear system
- Expanded species animation profiles

---

*AI Forge MCP Package — Hurtz Donut Studios*
*Built by Jeremy Fawcett*
