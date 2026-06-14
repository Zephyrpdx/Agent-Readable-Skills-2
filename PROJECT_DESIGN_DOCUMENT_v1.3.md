# Project Design Document
## Agent-Readable Skills Infrastructure — Interactive Learning Curriculum

**Version:** 1.3  
**Status:** Active development — Phases 1 through 5 complete. Current work: production deployment, direct browser API access, and in-section activities.  
**Last updated:** 2026-06-14

---

## Purpose of This Document

This document is the authoritative briefing file for all future conversations in this project. Every new conversation should read this document before beginning work. It captures decisions already made, patterns already established, and the full implementation plan so that no decision needs to be re-litigated and no context needs to be reconstructed from scratch.

---

## What's New in v1.3

### Major Updates Since v1.2

1. **Model switched to claude-opus-4-8** — All API assessment calls now use `claude-opus-4-8` instead of `claude-sonnet-4-20250514`. This improves response quality and reliability for complex assessments. Reference: `ASSESS_MODEL` constant in all module files.

2. **Direct browser API access** — The application now runs as a web app with `main.jsx` providing two critical utilities:
   - **window.storage polyfill** — Artifact storage API backed by localStorage
   - **API fetch interceptor** — Automatically injects Anthropic API key and required headers to all `api.anthropic.com` requests
   - Users must provide their own Anthropic API key via the ApiKeyModal component

3. **API key modal** — New `ApiKeyModal.jsx` component manages Anthropic API key collection and storage in localStorage. Validates key format (must start with `sk-ant-`). Displays on first app launch if no key is found.

4. **GitHub Actions workflows** — Added automated deployment:
   - `.github/workflows/npm-publish-github-packages.yml` — publishes to npm on release
   - `deploy.yml` — Auto-deploys to GitHub Pages on push to main branch

5. **In-section activities** — `in-section-activities.json` now defines interactive micro-activities (Classify, Match, Sequence, Spot-the-Flaw, Cover-and-Reconstruct) to appear within content sections, not just at section end. Each activity is <60 seconds and tests only the core concept of its section. **NOTE: This file exists but activities are not yet integrated into module components — this is a planned enhancement for Phase 6.**

6. **Searchable curriculum reference** — `agent-skills-curriculum.md` provides a standalone, readable curriculum overview independent of the interactive artifacts. Can be published separately or used as supplementary reference material.

7. **Bug fixes** — Recent merge fixed lesson module crashes, API error handling, and thin feedback issues from the `fix/lesson-modules-api-and-feedback` branch.

---

## Project Overview

This project builds a complete, interactive, AI-assessed learning curriculum for a non-developer adult learner. The subject is **Agent-Readable Skills Infrastructure** — the practice of writing `skill.markdown` files that replace brittle ad-hoc LLM prompts with deterministic, version-controlled behavioral contracts for enterprise AI systems.

The curriculum has three levels and nine modules. All instructional content has been authored and exists in the project file `Agent_Skills_Curriculum.docx`. The engagement tracker, flashcard system, all nine lesson modules, and the progress dashboard are implemented in the repository.

The learning system is grounded in evidence-based principles drawn from the project's reference files: chunking, spaced repetition, retrieval practice, interleaving, deliberate practice, illusion-of-competence detection, focused vs. diffuse modes, and habit formation.

---

## Project Files

