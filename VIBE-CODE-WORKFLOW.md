# VIBE CODE SESSION — Grok-Build Complete Setup

> Token-min · Def: GSD · Spec: OpenSpec · BMAD · GSD  
> **Tok** (approx): JSON ≈ **2342** · MD ≈ **941** · method: chars/4 | words×1.3

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
// _viewport.scss
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

**System boost** (prepend to every build/spec call):
```
You are a senior staff engineer and product designer.
Produce production-ready, polished, complete output.
Prefer clarity, correctness, accessibility, and modern standards.
No placeholders, no TODOs, no incomplete stubs unless explicitly asked.
Match prismic tokens, viewport rules, and Grok-Build scaffold exactly.
```

**Rules**
- Build + Spec phases → always `quality=max`
- Never emit incomplete code under max mode
- Prefer full files over diffs
- Viewport anti-zoom + 16px inputs are non-negotiable

**SDK**
```python
from litellm import completion
r = completion(
  model="azure/<flagship-deployment>",
  messages=[...],
  temperature=0.3,
  max_tokens=8192,
  top_p=0.9,
)
```

## 1. Phase Loop
```
GRILL → MAP → SPEC → BUILD → DEPLOY
```
1. GRILL-ME.md → shared understanding  
2. Wayfinder → ROADMAP + tickets  
3. GSD (def): discuss → plan → execute → verify → ship  
4. Build (scaffold below)  
5. CF Pages (± SW)

## 2. Grok-Build Scaffold
```
/
├── index.html          # viewport meta locked
├── package.json
├── vite.config.ts
├── tsconfig.json
├── .env.example
├── public/
│   ├── favicon.ico
│   ├── robots.txt
│   └── manifest.webmanifest
└── src/
    ├── main.tsx
    ├── App.tsx
    ├── routes/
    ├── components/
    ├── hooks/
    ├── lib/
    ├── assets/
    └── styles/
        ├── _tokens.scss    # prismic tokens
        ├── _viewport.scss  # anti-zoom
        ├── _base.scss
        └── main.scss
```

### index.html head (required)
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#2BBE8B">
<title>{{app_name}}</title>
<link rel="icon" href="/favicon.ico">
```

### Scripts
```
dev          → vite
build        → tsc -b && vite build
preview      → vite preview
deploy:pages → wrangler pages deploy dist
deploy:full  → pages + worker
```

### .env.example
```
AZURE_API_KEY=
AZURE_API_BASE=
AZURE_API_VERSION=2024-08-01-preview
VITE_API_URL=
DATABASE_URL=
```

## 3. Prismic Tokens (CSS vars)
```scss
:root {
  --accent: #2BBE8B; --ink: #151515; --ink-soft: #505050;
  --bg: #FFF; --muted: #A4A4A4; --line: rgba(238,238,238,1);
  --space-1:4px … --space-8:96px;
  --radius-sm:2px; --radius-md:8px; --radius-lg:12px; --radius-pill:999px;
  --max-w: 1280px;
}
```

## 4. IDE Routing
```
/vibe       → session
/vibe/ade   → ADE
/vibe/ai    → LiteLLM Azure IDE
```

## 5. Pre-ship Checks
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

## 6. Quick Start
```
1. /grill-me <idea>
2. Wayfinder → map + tickets
3. /gsd-workflow
4. Scaffold (above) + apply _viewport.scss + _tokens.scss
5. pnpm i && pnpm dev
6. Deploy CF Pages (± SW)
```

---
*grok-build mode · viewport-locked · Azure-LiteLLM ready*
