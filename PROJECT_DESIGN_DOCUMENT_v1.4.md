# Project Design Document
## Agent-Readable Skills Infrastructure — Interactive Learning Curriculum

**Version:** 1.4  
**Status:** Production deployment complete. Current work: Phase 6 planning (in-section activities integration).  
**Last updated:** 2026-06-14

---

## Purpose of This Document

This document is the authoritative briefing for all future conversations in this project. Every new conversation should read this document before beginning work. It captures decisions already made, patterns established, the full implementation status, and the roadmap for Phase 6 and beyond.

---

## What's New in v1.4

### Deployment Status — Successfully Completed ✅

1. **GitHub Pages deployment live** — The app is now deployed at `https://zephyrpdx.github.io/Agent-Readable-Skills-2/`
   - Built via `deploy.yml` workflow on each push to `main`
   - All 9 modules, dashboard, flashcard system, and engagement tracker are accessible
   - Users provide their own Anthropic API key via modal on first launch

2. **GitHub repository synchronized** — All recent work is now pushed to `main`:
   - Resolved divergent branch state (`Maybe-works-now` merged into `main`)
   - `.gitignore` conflict resolved (both Claude session config entries consolidated)
   - Project design documentation (v1.3) committed and pushed

3. **README created** — Comprehensive project documentation at repository root
   - Quick-start guide for local development
   - Architecture overview with all component responsibilities
   - Learning science foundation explanation
   - Deployment instructions (local and GitHub Pages)
   - Security & privacy notes
   - Tech stack details

4. **Ready for Phase 6 planning** — All Phase 1–5 work is complete and deployed
   - in-section-activities.json specifications are defined but not yet integrated
   - Next work: integrate micro-activities into module components
   - Plan: define acceptance criteria, component modifications, testing approach

---

## Project Overview

This project builds a complete, interactive, AI-assessed learning curriculum for non-developer adult learners. The subject is **Agent-Readable Skills Infrastructure** — the practice of writing `.md` skill files that replace brittle ad-hoc LLM prompts with deterministic, version-controlled behavioral contracts for enterprise AI systems.

The curriculum has **three levels and nine modules**:

### Level 1 — Foundations (Modules 1–3)
Covers the problem with traditional prompts, the anatomy of a skill primitive, and how to write your first skill.

### Level 2 — Intermediate (Modules 4–6)
Covers agentic contracts, assessment recipes, and error handling strategies.

### Level 3 — Advanced (Modules 7–9)
Covers multi-step workflows, testing & improvement cycles, and building skill ecosystems at scale.

**All instructional content has been authored** and exists in `Agent_Skills_Curriculum.docx`. The engagement tracker, flashcard system, all nine lesson modules, progress dashboard, and interactive components are fully implemented and live in production.

The learning system is grounded in evidence-based principles: chunking, spaced repetition, retrieval practice, interleaving, deliberate practice, illusion-of-competence detection, and habit formation.

---

## Project Files

### Core Application

| File | Purpose | Status |
|---|---|---|
| `App.jsx` | Root application shell and main router | ✅ Complete |
| `ApiKeyModal.jsx` | Component for collecting and validating Anthropic API key | ✅ Complete |
| `Dashboard.jsx` | Home screen showing modules, flashcard queue, next actions | ✅ Complete |
| `main.jsx` | Bootstrap, `window.storage` polyfill, API fetch interceptor | ✅ Complete |

### Interactive Lessons (Full-Page Artifacts)

| File | Module | Title | Status |
|---|---|---|---|
| `module1-lesson.jsx` | Module 1 | Why Skills Matter: The Problem With Prompts | ✅ Complete (canonical template) |
| `module2-lesson.jsx` | Module 2 | Anatomy of a Skill Primitive | ✅ Complete |
| `module3-lesson.jsx` | Module 3 | Writing Your First Skill | ✅ Complete |
| `module4-lesson.jsx` | Module 4 | Agentic Contracts | ✅ Complete |
| `module5-lesson.jsx` | Module 5 | Assessment Recipes | ✅ Complete |
| `module6-lesson.jsx` | Module 6 | Error Handling & Graceful Degradation | ✅ Complete |
| `module7-lesson.jsx` | Module 7 | Multi-Step Workflows & Composition | ✅ Complete |
| `module8-lesson.jsx` | Module 8 | Testing & Continuous Improvement | ✅ Complete |
| `module9-lesson.jsx` | Module 9 | Building Skill Ecosystems at Scale | ✅ Complete |

### Engagement & Learning Systems

| File | Purpose | Status |
|---|---|---|
| `engagement-tracker.jsx` | Session history, scores, timestamps, learning analytics | ✅ Complete |
| `flashcard-system.jsx` | Adaptive flashcard review using Leitner box SRS | ✅ Complete |

### Data & Configuration