| File | Purpose |
|---|---|
| `App.jsx` | Root application shell and main router for dashboard, lesson pages, and flashcards; handles API key modal display |
| `ApiKeyModal.jsx` | Component for collecting and validating Anthropic API key; stores key in localStorage |
| `Dashboard.jsx` | Phase 5 artifact — home screen showing modules, flashcard queue, and recommended next actions |
| `module1-lesson.jsx` | Interactive lesson — Module 1 (complete, enhanced, canonical template) |
| `module2-lesson.jsx` | Interactive lesson — Module 2 (complete) |
| `module3-lesson.jsx` | Interactive lesson — Module 3 (complete) |
| `module4-lesson.jsx` | Interactive lesson — Module 4 (complete) |
| `module5-lesson.jsx` | Interactive lesson — Module 5 (complete) |
| `module6-lesson.jsx` | Interactive lesson — Module 6 (complete) |
| `module7-lesson.jsx` | Interactive lesson — Module 7 (complete) |
| `module8-lesson.jsx` | Interactive lesson — Module 8 (complete) |
| `module9-lesson.jsx` | Interactive lesson — Module 9 (complete) |
| `engagement-tracker.jsx` | Phase 1 artifact — engagement tracking, scores, timestamps, session logs |
| `flashcard-system.jsx` | Phase 2 artifact — adaptive flashcard review with Leitner box SRS |
| `main.jsx` | Bootstrap, `window.storage` polyfill, and Anthropic API fetch interceptor for direct browser access |
| `flashcard-content.json` | Structured flashcard inventory for all modules |
| `in-section-activities.json` | Specification for in-section micro-activities — currently defined but not integrated into modules (Phase 6) |
| `agent-skills-curriculum.md` | Searchable curriculum reference — standalone overview of all 9 modules and learning structure |
| `deploy.yml` | GitHub Actions workflow for deploying built app to GitHub Pages on push to main |
| `.github/workflows/npm-publish-github-packages.yml` | Automated npm package publishing workflow |
| `Agent_Skills_Curriculum.docx` | Full authored curriculum content for all 9 modules — source of truth for lesson content |
| `Agent_Readable_Skills_Curriculum.pdf` | Original source curriculum document |
| `In-Section_Activity_Content_Specification.docx` | Activity content specification — used across all nine modules |
| `Learning_How_to_Learn_-_Module_1_Flashcards.docx` | Learning science reference — flashcard principles |
| `Learning_How_to_Learn_-_Module_2_Transcripts.docx` | Learning science reference — neuromodulators, chunking, interleaving |
| `Learning_How_to_Learn_-_Module_3_1.docx` | Learning science reference — procrastination and habit formation |
| `Learning_How_to_Learn_-_Module_3_2.docx` | Learning science reference — memory techniques |
| `Learning_How_to_Learn_-_Module_3_2_Answer_Key.docx` | Learning science reference — memory answer key |
| `What_is_a_Chunk_Transcript.docx` | Learning science reference — chunking transcript |
| `PROJECT_DESIGN_DOCUMENT_v1.3.md` | This file |

---

## Curriculum Map

### Level 1 — Foundations
| Module | Title | Status |
|---|---|---|
| 1 | Why Skills Matter: The Problem With Prompts | ✅ Built (enhanced — canonical template) |
| 2 | Anatomy of a Skill Primitive | ✅ Built |
| 3 | Writing Your First Skill | ✅ Built |

### Level 2 — Intermediate
| Module | Title | Status |
|---|---|---|
| 4 | Agentic Contracts | ✅ Built |
| 5 | Composability & Pipelines | ✅ Built |
| 6 | Debugging Failure Modes | ✅ Built |

### Level 3 — Advanced
| Module | Title | Status |
|---|---|---|
| 7 | Governance Tiers | ✅ Built |
| 8 | Quantitative Testing | ✅ Built |
| 9 | Enterprise Deployment | ✅ Built |

---

## Design System

All artifacts in this project use a consistent design system. Do not deviate from these values without explicit instruction.

### Color Palette

```javascript
const G = {
  navy:   "#0F1B2D",   // primary background
  navyM:  "#162236",   // header, sidebar background
  navyL:  "#1D2E45",   // elevated surfaces, callout backgrounds
  slate:  "#2A3F5C",   // inactive UI elements
  muted:  "#4A6080",   // secondary labels
  border: "#2E4060",   // all borders
  amber:  "#E8A835",   // primary accent, active states, headings
  amberL: "#F5C055",   // amber highlight, gradient end
  cream:  "#F5F0E8",   // primary heading text
  creamD: "#E8E0D0",   // secondary heading text
  text:   "#D8CFC0",   // body text
  textD:  "#A09888",   // muted body text, labels
  red:    "#C44040",   // warning states, incorrect answers
  green:  "#3A9E6E",   // success states, correct answers
  white:  "#FFFFFF",   // high-contrast text on dark surfaces
  code:   "#0D2030",   // code block backgrounds
};
```

### Typography

