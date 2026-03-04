# what-i-missed


Coming to a new project or an old one that you left for a while, and you wonder what is new?
Here is an agentic skill to summarize a project's git history with natural language. 

It instructs your LLM to intelligently filter git commit noise and group repository changes into **Feature**, **Bug Fix**, and **Chore** categories with concise one-liners.

## Installation & Setup


### Claude Code
Claude Code automatically discovers skills placed in specific directory structures.
1. Clone this repository.
2. Copy the `what-i-missed` directory into your global or project-level Claude skills folder:
   - **Global (Available in all projects):** 
     ```bash
     mkdir -p ~/.claude/skills/
     cp -r what-i-missed ~/.claude/skills/
     ```
   - **Project-level (Only in current project):** 
     ```bash
     mkdir -p .claude/skills/
     cp -r what-i-missed .claude/skills/
     ```

### Gemini CLI
Gemini CLI uses packaged `.skill` files for distribution.
1. Download the `what-i-missed.skill` file from this repository.
2. Install it globally using the Gemini CLI:
   ```bash
   gemini skills install what-i-missed.skill --scope user
   ```
3. Reload skills in your active Gemini session:
   ```bash
   /skills reload
   ```

### Cursor / Codex
For AI editors like Cursor that rely on context and rules files:
1. Open `what-i-missed/SKILL.md` and copy its contents.
2. Append the contents to your project's `.cursorrules` file.
3. Alternatively, save it as a standalone markdown file (e.g., `prompts/what-i-missed.md`) and @-mention it in your chat context when asking for a summary.

## Usage

Once installed, you can use natural language to ask your AI assistant about repository changes over any period:

- *"What have I missed in the past week?"*
- *"Use what-i-missed to summarize changes since Monday."*
- *"Summarize what happened in the last year."*
- *"What's new since commit a1b2c3d?"*

## How it Works

Instead of blindly repeating `git log` output, the skill provides your AI with a procedural workflow to:
1. Determine the exact `git log --since="..."` or SHA range from your natural language prompt.
2. Fetch the history and aggressively filter out non-informative messages (e.g., ".", "wip", "update stuff", "fixed bug").
3. Apply semantic heuristics (using the provided `categorization-guide.md`) to categorize each valid commit.
4. Output a clean, structured list grouped by intent.

## Example

Here is an example summary of a project of mine:

```
Over the past year, the AES67 streamer has evolved from a core implementation into a more feature-complete and documented tool. 
Key highlights include the integration of SAP and PTP for standard-compliant synchronization and discovery.


  Feature
   - Implemented SAP (Session Announcement Protocol) with a built-in announcer for automatic session discovery.
   - Added a full PTP (Precision Time Protocol) client to ensure high-fidelity synchronization.
   - Integrated SAP and PTP support directly into the main application.
   - Introduced a --verbose flag for easier debugging and set the default RTP port to 5004.


  Bug Fix
   - Resolved critical issues in the audio resampler and sample rate conversion logic.
   - Fixed performance bottlenecks and memory allocation bugs in the audio reader.
   - Corrected packet timing and sleep intervals to ensure stable streaming.
   - Addressed integer overflows and added bounds checking for safer audio format conversion.


  Chore
   - Completed Phase 5 (Integration & Optimization) of the development roadmap.
   - Significantly expanded documentation, including a professional README.md and updated CLAUDE.md.
   - Added a comprehensive E2E testing and validation suite for AES67 compliance.
   - Performed extensive code cleanup, including removing dead code and reducing log noise.
   - Established project licensing and improved test coverage for core audio modules.

```
