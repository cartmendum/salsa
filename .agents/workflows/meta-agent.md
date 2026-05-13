# Workflow: Meta-Agent 

## Phase 1: Context & Alignment
1. **Initialize:** Read `/.agents/memory-bank/process-overview.md` to align with the specific AI-native Agentic SDLC requirements.
2. **Audit:** Index all existing instructions in `/.agents/rules/`, `/.agents/workflows/`, and `/.agents/skills/` to prevent logic duplication.
3. **Validate:** Check `/.agents/memory-bank/project-brief.md` to ensure the agent roles being created match the project's scale and tech stack.

## Phase 2: Structural Design & Pathing
1. **Categorize:** For every new requirement, determine if it is a **Rule** (Constraint), a **Workflow** (Step-by-step), or a **Skill** (Technical SOP).
2. **Route:** Assign the exact file path based on the type:
    - **Rule** -> `/.agents/rules/{role}.md` (Global or Role-specific)
    - **Workflow** -> `/.agents/workflows/{role}.md`
    - **Skill** -> `.agents/skills/{capability}/{capability}.md`
3. **Drafting (English Only):** 
    - Use imperative, token-efficient English.
    - Ensure every sub-agent inherits the "Commit on Demand" policy and strict Directory Standards.
    - Define clear **In/Out** boundaries for each agent (which folders they "own").

## Phase 3: Integration & Quality Gate
1. **Cross-Reference:** Ensure the **Architect** knows how to trigger the **Programmer**, and the **Programmer** knows which **Skills** to invoke.
2. **Review:** Verify that all new files comply with the `Language & Token Policy` (Instructions in EN, Docs according description in `/.agents/memory-bank/project-brief.md`).
3. **Dependency Check:** If a new Workflow is created, ensure the corresponding Role's `/.agents/rules/` points to it.

## Phase 4: Finalization & Handover
1. **Update Memory Bank:** 
    - Log the new capability in `/.agents/memory-bank/progress.md`.
    - Document the reasoning in `/.agents/memory-bank/decision-log.md`.
    - Update `/.agents/memory-bank/active-context.md` to reflect that the system is ready for the next agent's session.
2. **User Sync:** Present the created files and structure to the User.
3. **Git Safety:** **WAIT** for explicit user confirmation before any `git` operations. Use `git add` only for the new infrastructure files.