| File | Purpose | Status |
|---|---|---|
| `flashcard-content.json` | Structured flashcard inventory for all 9 modules | ✅ Complete |
| `in-section-activities.json` | Specification for micro-activities (Classify, Match, Sequence, etc.) | ✅ Defined, not yet integrated |
| `agent-skills-curriculum.md` | Searchable standalone curriculum reference | ✅ Complete |
| `package.json` | npm dependencies and build scripts | ✅ Current |
| `vite.config.js` | Vite build configuration | ✅ Current |
| `index.html` | HTML entry point for the application | ✅ Complete |

### Documentation

| File | Purpose | Status |
|---|---|---|
| `README.md` | Quick-start guide, architecture overview, deployment instructions | ✅ Complete (NEW in v1.4) |
| `PROJECT_DESIGN_DOCUMENT_v1.4.md` | This comprehensive project specification | ✅ Current |
| `PROJECT_DESIGN_DOCUMENT_v1.3.md` | Previous version (archived for reference) | 📦 Archive |
| `PROJECT_DESIGN_DOCUMENT.md` | Original design document (archived) | 📦 Archive |

### Deployment & CI/CD

| File | Purpose | Status |
|---|---|---|
| `deploy.yml` | GitHub Actions workflow for GitHub Pages auto-deployment | ✅ Active |
| `.github/workflows/npm-publish-github-packages.yml` | Automated npm registry publishing | ✅ Active |
| `.gitignore` | Version control ignore rules | ✅ Updated |

### Reference & Learning Science Materials

| File | Purpose | Status |
|---|---|---|
| `Agent_Skills_Curriculum.docx` | Full authored curriculum (source of truth for all content) | 📚 Reference |
| `Agent_Readable_Skills_Curriculum.pdf` | Original source curriculum document | 📚 Reference |
| `In-Section_Activity_Content_Specification.docx` | Activity design patterns and specifications | 📚 Reference |
| `Learning_How_to_Learn_*.docx` | Learning science references and transcripts | 📚 Reference |
| `What_is_a_Chunk_Transcript.docx` | Deep dive into chunking mechanics | 📚 Reference |

---

## Architecture & Technical Design

### Application Structure

```
App.jsx (root)
├── Dashboard (view: 'dashboard')
├── Module1–9 (views: 'm1'–'m9')
├── EngagementTracker (view: 'tracker')
├── FlashcardSystem (view: 'flashcards')
└── ApiKeyModal (overlay)
```

**Navigation Pattern:**
- App maintains a `view` state that switches between dashboard, modules, flashcards, and tracker
- Full-page module views render a "← Dashboard" back button overlay (z-index: 9999)
- ApiKeyModal appears on first launch if no API key is found in localStorage

### Direct Browser API Access

**Problem Solved:** The curriculum was originally designed as Claude artifacts. Moving to standalone web app required handling API authentication without backend server.

**Solution Implemented in `main.jsx`:**

1. **`window.storage` polyfill** — Provides localStorage-backed implementation of Anthropic's artifact storage API
   - Allows module code to use `artifact.storage` patterns without modification
   - Keys prefixed with `artifact:` to avoid collisions

2. **API fetch interceptor** — Automatically injects Anthropic API key and required headers
   - Intercepts all `fetch()` calls to `api.anthropic.com`
   - Adds `Authorization: Bearer sk-ant-...` header
   - Adds required `anthropic-version` header
   - Does NOT intercept other requests (safe for external APIs)

3. **ApiKeyModal component** — User-provided credentials management
   - Appears on first launch if no key in localStorage
   - Validates key format (must start with `sk-ant-`)
   - Stores key in browser localStorage only
   - Provides settings button on dashboard to update key at any time

**Data Flow:**
```
User enters API key
  ↓
ApiKeyModal validates (must start with sk-ant-)
  ↓
localStorage.setItem('anthropic-api-key', key)
  ↓
main.jsx reads key on app bootstrap
  ↓
fetch interceptor injects key into all api.anthropic.com requests
  ↓
Module assessment calls reach Claude Opus with user's key
  ↓
Results returned and displayed in module
```

### Model Selection

**Current Model: `claude-opus-4-8`**

- Used for all assessment evaluation calls in modules
- Chosen for superior response quality on scenario-based evaluation tasks
- Better at detecting misconceptions and providing targeted feedback
- Defined as constant `ASSESS_MODEL = 'claude-opus-4-8'` in each module

**Previous Model: `claude-sonnet-4-20250514`**
- Used in earlier versions
- Deprecated in v1.3, fully replaced in v1.4

### Component Patterns

**Module Template (canonical from Module 1):**
- Full-page artifact structure
- Imports `ASSESS_MODEL` and assessment logic
- Uses localStorage for session state
- Includes styled section content and embedded assessments
- Assessment flow: user submits → fetch to Claude Opus → feedback displayed → engagement logged

