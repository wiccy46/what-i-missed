# Categorization Heuristics

When commit messages are vague, use these heuristics to determine the semantic category:

### 1. Feature (Heuristics)
- Changes in `src/` adding new modules, traits, or structs.
- Addition of new CLI flags in `config/`.
- New protocol implementations (e.g., PTP message parsing).

### 2. Bug Fix (Heuristics)
- "fixed", "bug", "crash", "error", "unintended" in message.
- "if" statements adding bounds checking or error handling.
- "unwrap()" replaced with safe error handling.

### 3. Chore (Heuristics)
- Changes only in `tests/` or `examples/`.
- Version bumps in `Cargo.toml`.
- Documentation changes (`README.md`, `CLAUDE.md`, `.md` files).
- Comment changes or code reformatting (whitespace, `rustfmt`).
- Renaming internal variables without logic changes.

### Vague Message Examples
| Commit Message | Inferred Category | Reason |
| :--- | :--- | :--- |
| "refactor audio engine" | Chore | Internal restructuring, no new functionality. |
| "added tests for rtp" | Chore | Test addition. |
| "updated dependencies" | Chore | Build process maintenance. |
| "handle empty packets" | Bug Fix | Logic correction for an edge case. |
| "it works" | (Check diff) | If new files in `src/`, then **Feature**; if just logic fix, then **Bug Fix**. |
