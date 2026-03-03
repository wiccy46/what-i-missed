---
name: what-i-missed
description: Summarizes recent git repository changes into features, bug fixes, and chores. Use when you want a concise "what's new" report for a specific period (e.g., "past week", "last year", or since a specific commit).
---

# What I Missed

This skill provides a high-level, categorized summary of repository changes. It intelligently filters noise and groups commits into semantic categories.

## Workflow

### 1. Determine the Time Range
Analyze the user's request for any mention of time or a specific commit.
- **Natural Language Time:** Map phrases like "past year", "last 3 months", "yesterday", "since Monday" to the appropriate `git log --since="..."` value.
- **Commit Reference:** If a commit SHA or tag is mentioned, use that as the starting point (e.g., `SHA..HEAD`).
- **Default:** If no period is specified, default to the **past 7 days**.

### 2. Fetch and Clean History
Retrieve commits using: `git log <range> --pretty=format:"%H|%s|%b" --no-merges`.
**Filter out non-informative commits:**
- Exclude subjects like: "update", "fix", "wip", ".", "asdf", "test", "commit", "minor changes".
- Exclude automated commits (e.g., "version bump", "dependency update" with no logic change).

### 3. Semantic Categorization
Group every relevant commit into exactly one of these three categories. If the commit message is vague, use the `references/categorization-guide.md` to infer the intent from the diff or context:
- **Feature:** User-facing changes, new capabilities, API additions, or significant enhancements.
- **Bug Fix:** Corrections to errors, crashes, or unintended behavior.
- **Chore:** Maintenance, documentation (e.g., `README.md`, `CLAUDE.md`), internal refactoring, test additions, and build configuration.

### 4. Output the Summary
Generate a concise list of **one-liners** grouped by category. Omit any category that has no relevant commits.

## Example Output
### Feature
- Added PTP master fallback mode for resilient synchronization.
- Implemented SAP/SDP support for automatic session discovery.

### Bug Fix
- Fixed RTP timestamp calculation for high-sample-rate audio files.
- Resolved memory leak in the audio node chain.

### Chore
- Updated project documentation for AES67 compliance details.
- Refactored network socket handling for better cross-platform support.
