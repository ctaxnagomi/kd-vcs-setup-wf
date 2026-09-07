# VIBE CODE SESSION — Grok-Build Complete Setup

> Token-min · Def: GSD · Spec: OpenSpec · BMAD · GSD  
> **Tok** (approx): JSON ≈ **2768** · MD ≈ **1191** · method: chars/4 | words×1.3

## 0. Core
| Key | Val |
|-----|-----|
| Mode | grok-build |
| UI/UX | prismic.io tokens |
| Stack | TanStack + Vite + pnpm |
| Web/Mobile | RN \| Bootstrap \| HTML5 \| SCSS |
| Game | three.js \| WebGL |
| Backend | Python \| Express |
| DB | SQLite \| Postgres-Supabase |
| Deploy | CF Pages · CF SW · Pages+SW |
| Agents | BrowserOS-neo · snapDOM/compactDOM/snapShot/html2canvas |
| Fmt | ctecx Instruct Formatter |
| Learn | GRILL-ME.md · Wayfinder |
| LLM | LiteLLM → Azure |

## 0.1 Viewport + Anti-Zoom (mandatory)
```html
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```
```scss
input, textarea, select { font-size: 16px; }
@media (hover: none) and (pointer: coarse) {
  input, textarea, select { font-size: 16px; }
}
button, a, [role="button"] { touch-action: manipulation; }
body {
  padding: env(safe-area-inset-top) env(safe-area-inset-right)
           env(safe-area-inset-bottom) env(safe-area-inset-left);
}
```
**Forbid**: `maximum-scale=1` · `user-scalable=no`

## 0.2 LiteLLM + Azure
```
ENV: AZURE_API_KEY · AZURE_API_BASE · AZURE_API_VERSION
Model: azure/<deployment>
Proxy: model_list → os.environ/AZURE_API_*
SDK: from litellm import completion
```

## 0.3 Max Quality (API / LiteLLM Azure)
When using Azure key → force **high-end** output:

| Param | Value | Why |
|-------|-------|-----|
| temperature | **0.3** | Precise, less random |
| top_p | **0.9** | Controlled diversity |
| max_tokens | **8192** | Full files, no truncation |
| timeout | **120s** | Allow deep generation |
| retries | **3** | Resilience |

**Model**: prefer flagship Azure deployment (`azure/<flagship>`)  
**Alias**: `vibe-max` in proxy config

**System boost**: senior staff engineer + production-ready, no stubs, match prismic + viewport + scaffold.

**SDK**
```python
from litellm import completion
r = completion(model="azure/<flagship-deployment>", messages=[...], temperature=0.3, max_tokens=8192, top_p=0.9)
```

## 0.4 Local Data Container (privacy)
When using **cloud Azure API key**, user local data + inputs stay on-device.

```
.vibe/local/          ← vibe-local-vault
├── inputs/           # user typed / pasted inputs
├── uploads/          # files user attached
├── session-cache/    # agent session scratch
├── dom-snapshots/    # BrowserOS / snapDOM captures
└── env.local         # non-secret local overrides
```

**Rules**
- Azure/LiteLLM receives **prompt text only** — no filesystem sync
- Never send raw `.env`, vault paths, keys, or unapproved uploads
- Only redacted/scoped excerpts the task needs
- BrowserOS-neo + DOM capture remain local unless user opts in
- API key = cloud auth only; it does **not** open the local vault

**Scaffold**
```
.vibe/local/**  → gitignored
.gitignore      → .vibe/local/ · .env · .env.local · *.pem · *.key
```

**Boundary**
| May send to LLM | Never send |
|-----------------|------------|
| Task prompt | Raw .env / keys |
| User-approved attachments | Full local vault |
| Redacted context | Unapproved uploads |
| | Private session-cache |

## 1. Phase Loop
```
GRILL → MAP → SPEC → BUILD → DEPLOY
```
1. GRILL-ME.md → shared understanding  
2. Wayfinder → ROADMAP + tickets  
3. GSD (def): discuss → plan → execute → verify → ship  
4. Build (scaffold + viewport + vault)  
5. CF Pages (± SW)

## 2. Grok-Build Scaffold
```
/
├── index.html
├── package.json
├── vite.config.ts
├── .env.example
├── .gitignore
├── .vibe/local/     # gitignored vault
├── public/
└── src/
    ├── main.tsx
    ├── App.tsx
    ├── routes/
    ├── components/
    └── styles/
        ├── _tokens.scss
        ├── _viewport.scss
        └── main.scss
```

### Scripts
```
dev → vite | build → tsc -b && vite build | deploy:pages → wrangler pages deploy dist
```

## 3. Pre-ship Checks
- [ ] viewport meta present + correct
- [ ] input/textarea/select ≥ 16px
- [ ] no maximum-scale / user-scalable=no
- [ ] safe-area env() applied
- [ ] touch-action: manipulation
- [ ] prismic tokens in :root
- [ ] LiteLLM Azure env ready
- [ ] CF Pages deploy works
- [ ] quality=max used for build/spec
- [ ] flagship Azure deployment selected
- [ ] local vault present (.vibe/local)
- [ ] .vibe/local gitignored
- [ ] no local vault path in LLM prompts by default

## 4. Quick Start
```
1. /grill-me <idea>
2. Wayfinder → map + tickets
3. /gsd-workflow
4. Scaffold + _viewport.scss + _tokens.scss + .vibe/local
5. pnpm i && pnpm dev
6. Deploy CF Pages (± SW)
```

---
*grok-build · viewport-locked · Azure-LiteLLM · local-vault privacy*
