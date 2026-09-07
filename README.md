# kd-vcs-setup-wf

**VIBE CODE SESSION** — Grok-Build quantized workflow for high-end app scaffolding.

## What's inside

| File | Purpose |
|------|---------|
| `vibe-code-workflow.json` | Machine-ready workflow (token-quantized) |
| `VIBE-CODE-WORKFLOW.md` | Human / agent readable mirror |

## Stack

- **UI/UX** — [prismic.io](https://prismic.io) design tokens
- **Framework** — TanStack
- **Web / Mobile** — React Native · Bootstrap · HTML5 · SCSS
- **Game / Browser** — three.js · WebGL
- **Backend** — Python · Express
- **DB** — SQLite · Postgres (Supabase)
- **Deploy** — Cloudflare Pages ± Service Worker
- **LLM** — LiteLLM → Azure (`AZURE_API_KEY` / `AZURE_API_BASE` / `AZURE_API_VERSION`)
- **Agents** — BrowserOS-neo · snapDOM / compactDOM / snapShot / html2canvas
- **Spec kits** — **GSD** (default) · OpenSpec · BMAD
- **Learn** — GRILL-ME.md · Wayfinder

## Viewport & Anti-Zoom (mandatory)

```html
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```

```scss
input, textarea, select { font-size: 16px; } /* prevents iOS/Android auto-zoom */
button, a, [role="button"] { touch-action: manipulation; }
body { padding: env(safe-area-inset-*); }
```

**Forbidden:** `maximum-scale=1` · `user-scalable=no`

## Max Quality (Azure / LiteLLM)

| Param | Value |
|-------|-------|
| temperature | `0.3` |
| top_p | `0.9` |
| max_tokens | `8192` |
| timeout | `120s` |
| retries | `3` |

Model alias: `vibe-max` → flagship Azure deployment.

## Local Data Container (privacy)

When using the **cloud Azure API key**, user local data and inputs stay on-device:

```
.vibe/local/          ← vibe-local-vault
├── inputs/
├── uploads/
├── session-cache/
├── dom-snapshots/
└── env.local
```

- Azure/LiteLLM receives **prompt text only** — no filesystem sync
- Never send raw `.env`, vault paths, keys, or unapproved uploads
- API key = cloud auth only; it does **not** open the local vault
- `.vibe/local/` is gitignored

## Phase loop

```
GRILL → MAP → SPEC → BUILD → DEPLOY
```

1. **GRILL-ME.md** — interview to shared understanding  
2. **Wayfinder** — map + tickets  
3. **GSD** — discuss → plan → execute → verify → ship  
4. **Build** — Grok-Build scaffold + prismic tokens + viewport lock  
5. **Deploy** — Cloudflare Pages (± Service Worker)

## Quick start

```bash
# 1. Copy workflow into your agent context
# 2. Set Azure env
export AZURE_API_KEY=...
export AZURE_API_BASE=https://<resource>.openai.azure.com/
export AZURE_API_VERSION=2024-08-01-preview

# 3. Run session
/grill-me <idea>
# then Wayfinder → GSD → scaffold → deploy
```

## IDE routing

```
/vibe       → session entry
/vibe/ade   → ADE adapter
/vibe/ai    → LiteLLM Azure IDE
```

## License

MIT