```
Display / Section titles:  Crimson Pro (serif) — weights 300, 400, 600 including italic
UI / Body / Buttons:       DM Sans (sans-serif) — weights 300, 400, 500, 600
Code blocks / Monospace:   JetBrains Mono — weights 400, 500
```

Google Fonts import string (always include at top of CSS):
```
@import url('https://fonts.googleapis.com/css2?family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');
```

### Layout

- Shell: CSS Grid, `grid-template-columns` driven by `sidebarOpen` state
- Sidebar expanded: 260px | Sidebar collapsed: 44px
- Header: 56px fixed height, `grid-column: 1 / -1`
- Main content: max-width 820px, padding `48px 56px 80px`
- **Critical:** `.lesson-main` MUST have `background: ${G.navy}` explicitly set — Claude artifact iframes default to white, which breaks all text contrast

### Component Inventory

Every lesson module uses these components. Build them identically in each module file — do not import across files, as each artifact is self-contained.

| Component | Class/Pattern | Notes |
|---|---|---|
| Section eyebrow | `.sec-eyebrow` | Amber, uppercase, 11px, letter-spaced |
| Section title | `.sec-title` | Crimson Pro, 34px, cream |
| Section subtitle | `.sec-sub` | Crimson Pro, 22px, text |
| Body prose | `.prose` | DM Sans, with `strong` → cream, `em` → amberL |
| Bullet list | `ul.content-list` | Custom amber chevron, no standard list markers |
| Insight callout | `.callout.callout-insight` | navyL background, amber left border |
| Warning callout | `.callout.callout-warning` | `#2A1515` background, red left border |
| Tip callout | `.callout.callout-tip` | `#0F2A1D` background, green left border |
| Compare grid | `.compare-grid` | 2-column, red-tinted left / green-tinted right |
| Code block | `.code-block pre` | JetBrains Mono, `#8EC8F0` text on `#0D2030` |
| Recall box | `.recall-box` | navyL, amber border, Claude-assessed free text |
| Quiz option | `.quiz-option` | Multi-state: default / selected / correct / wrong / locked |
| Feedback box | `.feedback-box` | Three variants: correct (green), partial (gold), incorrect (red) |
| Primary button | `.btn.btn-primary` | Amber background, navy text |
| Next button | `.btn.btn-next` | navyL background, amber text and border |
| Spinner | `.spinner` | CSS animation, amber top-border |

---

## Quiz Component Design Requirements

**These three requirements are mandatory for all quiz components in all modules. They exist because a flaw in the pre-Phase-3 `module1-lesson.jsx` allowed correct answers to be identified without answering the question. Phase 3 corrected that artifact. All subsequent builds must comply from the start.**

### 1. Randomized Answer Positions

Correct answers must never occupy a predictable position. Store each question as an object with labeled options and a `correctIndex` field pointing to the correct answer, then shuffle the options array at render time before displaying.

```javascript
const question = {
  text: "Question text here",
  options: [
    { text: "Correct answer", correct: true },
    { text: "Distractor A",   correct: false },
    { text: "Distractor B",   correct: false },
    { text: "Distractor C",   correct: false },
  ],
};

function shuffleOptions(options) {
  return [...options].sort(() => Math.random() - 0.5);
}
```

The correct answer must appear in positions A, B, C, and D with roughly equal frequency across a session. No hardcoded position is acceptable.

### 2. Uniform Pre-Selection Styling

All four answer choices must be visually identical before the student submits. No option may carry styling — color, weight, border, background, padding — that distinguishes it from the others in the unselected state. The existing design system color states apply only *after* submission:

| State | When applied | Style |
|---|---|---|
| Default (unselected) | Before submission | `navyL` background, `border` border, `text` text — identical for all options |
| Selected (pending) | After click, before submit | `slate` background, `amber` border — identical regardless of correctness |
| Correct (revealed) | After submission, correct option | `green` left border or background tint |
| Incorrect (revealed) | After submission, wrong selection | `red` left border or background tint |
| Locked | After submission, all options | Pointer events disabled |

The `correct: true` field in the data structure must never drive any CSS class or inline style before the answer is submitted.

### 3. Answer Key Separation (Static Documents)

