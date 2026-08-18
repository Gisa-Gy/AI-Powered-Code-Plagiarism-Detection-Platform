# CodeGuard AI

**AI-Powered Code Plagiarism Detection Platform**

CodeGuard AI is a single-file web application that demonstrates an AST-based structural similarity detector with a separate AI-assisted scoring layer for detecting plagiarism in programming assignments. It is a final-year Computer Science research prototype built for an academic (University of Kigali / Rwanda) context.

> **Prototype notice.** This is a browser-only demonstration. All data, scores, and metrics are labelled *Demo / Illustrative* — no real research findings are fabricated. The AI layer is a *supporting* signal only: it never decides academic misconduct. A human lecturer always makes the final decision (human-in-the-loop).

---

## Features

- **Role-based access control** — three roles (System Administrator, Lecturer, Student) with enforced permissions
- **12-stage animated analysis pipeline** — Submission → Language ID → Preprocess → Normalize → AST Generation → AST Normalization → Feature Extraction → Structural Similarity → AI Scoring → Classification → Evidence → Human Review
- **AST-based structural analysis** kept architecturally separate from the AI-assisted score
- Interactive **SVG AST viewer** (zoom, collapse, compare-highlight)
- **Split-screen code comparison** with line-match highlighting
- Plagiarism **case management** and review workflow
- Printable / exportable **reports** (JSON + CSV)
- Admin tools: user management, roles & permissions, departments, courses, database + ERD, security center, audit logs, system monitoring
- Configurable scoring weights (AST 60% / Token 20% / AI 20%)
- Evaluation dashboard with a confusion matrix (labelled *Demo*)
- Global search (Ctrl+K), notifications, dark mode, native SVG charts
- Guided **presentation / demo mode**

---

## Running it

### Option A — Open directly

Download or clone the repo and open `index.html` in any modern browser (Chrome, Edge, or Firefox). No server, build step, or installation is required.

### Option B — Deploy to GitHub Pages

1. Push `index.html` to a GitHub repository.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*.
4. Select branch **`main`** and folder **`/ (root)`**, then **Save**.
5. Wait for the deployment and open the published URL.

Application state is stored in the browser's `localStorage` (key `codeguard_ai_v1`) and can be reset from the Database page.

---

## Demo credentials

Sign-in autofills these accounts.

| Role                 | Email                       | Password       |
| -------------------- | --------------------------- | -------------- |
| System Administrator | `admin@codeguard.demo`      | `Admin@123`    |
| Lecturer             | `lecturer@codeguard.demo`   | `Lecturer@123` |
| Student              | `student@codeguard.demo`    | `Student@123`  |

Access control is enforced: students cannot reach admin, audit, security, or database pages, nor other students' code and cases.

---

## Production architecture notes

The single-file app is a client-side prototype. A production deployment would use:

- **Backend:** Python (FastAPI / Flask). Real AST parsing via the `ast` module (Python), `javalang` or Tree-sitter (Java / JavaScript). Structural signatures are computed server-side.
- **AI layer:** a fine-tuned code-embedding model (e.g. CodeBERT / GraphCodeBERT) producing a supporting similarity signal only, kept separate from the deterministic structural score. The lecturer makes the final call.
- **Data:** PostgreSQL for users, courses, submissions, and cases; object storage for code artifacts.
- **Security:** server-side RBAC, JWT sessions, and MFA, replacing the demo's client-side auth.
- **Scoring weights** become server configuration; every displayed metric stays labelled *Demo / Illustrative* until validated on a real dataset.

---

## Tech stack

Pure HTML, CSS, and vanilla JavaScript in a single file. Inline SVG for icons, charts, the AST viewer, and the ERD. No external dependencies or frameworks.

---

## Academic integrity

CodeGuard AI is a decision-support tool, not a decision-maker. Similarity scores indicate where a human should look; they are not proof of misconduct. Final judgment on any academic integrity case rests with the responsible lecturer or committee.

---

## License

Released under the MIT License. See [`LICENSE`](LICENSE) for details.
