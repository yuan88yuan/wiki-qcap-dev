# Codebase Reviewer & Wiki Schema

This document defines the structure and workflows for the Codebase Reviewer and its associated Wiki system.

## Directory Structure
- `/raw`: The codebase under review (immutable source files).
- `/wiki`: LLM-maintained knowledge base documenting the codebase (summaries, architecture, components, index, log).

## Core Workflows

### 1. Codebase Analysis (Ingest)
When new code is added to `/raw` or a new module is explored:
1. **Analyze**: Review the code to identify its purpose, key functions, data structures, and dependencies.
2. **Summarize**: Create or update a summary page in `/wiki` for the module/file.
3. **Integrate**:
    - Update architectural overview pages in `/wiki`.
    - Map dependencies and components in relevant wiki pages.
    - Note design patterns used.
4. **Index**: Update `wiki/index.md` to include the newly documented parts of the codebase.
5. **Log**: Append an entry to `wiki/log.md`: `## [YYYY-MM-DD] analysis | File/Module Name`.

### 2. Query & Knowledge Capture
When asked a question about the codebase in `/raw`:
1. **Search**: Consult the codebase in `/raw` and existing documentation in `/wiki`.
2. **Synthesize**: Formulate a comprehensive answer based on the code.
3. **Update Wiki**: If the answer reveals new insights, logic, or architectural details not yet documented, create or update the corresponding page in `/wiki`.
4. **Cite**: Reference specific files and line numbers from `/raw` in the wiki updates.

### 3. Wiki Maintenance (Lint)
Periodically ensure the wiki reflects the current state of the code:
1. **Staleness**: Identify wiki pages that are outdated compared to the latest code in `/raw`.
2. **Gaps**: Find undocumented critical functions or modules in `/raw`.
3. **Consistency**: Ensure naming and terminology are consistent across the wiki and codebase.
4. **Maintenance**: Fix broken internal links `[[WikiPage]]`.

## Page Conventions
- All wiki pages are Markdown.
- Use `[[WikiPage]]` for internal cross-references.
- Use YAML frontmatter for metadata (tags, last reviewed date, related files).

## Constraints
- Don't git add any files in ./raw
- When referring to paths in ./raw, always use relative paths.