This requirement applies when quiz content appears in any static or printable format (PDF supplements, worksheets, or reference documents):

- The answer key must appear on a separate page or clearly delineated section, not inline with the questions.
- At the question block, include a conspicuous instruction directing the student to the key, e.g.: *"Answer key for questions 1–5: see Answer Key section, p. 7."*
- This requirement does not apply to interactive `.jsx` artifacts (answers are revealed only after submission), but the randomization and styling requirements above still apply to those.

---

## Sidebar Collapse Pattern

The sidebar is collapsible. This pattern must be replicated in all lesson modules and the dashboard.

```jsx
const [sidebarOpen, setSidebarOpen] = useState(true);

<div className="lesson-shell" 
  style={{ gridTemplateColumns: sidebarOpen ? "260px 1fr" : "44px 1fr" }}>

<nav className={`lesson-sidebar ${sidebarOpen ? "" : "collapsed"}`}
  style={{ background: G.navyM, borderRight: `1px solid ${G.border}`, 
           overflowY: "auto", padding: "16px 0", transition: "width .25s ease" }}>
  <div className="sidebar-toggle-row">
    {sidebarOpen && <span className="sidebar-section-label">Contents</span>}
    <button className="sidebar-toggle" onClick={() => setSidebarOpen(o => !o)}>
      {sidebarOpen ? "←" : "→"}
    </button>
  </div>
  {SECTIONS.map((sec, idx) => (
    <div className={`sidebar-item ${idx === sectionIdx ? "active" : ""} 
                    ${completed.has(sec.id) ? "completed" : ""}`}
         onClick={() => goTo(idx)}
         title={!sidebarOpen ? sec.label : undefined}>
      <div className="si-dot" />
      {sidebarOpen && <div className="si-label">{sec.label}</div>}
    </div>
  ))}
</nav>
```

---

## API Assessment Pattern

All recall and quiz feedback uses a live Claude API call. This is the established pattern — replicate exactly.

```javascript
async function assessWithClaude(systemPrompt, userMessage) {
  const res = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      model: "claude-opus-4-8",
      max_tokens: 1000,
      system: systemPrompt,
      messages: [{ role: "user", content: userMessage }]
    })
  });
  const data = await res.json();
  const text = data.content?.filter(b => b.type === "text").map(b => b.text).join("") || "";
  try {
    const clean = text.replace(/```json|```/g, "").trim();
    return JSON.parse(clean);
  } catch {
    return { grade: "partial", label: "Feedback", message: text };
  }
}
```

**Key changes in v1.3:**
- Model is now `"claude-opus-4-8"` (was `"claude-sonnet-4-20250514"`)
- API key is injected automatically by the fetch interceptor in `main.jsx` — no need to include Authorization headers in the fetch call
- The API key is retrieved from `localStorage.getItem('anthropic-api-key')` by the interceptor
- Required headers (`x-api-key`, `anthropic-version`, `anthropic-dangerous-direct-browser-access`) are added automatically

**Recall assessment system prompt returns:**
```json
{ "grade": "correct|partial|incorrect", "label": "2-4 word verdict", "message": "instructor feedback" }
```

**Quiz explanation system prompt returns:**
```json
{ "message": "2-3 sentence explanation" }
```

---

## Module File Structure

Every lesson module (module1 through module9) follows this identical structure. The content changes; the scaffolding does not.

```
SECTIONS array: [intro, content-1, content-2, content-3, content-4, recall, quiz, complete]
```

Each module contains:
- SectionIntro          — module overview, learning objectives, time estimate
- 4× Content Sections   — reading material with callouts, lists, code blocks, compare grids
- SectionRecall         — 3 open-ended questions, Claude-assessed
- SectionQuiz           — 3–5 multiple choice questions, Claude-explained
- SectionComplete       — weighted score, recommendation, spaced repetition reminder

Score weighting:
- Recall correct  = 2 points
- Recall partial  = 1 point
- Quiz correct    = 2 points
- Score ≥ 80%     → advance recommendation
- Score 55–79%    → review gaps before advancing
- Score < 55%     → re-read module

---

## Persistent Storage Pattern

