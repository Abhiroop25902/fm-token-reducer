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
  - You can watch the Apple developer video introducing the local LLM here: https://developer.apple.com/videos/play/wwdc2026/334/
- MacOS 27 (I use M3 16gb) with access to the `fm` binary in `$PATH`.

## License

MIT License – feel free to adapt and share.