**Styling Convention:**
- Color palette defined in `App.jsx` as `G` object (navy, slate, amber, cream, text colors)
- Font imports via Google Fonts in App.jsx
- CSS-in-JS via React inline styles
- Consistent design system across all modules and dashboard

**Engagement Tracking:**
- All user interactions logged to localStorage via `engagement-tracker.jsx`
- Data captured: session start/end, module visited, assessment taken, score, timestamp
- Accessible via Dashboard's "View Engagement History" or dedicated Tracker view

### Flashcard System (Leitner Box SRS)

- Card data from `flashcard-content.json` (structured by module)
- Each card tracks: front, back, box (1-5), due date, success rate
- User rates confidence (1-5) after attempting recall
- Box advancement: confidence 1-2 → stay in box, 3-4 → advance one box, 5 → advance two boxes
- Next review date calculated based on box (higher boxes = longer intervals)
- Cards only appear when due for review

---

## Deployment & CI/CD

### Local Development

```bash
npm install
npm run dev
# Opens at http://localhost:5173
```

### Production Build

```bash
npm run build
# Creates optimized bundle in dist/
npm run preview
# Test production build locally at http://localhost:4173
```

### GitHub Pages Deployment

**Workflow:** `deploy.yml`
- Triggered on every push to `main` branch
- Builds application with `npm run build`
- Deploys `dist/` to GitHub Pages
- **Live URL:** https://zephyrpdx.github.io/Agent-Readable-Skills-2/

**Workflow Status:**
- ✅ Tested and working
- ✅ Builds consistently
- ✅ Deploys automatically on push

### npm Registry Publishing

**Workflow:** `.github/workflows/npm-publish-github-packages.yml`
- Triggered on GitHub release creation
- Publishes package to npm registry
- Currently set as private package (can be made public in settings)

---

## Phase Breakdown & Status

### Phase 1 ✅ Complete
**Engagement Tracking System**
- User session logging
- Score and timestamp recording
- Session history visualization in Tracker view

### Phase 2 ✅ Complete
**Flashcard & Spaced Repetition System**
- Leitner box algorithm
- Confidence-based card advancement
- Adaptive review scheduling
- Data persistence in localStorage

### Phase 3 ✅ Complete
**Interactive Lesson Modules (Core Content)**
- All 9 lesson modules implemented as full-page artifacts
- Module 1 created as canonical template
- Modules 2–9 follow same pattern
- Inline assessments with Claude Opus evaluation
- Personalized feedback for each learner

