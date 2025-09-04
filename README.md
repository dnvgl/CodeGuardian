# CodeGuardian

_A lightweight, inner‑source project to leverage AI for code review and test generation across .NET and frontend stacks._

> **Status:** Early development — actively iterating on instruction‑driven workflows. Current focus is **Part 1 – AI‑Assisted Code Review (1.2 PR change scope review)**.

---

## Why CodeGuardian?

Modern teams want fast, consistent reviews without sacrificing quality. CodeGuardian provides **curated, versioned instruction sets** you can run with your AI assistant (e.g., GitHub Copilot Chat in VS Code) to perform repeatable code review and test‑generation tasks. The goal is to evolve from local, developer‑driven usage to CI/CD‑enforced checks in pipelines.

---

## Roadmap

**Part 1 — AI‑Assisted Code Review**  
- [ ] **1.1 Full solution scope review**  
- [x] **1.2 PR change scope review (current milestone)**  
- [ ] **1.3 Local _uncommitted_ scope review**  
- [ ] **1.4 Code review executed in pipeline (CI/CD)**  

**Part 2 — AI‑Assisted Unit Test Generation**  
- [ ] Generate or extend unit tests guided by repository standards and examples

**Part 3 — AI‑Assisted Automation (E2E) Test Generation**  
- [ ] Propose and scaffold UI/API automation suites aligned with app architecture

> This roadmap tracks functional scope only. Integration targets include VS Code (Copilot Chat), GitHub, and Azure DevOps pipelines.

---

## What’s in this repo (today)

This repository currently ships **instruction documents** you can copy/paste into your AI assistant to drive consistent reviews and generation tasks:

- **.NET**
  - `dotnet.pr.review.instructions.md` — PR change‑scope review guidelines for .NET
  - `dotnet.code.review.instructions.md` — Full solution review guidelines for .NET
  - `dotnet.unit.test.generation.instructions.md` — Unit test generation starter spec for .NET

- **Frontend**
  - `frontend.pr.review.instructions.md` — PR change‑scope review for frontend stacks
  - `frontend.code.review.instructions copy.md` — (work‑in‑progress) full‑solution review for frontend

> File names and availability may evolve as we consolidate guidance.

---

## Getting Started

### Prerequisites
- **VS Code** (latest)  
- **GitHub Copilot Chat** (or your preferred AI assistant)  
- Appropriate **toolchains** for your codebase (e.g., .NET SDK, Node.js) when you want the assistant to run/inspect code locally.

### Clone
```bash
git clone https://github.com/dnvgl/CodeGuardian.git
cd CodeGuardian
```

### Use with Copilot Chat (example)
1. Open an instruction file (e.g., `dotnet.pr.review.instructions.md`) in VS Code.  
2. Open **Copilot Chat** and run one of the prompts below (adjust paths as needed).

**PR change‑scope review (Git diff available locally):**
```text
Follow the standards in the currently open instruction file to review ONLY the changed files in this branch vs main. 
Output a single Markdown report with:
- Findings grouped by category and severity
- File:Line anchors for each finding
- Actionable fixes or code patches when possible
- A final “Summary & Next Steps” section
```
**Full solution review (entire workspace):**
```text
Using the open instruction file, scan the entire workspace (all projects) and produce a Markdown report with the same structure. 
Call out hotspots, dead code, async/DI issues, and duplicated logic. Suggest refactors and tests.
```

**Unit test generation (target project/folder):**
```text
Using the unit test generation instructions, propose/extend tests for the selected project. 
For each test, include: intent, arrangement, name, and the AAA sections. Prefer deterministic tests.
```

> Tip: Save your favorite prompts as VS Code snippets or Tasks.

---

## Output

Prefer a **single Markdown report** checked into the repo under a discoverable folder, for example:
```
/reports
  /code-review
    2025-09-04-pr-review.md
    2025-09-04-full-solution.md
  /unit-tests
    2025-09-04-generation-notes.md
```

When running in CI/CD (future 1.4), publish the same Markdown report as a build artifact and (optionally) post a summarized comment in the PR.

---

## Design Principles

- **Instruction‑first:** Clear, deterministic rules beat ad‑hoc LLM prompts.
- **Actionability over verbosity:** Every finding should be fixable; avoid noise.
- **Traceability:** Reference file & line; keep the review order aligned with the diff.
- **Separation of concerns:** Authoritative rules live in this repo; tool‑specific wrappers (VS Code tasks, ADO, GitHub Actions) are thin layers.
- **Privacy:** Use local context whenever possible; be mindful of sensitive code in cloud LLMs.

---

## Contributing

We welcome issues and PRs that improve clarity, reduce noise, or add high‑value checks.

1. Open an issue describing the change and the **problem it solves**.  
2. For instruction edits, include before/after examples and expected assistant behavior.  
3. Keep rule wording **concise and testable**.  
4. Add/adjust examples so new contributors can validate the change.

---

## Project Structure (subject to change)

```
.
├─ dotnet.code.review.instructions.md
├─ dotnet.pr.review.instructions.md
├─ dotnet.unit.test.generation.instructions.md
├─ frontend.pr.review.instructions.md
└─ frontend.code.review.instructions copy.md
```

---

## FAQ

**Is there a VS Code extension?**  
Not yet. Early milestones focus on high‑quality instructions you can run with Copilot Chat or similar tools. Extension and CI/CD wrappers will follow in Part 1.3–1.4.

**Which languages are supported?**  
The instructions target .NET and common frontend stacks first; contributions for other ecosystems are welcome.

**Can I run this in CI/CD?**  
That’s the aim of **Part 1.4**. The same instruction sets will back a pipeline task that emits a Markdown report and (optionally) fails the build on configurable thresholds.

---

## License

TBD. If you plan to reuse the instructions outside this repo’s license later, please open an issue so we can clarify terms early.

---

## Acknowledgements

Thanks to the contributors and reviewers who shaped the initial instruction sets and usage patterns.
