# Agent-Readable Skills Infrastructure — Interactive Learning Curriculum

An interactive, AI-assessed learning platform teaching professionals how to write skill primitives for enterprise AI systems.

## 🎯 What is This?

This project builds a complete **interactive curriculum** for learning how to architect and write agent-readable skills — standardized `.md` files that replace brittle LLM prompts with deterministic, version-controlled behavioral contracts.

The curriculum is designed for **non-developer adult learners** and grounded in evidence-based learning science: chunking, spaced repetition, retrieval practice, interleaving, deliberate practice, and habit formation.

## 📚 Curriculum Structure

**9 modules across 3 levels:**

### Level 1 — Foundations
- **Module 1:** Why Skills Matter: The Problem With Prompts
- **Module 2:** Anatomy of a Skill Primitive
- **Module 3:** Writing Your First Skill

### Level 2 — Intermediate
- **Module 4:** Agentic Contracts
- **Module 5:** Assessment Recipes
- **Module 6:** Error Handling & Graceful Degradation

### Level 3 — Advanced
- **Module 7:** Multi-Step Workflows & Composition
- **Module 8:** Testing & Continuous Improvement
- **Module 9:** Building Skill Ecosystems at Scale

## 🚀 Getting Started

### Prerequisites
- Node.js 16+ and npm
- Modern browser with JavaScript enabled
- Anthropic API key (get one at https://console.anthropic.com/)

### Installation & Running Locally

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Zephyrpdx/Agent-Readable-Skills-2.git
   cd Agent-Readable-Skills-2
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start the development server:**
   ```bash
   npm run dev
   ```
   The app will open at `http://localhost:5173` (or the next available port).

4. **Build for production:**
   ```bash
   npm run build
   ```
   Built files go to the `dist/` directory.

5. **Preview production build:**
   ```bash
   npm run preview
   ```

### First Launch
- On first visit, the **API Key Modal** will prompt you to enter your Anthropic API key
- Format: must start with `sk-ant-`
- Your key is stored in **browser localStorage** only — never sent to external servers
- You can update your key anytime via the settings button in the dashboard

## 🏗️ Project Architecture

### Core Components

| Component | Purpose |
|---|---|
| `App.jsx` | Root router — orchestrates dashboard, modules, flashcards, and API key modal |
| `Dashboard.jsx` | Home screen — module index, flashcard queue, progress tracking, and recommended next actions |
| `module1-9.jsx` | Interactive lessons — full-page learning artifacts with embedded assessments and feedback |
| `ApiKeyModal.jsx` | API key management — secure collection and validation of user's Anthropic API key |
| `engagement-tracker.jsx` | Engagement metrics — tracks session history, scores, timestamps, and learning patterns |
| `flashcard-system.jsx` | Spaced repetition system — adaptive flashcard review using Leitner box methodology |
| `main.jsx` | Bootstrap & browser API bridge — initializes `window.storage` polyfill and fetch interceptor |

### Data & Configuration

| File | Purpose |
|---|---|
| `flashcard-content.json` | Structured flashcard inventory for all 9 modules |
| `in-section-activities.json` | Micro-activity specifications (Classify, Match, Sequence, etc.) — <60 sec per activity |
| `agent-skills-curriculum.md` | Searchable standalone curriculum reference |
| `Agent_Skills_Curriculum.docx` | Full authored curriculum content (source of truth) |

### Deployment

- **Development:** `npm run dev` (Vite dev server)
- **Production Build:** `npm run build` (optimized bundle in `dist/`)
- **GitHub Pages:** Auto-deployed on every push to `main` via `deploy.yml` workflow
- **npm Registry:** Auto-published on release via `npm-publish-github-packages.yml` workflow

## 🤖 How It Works

### Learning Flow

1. **Dashboard** — View available modules, track progress, queue flashcards
2. **Interactive Lesson** — Read content, complete in-section activities, take assessments
3. **Assessment** — Answer scenario-based questions; Claude Opus evaluates and provides personalized feedback
4. **Flashcard Review** — Spaced repetition system (Leitner box) prompts review of key concepts
5. **Engagement Tracking** — System logs all interactions: session times, scores, attempts

### Assessment Engine

- Each module includes scenario-based comprehension checks
- Assessments call **Claude Opus 4.8** model (`claude-opus-4-8`) for high-quality response evaluation
- Feedback is personalized and targets misconceptions
- Engagement tracker records all assessment attempts and scores for analytics

### Spaced Repetition

- Flashcard system implements **Leitner box algorithm**
- Cards are scheduled based on learner confidence (1-5 scale)
- Each card tracks review history, success rate, and next review date
- System optimizes for long-term retention

## 🔧 Development

### Tech Stack
- **UI Framework:** React 18.3.1
- **Build Tool:** Vite 5.4.0
- **Styling:** CSS-in-JS (inline styles via React)
- **API:** Anthropic API (Claude Opus for assessments)

### Key Architectural Patterns

**Direct Browser API Access**
- `main.jsx` provides two utilities:
  - **`window.storage` polyfill** — localStorage-backed artifact storage API
  - **API fetch interceptor** — auto-injects API key and auth headers to all `api.anthropic.com` requests

**Component Structure**
- Lesson modules are full-page artifacts (no shared chrome)
- Dashboard provides navigation overlay
- Modal components are rendered at app root for guaranteed z-index layering

### Available Scripts
```bash
npm run dev     # Start dev server (HMR enabled)
npm run build   # Build for production
npm run preview # Test production build locally
```

## 📊 Learning Science Foundation

This curriculum is grounded in evidence-based learning principles:

- **Chunking** — Information organized into digestible pieces
- **Spaced Repetition** — Optimal review intervals via Leitner box algorithm
- **Retrieval Practice** — Active recall through flashcards and assessments
- **Interleaving** — Related concepts presented in mixed order
- **Deliberate Practice** — Targeted scenario-based assessments
- **Illusion-of-Competence Detection** — Assessments reveal gaps in understanding
- **Habit Formation** — Daily engagement streaks and recommended next actions

## 📝 Reference Materials

The repository includes comprehensive learning science references:

- `Learning_How_to_Learn_*.docx` — Foundational neuroscience and learning theory
- `What_is_a_Chunk_Transcript.docx` — Deep dive on chunking mechanics
- `In-Section_Activity_Content_Specification.docx` — Activity design patterns
- `Agent_Readable_Skills_Curriculum.pdf` — Original source curriculum

## 🚢 Deployment

### Local Deployment
```bash
npm run build
npm run preview
```

### GitHub Pages Auto-Deployment
- Push to `main` branch
- `deploy.yml` workflow automatically builds and deploys to GitHub Pages
- Live at: https://zephyrpdx.github.io/Agent-Readable-Skills-2/

### npm Registry
- Create a release on GitHub
- `npm-publish-github-packages.yml` automatically publishes to npm

## 📋 Project Status

**Current Phase:** Production deployment & Phase 6 planning

### Completed (✅)
- Phases 1–5: All core features, interactive lessons, engagement tracking, flashcard system, dashboard
- Direct browser API access via `main.jsx` polyfill
- API key modal for user-provided credentials
- GitHub Actions deployment workflows
- All 9 interactive lesson modules
- Comprehensive project documentation (v1.3)

### In Progress / Planned (Phase 6)
- Full integration of in-section micro-activities into module components
- Performance optimizations for larger cohorts
- Analytics dashboard for course administrators
- Export/reporting features for learner progress

## 🔐 Security & Privacy

- **API Keys:** User-provided keys stored in browser localStorage only
- **Data Privacy:** No learner data sent to external services (only to Anthropic API for assessment)
- **Assessment Calls:** Only Claude Opus model receives learner responses — no telemetry
- **No Tracking:** Project uses no analytics, cookies, or third-party trackers

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Rodney Tyler** — [GitHub](https://github.com/Zephyrpdx) | [Twitter](https://twitter.com/Zephyrpdx)

---

## 📖 Additional Resources

For deep understanding of this project, read:

- [PROJECT_DESIGN_DOCUMENT_v1.3.md](PROJECT_DESIGN_DOCUMENT_v1.3.md) — Comprehensive project specification and roadmap
- [agent-skills-curriculum.md](agent-skills-curriculum.md) — Searchable curriculum reference
- Original curriculum: [Agent_Skills_Curriculum.docx](Agent_Skills_Curriculum.docx)

---

**Questions?** Open an issue on GitHub or check the [project design document](PROJECT_DESIGN_DOCUMENT_v1.3.md) for detailed implementation notes.
