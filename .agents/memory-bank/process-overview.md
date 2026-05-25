# Fast-ASDLC: Software Development Process & AI Runtime Overview

## 1. Local AI Execution Environment (Model-Agnostic Setup)
*Meta-Agent references this to adjust token chunking, reasoning latency, and context limitations.*
- **Deployment Strategy:** [e.g., On-Prem Local Server, Shared Corporate Cluster, Private Cloud GPU VM].
- **Inference Engine Platform:** [e.g., Ollama v0.x, vLLM Server API, lmstudio].
- **Primary Reasoning / Orchestration Model:** [e.g., GLM-4-9B-Chat, Llama-3.3-70B].
- **Primary Code Generation Model:** [e.g., Qwen-2.5-Coder-32B-Instruct, DeepSeek-Coder-V2].

## 2. Local Human-Agent Interface Setup & Role Mapping
*Identifies which wrapper tools the human and specific agents use to execute the pipeline.*
- **Primary IDE Environment:** [e.g., Cursor IDE, VS Code with Cline Extension, Windsurf].
- **CLI Workspace Tooling:** [e.g., Native Zsh/Bash, Tmux Workspace automation].

### 2.1 Role-to-Tool Matrix
*Meta-Agent references this matrix to compile environment-specific configuration files (e.g., .cursorrules, .clinerules) restricting agent behavior to their designated workspaces.*


| SDLC Role Agent | Target IDE / Interface | Agentic Tool / Wrapper | Workspace Restriction |
| :--- | :--- | :--- | :--- |
| **Analyst Agent** | [e.g., VS Code / Obsidian] | [e.g., Cline / None] | `/.backlog/`, `/docs/domain/` |
| **Architect Agent**| [e.g., VS Code] | [e.g., Cline / CLI] | `/docs/` (domain, specs, arch) |
| **Programmer Agent**| [e.g., Cursor IDE] | [e.g., Cursor Composer / Cline]| `/src/`, `/tests/`, `/infra/` |
| **QA Automation** | [e.g., CLI / Windsurf] | [e.g., Custom CLI script / Cline]| `/tests/`, `/docs/specs/` (READ) |


## 3. Target Infrastructure Manifest Targets
*Guides the DevOps agent on where manifests must land.*
- **CI/CD Orchestration Tool:** [e.g., GitHub Actions local runner, GitLab CI, Jenkins].
- **Infrastructure-as-Code Engine:** [e.g., Terraform, Ansible, Pure K8s Manifests].
- **Application Security Tooling:** [e.g., SonarQube, Trivy Container Scanning].

## 4. The Meta-Agent (Process Architect) Role
- **Role Purpose:** Designs, initializes, and continuously fine-tunes the local AI-native agentic SDLC infrastructure.
- **Responsibilities:** Configures agent identities (`rules/`), operational sequences (`workflows/`), and capabilities (`skills/`). Integrates tool environments.
- **Deliverables:** Operational configurations for downstream project agents based on `project-brief.md` constraints.

## 5. Agentic Workforce Roles
- **Analyst Agent:** Translates human intentions into Use Cases, UI mocks, and Ubiquitous Language mappings inside `/docs/domain/`.
- **Architect Agent:** Builds C4 Model views (Mermaid.js), enforces Threat Modeling, and produces strict, low-level execution task files inside `/docs/specs/`.
- **Programmer Agent:** Implements production logic, unit tests, and infrastructure automation containers (`infra/`) sequentially.
- **QA Automation Agent:** Orchestrates integration/load validation setups by deploying the System Under Test (SUT) and tracking bugs.

## 6. Git-Centric Lifecycle & Quality Gates
- **Isolation:** Every backlog task triggers a dedicated feature-branch.
- **The Backlog "Bus":** The tracking file in `.backlog/` acts as the context handoff bus. Each agent appends links to their newly created artifacts.
- **State Transition:** Architectural assets inside a feature branch represent the *TO-BE* state. Upon successful human review and merge to `main`, they transition to the definitive *AS-IS* system state.
- **Human-in-the-Loop:** Explicit human validation checkpoints block every inter-agent role transition.

## 7. SDLC Phase Execution Sequence
- **Phase 0 (Infrastructure Setup):** Meta-Agent reads `project-brief.md` and `process-overview.md`, then initializes/updates the agent workforce manifests and tool configurations.
- **Phase 1 (Analysis & Design):** 
  - Analyst Agent builds requirements and Use Cases with formal Acceptance Criteria inside `/docs/domain/usecases/` and updates `/docs/domain/glossary.md`. [HITL Gate]
  - Architect Agent inputs these use cases to construct C4 models (Mermaid.js), Threat Models, and low-level specifications (file/class/method names) inside `/docs/specs/`.
  - QA Agent instantly performs static contract analysis of the generated architecture against the analytical use cases to verify design completeness before any code is written. [HITL Gate]
- **Phase 2 (Additive Implementation):** Programmer Agent writes code container-by-container (Independent -> Dependent) inside `/src/` and unit tests inside `/tests/`. Adheres strictly Architect`s specs.
- **Phase 3 (Environment Deployment):** Programmer Agent (via DevOps skills) populates `/infra/` with orchestration manifests to allow one-command sandbox deployment.
- **Phase 4 (Validation & Quality Gating):** 
  - QA Agent translates Acceptance Criteria from `/docs/domain/usecases/` into executable automated test suites inside `/tests/`. [HITL Gate]
  - QA Agent executes deployment scripts from `/infra/` to spin up the System Under Test (SUT) and Component Stubs (DOC). 
  - QA Agent runs functional integration, regressions, performance, and AppSec vulnerability scans. Structured defect reports are logged directly in `.backlog/` if tests fail.
- **Phase 5 (Delivery):** Final human code audit, confirmation of test logs, and branch merge to `main` via DevSecOps CI/CD pipelines.

## 8. Universal Standards

### Language Policy
- **Agent System Prompts:** Strictly English for optimal token density and instruction following.
- **Project Documentation & Artifacts:** Dynamically governed by the *Language & Documentation Policy* defined in `.agents/memory-bank/project-brief.md`.

### Quality Engineering Foundations
- **Contract-First Constraint:** Code generation is prohibited without an approved upstream specification file.
- **Test Coverage Gates:** 100% unit test coverage required for the pure Domain layer; minimum 90% for Application and Infrastructure layers.
- **Context Preservation:** Agents must actively summarize task history inside `.agents/memory-bank/active-context.md` to protect the LLM context window.