Phases 1–5 use the artifact persistent storage API. In v1.3, this is implemented via the `window.storage` polyfill in `main.jsx`, which backs to localStorage. Key rules:

- Keys: hierarchical, under 200 chars, no whitespace/slashes/quotes — e.g., `engagement:module1:recall:r1`
- Values: JSON strings under 5MB per key
- `shared: false` (default) — data is per-user, not shared
- Always wrap in try/catch; non-existent keys throw rather than returning null
- Batch related data into single keys to minimize sequential storage calls

```javascript
await window.storage.set('engagement:module1:recall:r1', 
  JSON.stringify({ grade: 'partial', timestamp: Date.now() }));

try {
  const result = await window.storage.get('engagement:module1:recall:r1');
  const data = result ? JSON.parse(result.value) : null;
} catch (e) {
  // key doesn't exist yet
}
```

---

## API Key Management

In v1.3, the application requires a user-provided Anthropic API key for all assessment features.

### User Setup
1. On first app launch, `App.jsx` checks `localStorage.getItem('anthropic-api-key')`
2. If no key is found, `ApiKeyModal` is displayed
3. User enters their key (must start with `sk-ant-`)
4. Key is validated and stored in localStorage as `'anthropic-api-key'`

### Runtime Access
- The `main.jsx` fetch interceptor reads the stored key and injects it into all `api.anthropic.com` requests
- Required headers: `x-api-key`, `anthropic-version: 2023-06-01`, `anthropic-dangerous-direct-browser-access: true`
- All module files can call fetch to `https://api.anthropic.com/v1/messages` without adding auth headers manually

### Error Handling
- If the API key is invalid or missing at runtime, the API returns a 401 error
- If the key is valid but does not have access to the model, the API returns a 404 error
- Module error handling displays user-friendly feedback directing them to check the Settings modal

---

## Phase Status Summary

### Phase 1 — Engagement Tracker ✅ Complete
**Deliverable:** `engagement-tracker.jsx` — saved to project  
**Stores:** Module completion timestamps, recall grades per question ID, quiz results per question ID, flashcard review history, session start/end times, written summary grades

### Phase 2 — Flashcard System ✅ Complete
**Deliverable:** `flashcard-system.jsx` — saved to project  
**Behavior:** Reads engagement log to determine due cards per Leitner box schedule; shows cards in randomized due-order; accepts know-it/almost/didn't-know response; writes result back to engagement tracker

### Phase 3 — Enhanced Module 1 ✅ Complete
**Deliverable:** Updated `module1-lesson.jsx` — saved to project, now the canonical template  
**Changes delivered:** Five enhancements listed in Phase 3 Enhancements section in v1.2 document

### Phase 4a — Modules 2 and 3 ✅ Complete
**Deliverables:** `module2-lesson.jsx`, `module3-lesson.jsx` — saved to project  
**Content source:** `Agent_Skills_Curriculum.docx` — Level 1 modules

### Phase 4b — Modules 4, 5, and 6 ✅ Complete
**Deliverables:** `module4-lesson.jsx`, `module5-lesson.jsx`, `module6-lesson.jsx` — saved to project  
**Content source:** `Agent_Skills_Curriculum.docx` — Level 2 modules

### Phase 4c — Modules 7, 8, and 9 ✅ Complete
**Deliverables:** `module7-lesson.jsx`, `module8-lesson.jsx`, `module9-lesson.jsx` — saved to project  
**Content source:** `Agent_Skills_Curriculum.docx` — Level 3 modules

### Phase 5 — Progress Dashboard ✅ Complete
**Deliverable:** `Dashboard.jsx` — saved to project  
**Behavior:** Module status cards with last-accessed date and best score; flashcard queue showing cards due today and overdue count; "Recommended Next Action" derived from engagement log; links to launch any module or flashcard review; Leitner box retention visualization

### Phase 5b — Direct Browser API Access & Deployment ✅ Complete (v1.3 Update)
**Deliverables:** 
- `main.jsx` with `window.storage` polyfill and API fetch interceptor
- `ApiKeyModal.jsx` for API key collection and validation
- `deploy.yml` for GitHub Pages deployment
- `.github/workflows/npm-publish-github-packages.yml` for npm publishing
- Bug fixes to lesson modules for API error handling and thin feedback

