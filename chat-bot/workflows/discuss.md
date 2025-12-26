---
description: A workflow for discussing requirements, researching solutions, and validating mutual understanding.
---

# Discussion & Requirement Clarification Workflow

This workflow is triggered when the user initiates a discussion to clarify requirements, requesting research, analysis, or solution proposals.

## 1. Understand and Validate

- **Listen**: Carefully analyze the user's input.
- **Clarify**: Ask targeted questions if requirements are unclear.
- **Confirm**: Paraphrase to ensure you understand. Ask: "Do I have this right?"

## 2. Context & Research (Hybrid Approach)

- **Read Local First**: BEFORE searching, always read the relevant local files (using `view_file`, `grep_search`, etc.) to understand the existing architecture, patterns, and constraints. Solution MUST fit the current codebase.
- **Search Web**: Use `search_web` for latest documentation and best practices.
- **Synthesis**: Combine local context with external best practices.

## 3. Propose & Challenge

- **Critical Thinking**: Do not be a "Yes Man". Point out risks, complexity, or bad practices.
- **Propose**: Present a clear solution or analysis. Explain "Why".

## 4. Communication Style (Strict)

- **Concise**: Bullet points. No fluff.
- **No Hallucinations**: Verify APIs.

## 5. Execution Rules (NO CODING)

- **NO Auto-Coding**: Do NOT write/edit code in the codebase.
- **Discussion Only**: This phase is for planning and alignment only.

## 6. Finalization (Trigger: "ok done")

- **Trigger**: When the user says "ok done" (or similar):
  1.  **Stop Discussion**.
  2.  **Generate Plan**: Create a comprehensive Markdown file in `docs/` (e.g., `docs/feature-name_plan.md`).
  3.  **Content**: The plan must include:
      - **Summary**: What was agreed upon.
      - **Requirements**: The finalized requirements.
      - **Implementation Steps**: Step-by-step guide on what needs to be done.
      - **Verification**: How to test.
  4.  **Halt**: After writing the plan, **STOP**. Do not implement code. Wait for the user's next explicit instruction (e.g., "Implement the plan").
