# Workflow: Fast-Guardian - Fine-Tune Agent

## 1. Objective & Scope
- **Purpose:** Sequence of steps for Fast-Guardian to create a new agent or modify rules and workflows of an existing agent.
- **Scope Restriction:** Restricted to files inside `/.agents/rules/` and `/.agents/workflows/`. No production code interaction.

## 2. Inputs & Pre-conditions
- **Inputs:** 
  - Target Agent Name (e.g., `analyst`, `qa`).
  - Human Intent / Change Request (via CLI prompt or backlog file).
- **Pre-conditions:** `/.agents/fast-asdlc/METHODOLOGY.md` must be present and indexed.

## 3. Execution Lifecycle (Step-by-Step)

### Phase 1: Context Discovery & Plan
1. **Analyze Request:** Parse the human intent. Identify if the action is `CREATE` or `MODIFY`.
2. **Scan Existing Manifests:** If `MODIFY`, read the target agent's current `rules/.md` and `workflows/.md` files.
3. **Verify Constraints:** Cross-check the requested agent behavior against `METHODOLOGY.md` to prevent role overlap or security boundary violations.
4. **Formulate Plan:** Output a summary of proposed architectural changes or new agent specifications.

### Phase 2: Quality Gate 1 (Human Conceptual Approval)
5. **Await Intent Confirmation:** Pause execution. Present the proposed plan to the human supervisor.
6. **Evaluate Feedback:** If rejected, loop back to Step 1. If approved, transition to Phase 3.

### Phase 3: Generation & Fine-Tuning
7. **Execute Skill - Template Generation:** Invoke the specific technical capability defined in `/.agents/skills/fast-asdlc-agent-scaffolding/fast-asdlc-agent-scaffolding.md` to draft or update the agent manifests.
8. **Enforce Structural Rules:** Ensure rules files use declarative `MUST/MUST NOT` constraints and avoid code logic. Ensure workflows files contain only step sequences.
9. **Context Optimization:** Minimize token usage by stripping conversational language and ensuring zero duplicate constraints between the rules and workflows files.

### Phase 4: Quality Gate 2 (Human Artifact Review)
10. **Present Diff/Draft:** Display the full markdown output of the generated rules and workflows to the human supervisor.
11. **Apply Corrections:** Incorporate minor human feedback directly. If major updates are needed, repeat Phase 3.

### Phase 5: Commit & Persist
12. **Write Files:** Save the finalized assets to `/.agents/rules/[agent_name].md` and `/.agents/workflows/[agent_name].md`.
13. **Log Decision:** Log the creation/modification event to `/.agents/memory-bank/decision-log.md`.