**Changes:**
- All modules now use `claude-opus-4-8` instead of `claude-sonnet-4-20250514`
- API key is user-provided and stored in localStorage
- Fetch interceptor automatically injects auth headers for all API calls
- Application can now run as a standalone web app instead of Claude artifact

---

## Decisions Made — Do Not Revisit Without Good Reason

- **No localStorage or sessionStorage directly** — use `window.storage` polyfill for abstraction. The polyfill backs to localStorage in the web app context.
- **Each artifact is self-contained** — no imports between module files. Shared components are duplicated in each module file.
- **Leitner box, not SM-2** — simpler to implement in browser artifact, no floating-point intervals, well-validated for this material type.
- **claude-opus-4-8** — model used for all API assessment calls (updated from claude-sonnet-4-20250514 in v1.3). Do not substitute without testing.
- **max_tokens: 1000** — sufficient for all assessment responses. Do not increase without reason.
- **Dark theme only** — no light/dark toggle. The dark theme is intentional and consistent.
- **Collapsible sidebar default: open** — `useState(true)` in every module and in the dashboard.
- **Score weighting: recall correct = 2pts, recall partial = 1pt, quiz correct = 2pts** — consistent across all modules.
- **Module structure: always 4 content sections** — intro + 4 content + recall + quiz + complete = 8 sidebar items.
- **User-provided API key** — Application requires each user to supply their own Anthropic API key. No shared backend or proxy. This is intentional for privacy and cost transparency.
- **Direct browser API access** — Anthropic API calls are made directly from the browser, not through a backend. The `anthropic-dangerous-direct-browser-access: true` header acknowledges this pattern.

---

## Open Items — Planned but Not Yet Built

These were identified during prior conversations and should be addressed in future work.

### Phase 6 — In-Section Activities (Planned)
**Status:** Activity specification complete (`in-section-activities.json`); integration not yet started  
**Scope:** Add interactive micro-activities (Classify, Match, Sequence, Spot-the-Flaw, Cover-and-Reconstruct) to content sections. Each activity should:
- Appear after section body, before Next button
- Be completable in <60 seconds
- Test only the core concept of that section
- Use React state only — no API calls
- Allow a Skip button
- Log results to engagement tracker with key pattern `engagement:module[N]:activity:[section-id]`

### Coaching System Updates (Planned)
Two corrections are needed to the learning coach system prompt:
   - *Engagement data access:* The coach cannot query `window.storage` directly. The coach must ask the student to report current scores, last session date, and Leitner box states from the tracker or dashboard before making spaced repetition recommendations.
   - *Scoring rubric:* Add explicit notation of the scoring convention — recall correct = 2pts, recall partial = 1pt, quiz correct = 2pts — so manual chat-based assessments are consistent with what the artifacts apply.

### Per-Module Reset (Planned)
**Status:** Not yet implemented  
**Scope:** Add per-module reset in `engagement-tracker.jsx` to clear test data from a specific module under active development without wiping legitimate learning history from completed modules. Current reset options are global (all data, all flashcards, all sessions).

---

## Learner Profile Notes

- Adult learner, non-developer background — applies to both the builder role and the student role
- Engages seriously and methodically with material
- Responsive to direct feedback without excessive softening
- Asks precise, practical questions — does not need concepts over-explained
- Do not assume familiarity with React, Node.js, or API concepts beyond what the curriculum itself covers — this applies in both builder and student contexts
- Learning sessions are now live — users have started engaging with modules and are providing real usage feedback

---

## Document Maintenance Protocol

**The document drifts because updating it is the last thing on your mind when a phase finishes.** To prevent this, add the following as a closing step to every phase conversation before ending it:

*"Update the PROJECT_DESIGN_DOCUMENT_v1.3.md to reflect what was completed in this conversation: [brief description of what was built or decided]. Mark the relevant phases and modules as complete, add any new decisions to the Decisions Made section, and update the status line at the top."*

This is a one-prompt ritual. It takes less than a minute and keeps every future conversation fully oriented.

---

*End of document. Update this file when significant decisions are made or the plan changes.*
