# CLAUDE.md — CPD Log Project

This file is the single source of truth for how Claude Code should understand and work within this project. Keep it up to date.

Full project specification: [docs/project_spec.md](docs/project_spec.md)

---

## 1. Project Goals

Build a web-based tool that lets UK pharmacists and level 3 dispensing technicians create GPhC-compliant CPD (Continuing Professional Development) entries from a short questionnaire, using AI to generate the entry text.

**MVP goal:** A user answers questions about a learning activity (planned or unplanned), receives an AI-generated CPD entry, edits it, and downloads it as a plain text file. No login or account required.

**Success metric:** CPD entry creation takes roughly half the time of the current manual process.

---

## 2. Architecture Overview

```
Browser (React SPA)
        │
        │  POST /api/generate-cpd
        ▼
Express Server (Node.js)          ← API key stored as Replit Secret
        │
        │  Anthropic Claude API
        ▼
Generated CPD entry text
        │
        ▼
Returned to React frontend → user edits → downloads as .txt
```

| Layer | Technology |
|---|---|
| Hosting | Replit |
| Frontend | React + Tailwind CSS |
| Backend | Node.js + Express |
| AI / LLM | Anthropic Claude API |
| Database | None (MVP) |
| Linting | ESLint + Prettier |
| Unit Testing | Jest |
| E2E Testing | Playwright + Playwright MCP |

**Key rule:** The Anthropic API key lives server-side only (Replit Secret). It must never be referenced in any frontend code.

For deeper architecture detail see [docs/project_spec.md — Section 4](docs/project_spec.md).

---

## 3. Design, Style & UX Guides

- **Visual tone:** Professional. Clean layout, clear hierarchy, generous whitespace. Not corporate or clinical — approachable but credible.
- **CSS framework:** Tailwind CSS. Use utility classes. Avoid writing custom CSS unless Tailwind cannot cover the need.
- **Layout pattern:** Single-page app. The user moves through steps (select type → fill form → review output → download) without page reloads.
- **Loading state:** The AI call will take a few seconds. Always show a visible loading indicator while waiting for the response. Do not leave the button active / clickable during generation.
- **Forms:** Labels above inputs. Clear placeholder text. Textarea for longer answers. Visible focus states.
- **Download button:** Prominent, positioned near the generated output. Uses the browser's native file download (no server round-trip needed for the .txt save).

---

## 4. Constraints & Policies

- **Security:** API key must never be exposed to the client. All Anthropic calls go through the Express backend.
- **Scope (MVP):** No user accounts, no database, no payment, no persistent storage. Resist the temptation to add these before the core flow works end-to-end.
- **Reference examples:** The `cpd examples/` folder contains PDF files. Before building, these must be converted to plain text and placed in `server/examples/` for the AI prompt. Do not modify the original PDFs.
- **AI output:** The generated CPD entry is a best-effort output. The user is expected to review and edit it. Do not present it as automatically compliant.
- **Replit constraints:** Everything runs in a single Replit workspace. Keep dependencies minimal. Avoid anything that requires a long build step or native binaries.

---

## 5. Repo / Git Etiquette

- **Workflow:** Commit directly to `main`. This is a solo prototype — no branches or PRs needed at this stage.
- **Commit messages:** Short, descriptive, present tense. Example: `Add learning type selector to form`. Use conventional-style prefixes where natural: `feat:`, `fix:`, `chore:`.
- **What to commit:** Working code only. Do not commit `.env` files, node_modules, or API keys under any circumstances.
- **`.gitignore`:** Must include `node_modules/`, `.env`, and any build output folders before the first commit.

---

## 6. Frequently Used Commands

```bash
# Install dependencies
npm install

# Start the dev server (runs both React dev server and Express)
npm run dev

# Run unit tests
npm test

# Lint and auto-fix
npx eslint . --fix
npx prettier --write .

# Build for production (if needed for Replit deploy)
npm run build

# Install Playwright browsers (first time only)
npx playwright install

# Run E2E tests (headless)
npx playwright test

# Run E2E tests in interactive UI mode
npx playwright test --ui
```

> These commands assume the standard Replit Node.js project structure. Adjust if the scaffolding differs.

---

## 7. Testing Instructions

Testing has three layers: unit, E2E, and regression. Full detail is in [docs/project_spec.md — Section 5](docs/project_spec.md).

---

### 7.1 Unit Tests — Jest

Tests individual functions. No browser or server needed.

**What to test:**
1. **Prompt assembly** — learning type + answers → correct prompt string with reference examples injected.
2. **Form validation** — required fields enforced; API not called with empty data.
3. **Download helper** — correct .txt blob and filename generated.
4. **API route handler** — Express route returns correct JSON from a mocked Anthropic client.

**Run:**
```bash
npm test
```

---

### 7.2 E2E Tests — Playwright + Playwright MCP

Tests the full app in a real browser. Test files live in `e2e/` (or `tests/` — match whatever Playwright scaffolding uses).

**What to test:**
- Planned learning happy path (fill form → generate → edit → download)
- Unplanned learning happy path (same flow, Q2 differs)
- Learning type switcher correctly updates Q2
- Loading state appears on submit, Submit button disabled during load
- Empty form validation blocks submission
- Network intercept confirms API key is not leaked to the browser

**Run:**
```bash
npx playwright test          # headless
npx playwright test --ui     # interactive UI mode
```

**Playwright MCP during development:** Use Playwright MCP to let Claude navigate the running app, click elements, read content, and take screenshots — useful for quick verification and debugging without writing a full test script each time.

---

### 7.3 Regression Suite

Both the Jest suite and the Playwright suite together form the regression suite. Run both before every commit — especially after changes to form logic, prompt assembly, the API route, or any UI state transition. Block the commit if either suite fails.

---

## Self-Update Reminder

After any of the following events, update this CLAUDE.md to reflect the current state of the project:

- A new feature is built or a milestone is reached
- The tech stack or architecture changes
- New commands, scripts, or tools are added
- Testing scope expands
- The project moves from prototype to a more production-ready state

Do not let this file go stale. It is how future work (and future Claude sessions) stays aligned with the project.
