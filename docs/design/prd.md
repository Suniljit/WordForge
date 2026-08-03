---
doc_type: prd
status: draft
depends_on: []
last_updated: 2026-08-03
---

# WordForge — PRD

## Problem Statement & Goals
Writing a new document from an existing draft or template today means either manually rewriting it by hand, or generating a whole new draft blind with a single AI prompt and losing control over structure and voice. WordForge lets an author extract the structure from an existing document, get an AI first pass tuned to a prompt, then refine the result section-by-section or paragraph-by-paragraph with AI assistance — including cascading updates when a change in one section should ripple to others — while staying in control of the final wording throughout.

## Target Persona
| Persona | Needs | Role / Permissions |
|---|---|---|
| Solo Author (e.g. consultant, PM, analyst) | Reuse a past or borrowed document as the basis for a new one; get a fast, structurally faithful first pass; retain fine-grained control while refining | Single role, no permissions split. No login for MVP — documents persist locally to the running instance without an account. |

## Feature Scope

### Must-haves (MVP)
- **Document import & extraction** — upload a draft or template as `.docx`, PDF, or Markdown; the system extracts its sections and text into an editable structure.
- **Prompt-guided initial draft** — given a prompt, the system produces a first-pass update of the extracted document before co-writing begins.
- **Co-writer navigation** — move through the document section-by-section or paragraph-by-paragraph.
- **Edit with AI (scoped edit)** — select any section, subsection, or paragraph and have the AI revise only that scope.
- **Cascading update orchestration** — when an edit to one section should affect others, an orchestrator agent auto-detects and proposes the likely-affected sections; on user confirmation, it spawns one sub-agent per affected section to apply the change.
- **Chat mode** — a conversational interface for describing a desired change; the orchestrator routes it to the relevant section(s), reusing the same per-section sub-agent mechanism as scoped cascades.
- **Version history & revert** — every AI-driven edit (single-section or a full cascade) is tracked and can be reviewed and reverted.
- **Export** — export the finished document to `.docx` and PDF.
- **Document list** — a flat, most-recent-first list of the user's documents.

### Nice-to-haves
- User accounts / login, enabling documents to persist across devices instead of only locally.
- Full search, filter, and tagging across the document library.
- Letting the user explicitly name target sections for a cascade, as an alternative to orchestrator auto-detection.

### Out-of-scope
- Real-time multi-user simultaneous editing (Google-Docs-style co-presence). This is a solo-author tool.
- "Tuned workflow" presets on the start page (e.g. a resume-writer or contract preset). Explicitly deferred to a later customization phase.
- Direct publish integrations (Google Docs, Notion, CMS, etc.) — export-only for MVP.

## User Stories & Acceptance Criteria
| User Story | Feature | Summary |
|---|---|---|
| [Import and extract a document](#import-and-extract-a-document) | Document import & extraction | Upload a draft/template, get it split into sections |
| [Generate an initial prompt-guided draft](#generate-an-initial-prompt-guided-draft) | Prompt-guided initial draft | First AI pass over the extracted document, guided by a prompt |
| [Navigate the document in co-writer mode](#navigate-the-document-in-co-writer-mode) | Co-writer navigation | Move section-by-section or paragraph-by-paragraph |
| [Edit a single section with AI](#edit-a-single-section-with-ai) | Edit with AI (scoped edit) | Revise just the selected section/paragraph |
| [Cascade an edit to other sections](#cascade-an-edit-to-other-sections) | Cascading update orchestration | Propose and apply a multi-section update from one edit |
| [Request a change via chat](#request-a-change-via-chat) | Chat mode | Describe a change conversationally, orchestrator routes it |
| [Review and revert an edit](#review-and-revert-an-edit) | Version history & revert | See what changed, undo a single edit or a whole cascade |
| [Export the finished document](#export-the-finished-document) | Export | Download the result as `.docx` or PDF |

### Import and extract a document
**Feature:** Document import & extraction
**As a** Solo Author, **I want** to upload a draft or template document, **so that** I can reuse its structure as the basis for a new document.
**Given** a user has a `.docx`, PDF, or Markdown file to use as a draft or template, **When** they upload it, **Then** the system extracts its sections and text into an editable, section-structured representation.

### Generate an initial prompt-guided draft
**Feature:** Prompt-guided initial draft
**As a** Solo Author, **I want** to describe the new document I need in a prompt, **so that** I get a structurally faithful first draft to start refining from.
**Given** an extracted document and a prompt describing the desired new document, **When** the user submits the prompt, **Then** the system produces a first-pass update applied across the extracted structure, ready for co-writing.

### Navigate the document in co-writer mode
**Feature:** Co-writer navigation
**As a** Solo Author, **I want** to move through my document section-by-section or paragraph-by-paragraph, **so that** I can focus my attention and edits at the level of detail I need.
**Given** a document with an initial draft in place, **When** the user enters co-writer mode, **Then** they can move between sections and paragraphs and see the current text at each level.

### Edit a single section with AI
**Feature:** Edit with AI (scoped edit)
**As a** Solo Author, **I want** the AI to revise only the section or paragraph I select, **so that** I can refine specific parts without affecting the rest of the document.
**Given** a user has selected a section, subsection, or paragraph, **When** they invoke "Edit with AI" with an instruction, **Then** only that selected scope is revised, leaving the rest of the document unchanged.

### Cascade an edit to other sections
**Feature:** Cascading update orchestration
**As a** Solo Author, **I want** the system to propose and apply related updates across other sections when I make an edit, **so that** my document stays consistent without manually updating every affected section.
**Given** a user has just edited a section and indicates other sections should be updated accordingly, **When** they request a cascade, **Then** the orchestrator proposes which other sections look affected, and on confirmation spawns one sub-agent per affected section to apply consistent updates.

### Request a change via chat
**Feature:** Chat mode
**As a** Solo Author, **I want** to describe a desired change in conversational language, **so that** I don't have to manually locate and select the exact section to edit.
**Given** a user is in chat mode, **When** they describe a desired change in natural language, **Then** the orchestrator determines which section(s) it applies to and dispatches the update via the same per-section sub-agent mechanism as a cascade.

### Review and revert an edit
**Feature:** Version history & revert
**As a** Solo Author, **I want** to see the history of AI-driven edits and revert any of them, **so that** I can undo unwanted changes with confidence.
**Given** a document has one or more AI-driven edits applied, **When** the user opens version history, **Then** they can see prior versions of any changed section and revert a single edit or an entire cascade back to its pre-edit state.

### Export the finished document
**Feature:** Export
**As a** Solo Author, **I want** to export my finished document to `.docx` or PDF, **so that** I can use it outside of WordForge.
**Given** a document the user is satisfied with, **When** they choose to export, **Then** the system produces a downloadable `.docx` or PDF matching the current state of the document.

## Success Metrics (KPIs)
| Metric | Target | How measured |
|---|---|---|
| Task success | % of co-writing sessions that end in an export, not abandoned | Sessions with a completed export ÷ total sessions started |
| Engagement | Avg. number of AI edit interactions (scoped edits, cascades, chat requests) per document | Count of edit-with-AI, cascade, and chat actions per document |
| Retention | % of users who return to co-write a second document within 30 days | Users with ≥2 documents started, second within 30 days of the first ÷ total users |

## Related
