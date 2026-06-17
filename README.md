# fm-token-reducer Skill

## Overview

`fm-token-reducer` is an **Antigravity CLI skill** that helps you conserve cloud compute tokens by delegating all code‑generation tasks to the local Apple Foundation Model (`fm` CLI). It implements a strict manager‑worker pipeline:

1. **Decompose** user requests into tiny, self‑contained subtasks.
2. **Delegate** each subtask to `fm` (the local LLM) using `fm respond "..."`.
3. **Review** the raw output for security and architectural fit.
4. **Save** the vetted code to your project.
5. **Iterate** until the whole request is complete.

The skill maintains a `summary.md` file that acts as a persistent architectural brain, automatically logging every change.

> **Why?**  After hitting my weekly token quota on cloud LLMs, I discovered Apple’s on‑device Foundation Model (the `fm` CLI) and built this workflow to keep development local, fast, and **privacy‑first**.

---

## Prerequisites

- **Antigravity CLI** installed and authenticated (see the official Antigravity docs).
- **Apple `fm` CLI** installed and set up on your macOS machine.
  - You can watch the Apple developer video introducing the local LLM here: https://developer.apple.com/videos/play/foundation-model-intro (replace with actual URL).
- A recent macOS version (Apple Silicon recommended) with access to the `fm` binary in `$PATH`.

## Installation

```bash
# From your project root (e.g., the repo containing this skill)
antigravity skill install fm-token-reducer
```

This command clones the skill into `./fm-token-reducer` and registers the slash command `/fm-token-reducer`.

## Setup

1. **Verify `fm` works**
   ```bash
   fm version   # should print the installed version
   ```
2. **Open the skill directory**
   ```bash
   cd fm-token-reducer
   ```
3. **Read the `summary.md`** (created automatically on first run). It contains the architecture log and will be updated after every task.
   ```bash
   cat summary.md
   ```
4. **Run the skill**
   ```bash
   antigravity /fm-token-reducer "Your request here"
   ```
   The skill will:
   - Break your request into micro‑tasks.
   - Call `fm respond "..."` for each.
   - Review the output.
   - Append the code to the appropriate files.
   - Log the action in `summary.md`.

## Usage Example

```bash
antigravity /fm-token-reducer "Add a utility function that formats dates as ISO strings."
```

The skill will:
- Prompt `fm` for a single Python function.
- Validate the generated code.
- Write it to `utils/date.py`.
- Append a line to `summary.md` like:
  ```
  - [$(date +%F)] Added ISO date formatter via fm delegation
  ```

## `summary.md` – Persistent Brain

`summary.md` tracks:
- Architectural decisions.
- New libraries or dependencies.
- Completed features (timestamped).
- Any manual overrides you make.

The file lives at the project root and is automatically committed by the skill after each successful sub‑task.

## Contributing

1. Fork the repo.
2. Make changes.
3. Ensure the manager‑worker workflow still works (`fm respond` → review → write).
4. Open a PR.

## License

MIT License – feel free to adapt and share.