### Phase 4 ✅ Complete
**Dashboard & Navigation**
- Home screen showing all modules
- Module status tracking
- Flashcard queue (today's due cards)
- Recommended next actions
- Navigation to modules, tracker, and flashcards
- Settings button for API key management

### Phase 5 ✅ Complete
**Production Deployment & Direct Browser API Access**
- Standalone web app (not just Claude artifact)
- `window.storage` polyfill for artifact storage API compatibility
- API fetch interceptor for automatic auth header injection
- ApiKeyModal for user-provided Anthropic API key
- GitHub Pages auto-deployment via `deploy.yml`
- GitHub Actions npm publishing workflow
- Comprehensive documentation (README + PROJECT_DESIGN_DOCUMENT)

### Phase 6 🚀 In Planning
**In-Section Activities Integration**
- Micro-activities defined in `in-section-activities.json` but not yet rendered in modules
- Activity types: Classify, Match, Sequence, Spot-the-Flaw, Cover-and-Reconstruct
- Each activity <60 seconds, tests single core concept
- Planned work:
  - Create reusable `ActivityComponent.jsx` for each activity type
  - Integrate activity components into appropriate sections of modules
  - Hook activities to engagement tracker
  - Update assessment logic to weight activities

---

## Technical Stack & Dependencies

### Runtime
- **React** 18.3.1 — UI framework
- **react-dom** 18.3.1 — React DOM rendering

### Build & Development
- **Vite** 5.4.0 — Build tool and dev server
- **@vitejs/plugin-react** 4.3.1 — React plugin for Vite

### External Services
- **Anthropic API** — Claude Opus model for assessments
- **GitHub Pages** — Application hosting
- **GitHub Actions** — CI/CD pipeline

### Browser APIs Used
- `localStorage` — User API key and session data persistence
- `fetch()` — HTTP requests to Anthropic API
- `window.storage` — Polyfill for artifact storage API (custom implementation)

---

## Key Decisions & Rationale

### 1. Standalone Web App Instead of Claude Artifacts

**Decision:** Move from Claude artifact-only deployment to standalone React app on GitHub Pages.

**Rationale:**
- Allows repeated access without Claude interface
- Enables long-form engagement and habit formation
- Supports progress persistence across sessions
- Removes dependency on Claude artifact API availability

**Implementation:**
- Added `main.jsx` with polyfills for artifact storage API
- API fetch interceptor handles authentication
- ApiKeyModal lets users provide their own API keys

### 2. Claude Opus Model for Assessments

**Decision:** Use `claude-opus-4-8` for all assessment evaluations.

**Rationale:**
- Superior response quality for nuanced scenario evaluation
- Better at detecting misconceptions and providing targeted feedback
- Justifies higher cost through improved learning outcomes
- Critical for reliability in assessment pipeline

### 3. Leitner Box Spaced Repetition

**Decision:** Implement Leitner box algorithm rather than SM-2 or other SRS algorithms.

**Rationale:**
- Simpler to understand and debug
- Proven effective for adult learning
- Learner confidence (1-5) directly maps to box advancement
- Easier to integrate with engagement tracking

### 4. localStorage for Data Persistence

**Decision:** Use browser localStorage instead of backend database.

**Rationale:**
- No backend server required
- Privacy-preserving (data stays on user's device)
- Sufficient for single-device engagement tracking
- Reduces infrastructure complexity for initial deployment

### 5. In-Section Activities Over Post-Section Only

**Decision:** Define micro-activities (`in-section-activities.json`) to appear within content sections, not just at section end.

**Rationale:**
- Retrieval practice increases retention
- Breaks up content with cognitive breaks
- Tests understanding before moving to next concept
- Activities <60 sec prevent cognitive overload

---

## Known Limitations & Future Enhancements

### Current Limitations
1. **No cross-device sync** — Data only persists on the device where learning occurs
   - Workaround for Phase 7: Add cloud backup option
2. **No collaborative features** — Cohort-based learning not yet supported
   - Planned for Phase 7: Add instructor dashboard
3. **In-section activities defined but not rendered** — `in-section-activities.json` exists but integration pending
   - Phase 6 work (in planning)
4. **No export/reporting** — Learner progress not downloadable
   - Planned for Phase 8: Add analytics export

### Future Enhancements (Phase 7+)

**Phase 7 — Cloud Sync & Collaboration**
- Optional cloud backend for cross-device sync
- Basic instructor dashboard (view learner progress)
- Cohort grouping and discussion features

**Phase 8 — Analytics & Reporting**
- Engagement metrics dashboard
- Progress reports (downloadable)
- Curriculum effectiveness analysis
- Per-module success rates

**Phase 9 — Adaptive Learning**
- ML-based module recommendation
- Difficulty scaling based on assessment performance
- Prerequisite enforcement

**Phase 10 — Extensibility**
- Skill template for adding new modules
- Third-party activity plugin system
- Custom assessment recipe library

---

## Security & Privacy

### Data Handling
- **API Keys:** User-provided; stored in browser localStorage only; never sent to external services other than Anthropic API
- **Assessment Responses:** Sent to Claude Opus for evaluation only; not persisted on Anthropic servers
- **Engagement Data:** Stored locally in browser; never uploaded to any server
- **User Identity:** No authentication, login, or user tracking

### HTTPS & Transport Security
- GitHub Pages enforces HTTPS
- All API calls to Anthropic use HTTPS
- No unencrypted data transmission

### No Third-Party Tracking
- No Google Analytics, Mixpanel, or similar
- No cookies for tracking purposes
- No telemetry beyond what localStorage provides

---

## Version History

| Version | Date | Key Changes |
|---|---|---|
| 1.0 | 2026-05-XX | Initial design, Phases 1–3 complete |
| 1.1 | 2026-05-XX | Dashboard added (Phase 4) |
| 1.2 | 2026-06-XX | Production deployment planning, documentation updates |
| 1.3 | 2026-06-14 | Model upgrade to claude-opus-4-8, API key modal, GitHub Actions workflows, README draft |
| 1.4 | 2026-06-14 | Production deployment successful, GitHub Pages live, comprehensive README, Phase 6 planning ready |

---

## How to Read This Document in Future Conversations

1. **New conversation?** Start here. This document captures all project decisions, architecture, and status.
2. **Making changes to a module?** Reference the canonical template in Module 1 (`module1-lesson.jsx`).
3. **Adding new data?** Consult the data structure sections for `flashcard-content.json` and `in-section-activities.json`.
4. **Troubleshooting?** Check the Known Limitations and Architecture sections.
5. **Deploying changes?** Follow the Deployment & CI/CD section — workflows are automated.

---

## Contact & Support

- **Repository:** https://github.com/Zephyrpdx/Agent-Readable-Skills-2
- **Live App:** https://zephyrpdx.github.io/Agent-Readable-Skills-2/
- **Author:** Zachary Poole ([@Zephyrpdx](https://twitter.com/Zephyrpdx) on Twitter)

---

**End of Project Design Document v1.4**
