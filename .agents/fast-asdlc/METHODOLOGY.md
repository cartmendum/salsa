# Fast-ASDLC Methodology (V1.1)

## 1. Core Paradigm
- **AI-Native & Agentic:** Agents execute 80-90% of tasks. Humans define intent and review outputs. Use **Meta-Agent** to orchestrate and fine-tune subordinate agents.
- **Model-Agnostic:** Optimized for high-performance open weights (Qwen, GLM) deployed on-prem for privacy.
- **Agent-Agnostic:** Portable system supporting diverse interfaces (OpenCode, Cursor, Cline, CLI, CI/CD and Docker). **Meta-Agent** handles cross-tool onboarding.
- **Git-Centric Workflow:** Every feature/bugfix starts with a feature-branch and a tracking file in `/.backlog/`.
- **Everything-as-Code:** All artifacts (Analysis, Architecture) are stored in Git as Markdown or Mermaid.js alongside source code and infrastructure code.
- **Spec-Driven Development:** Implementation is strictly based on markdown specs in `/docs/specs/`.

## 2. Agent Management & Orchestration
* **Meta-Agent:** Responsible for generating and tuning behavior via:
    - **Rules:** Core behavioral constraints and identity.
    - **Skills:** Specialized capabilities (e.g., C4 diagramming, Docker detection) often leveraging **MCP** servers.
    - **Workflows:** Step-by-step procedures for SDLC phases.
* **Fast-Guardian:** A specialized framework mentor that ensures correct onboarding and architectural compliance. Provides consultancy on **Fast-ASDLC**.
* **Context Economy:** Agents must summarize previous steps to save context window for the next agent in the chain.

## 3. Architectural Constraints
### 3.1 Domain-Driven Design (DDD)
- **Ubiquitous Language:** Shared vocabulary documented in `/docs/domain/glossary.md`.
- **Bounded Contexts:** Explicit boundaries defined via C4 Models.

### 3.2 C4 Model
- All diagrams MUST use **Mermaid.js**.
- Hierarchy: Context (System level) -> Container (Apps/DBs) -> Component (Internal logic).

### 3.3 Hexagonal Architecture (Ports & Adapters)
- **Domain Layer (`/src/{container-name}/domain`):** Pure business logic. Zero dependencies on external libraries or frameworks. 100% unit test coverage mandatory.
- **Application Layer:** Use cases and interfaces (Ports).
- **Infrastructure Layer:** DB, API, Messaging implementations (Adapters).
- **Strict Isolation:** Dependency direction must flow inward (Infra -> App -> Domain).
- **Backend containers source code structure:**
```
/src/{backend-container-name}/
├── domain/                # Core business logic: pure entities and domain rules.
│   ├── entities/          # Domain models with state, identity, and business invariants.
│   └── services/          # Operations involving multiple entities or complex domain logic.
├── application/           # Orchestration layer: coordinates tasks and delegates work.
│   ├── commands/          # Request objects for operations that change system state.
│   ├── queries/           # Request objects for data retrieval (read-only).
│   ├── handlers/          # Logic to process specific commands or queries.
│   ├── validators/        # Business rule and input validation logic for requests.
│   └── ports/             # Abstract interfaces for external dependencies (e.g., Repositories).
├── infrastructure/        # External world: technical implementations of application ports.
│   ├── persistence/       # Database adapters, ORM mappings, and data access.
│   └── gateways/          # Clients for external APIs, messaging, or third-party services.
└── bootstrap/             # Wiring: DI registration, framework setup, and entry points.
```
- **Frontend containers source code structure:**
```
/src/{frontend-container-name}/
├── ui/                    # View layer: Components, Screens, or Activities
├── domain/                # Pure logic: Entities and Domain Services
├── application/           # State management orchestration
│   ├── commands/queries/  # Action/Request definitions
│   ├── handlers/          # "Interactors" or "Use Cases" logic
│   └── ports/             # Interfaces for API/Storage
├── infrastructure/        # Adapters for API (Axios/Retrofit) and Local Storage
└── bootstrap/             # Context Providers, DI, or Store configuration
```
### 3.4 OOD and Cloud-Native
- **SOLID, SRP, OCP:** Prioritize creating new files over modifying old ones to minimize side effects, LLM errors, and prevent context drift.
- **CQRS:** Mandatory to ensure clear command/query separation.
- **Cloud-Native:** Follows 12-Factor App principles.
### 3.5. Security
- **Security-as-Code:** Threat modeling and risk assessments are mandatory for every new Container or major Component.

## 4. Operational Workflow (The "Line")
1. **Intention:** Lead creates a file in `.backlog/` with a task tracker link (e.g., Jira). Feature-branch is created.
2. **Analysis:** Analyst Agent + Human define Business Logic and UI Mocks in `docs/domain/`. Dictionary is updated in `docs/domain/glossary.md`. Handoff links are added to the backlog file.
3. **Architecture:** Architect Agent + Human create C4 models, Threat Models, and detailed Specs (class/filenames). Specs include required **Skill Lists** for Programmer Agents.
4. **QA Test Generation (HITL Gate):** QA Agent reads structured Acceptance Criteria from `/docs/domain/usecases/` and Architect's specs to generate automated test suites inside `/tests/`. Execution pauses for Human Review.
5. **Implementation:** Programmer Agent generates code/unit tests container-by-container (Independent -> Dependent).
6. **Environment Deployment:** Programmer Agent populates `infra/` for one-command SUT deployment.
7. **QA Dynamic Execution (HITL Gate):** QA Agent deploys SUT/DOC using `infra/` assets, executes integration, regression, load, and AppSec suites. If tests fail, QA logs structured defects in `.backlog/` for the Programmer. If they pass, results are output for Human Gate 2 review.
8. **Delivery:** Programmer Agent (DevSecOps skill) creates CI/CD pipelines. Final merge to `main` triggers full validation suite.

## 5. Quality Gates
- **Plan/Act Cycle:** Agents discuss plans before acting.
- **Mandatory Human Review:** Every stage (Analysis -> Arch -> Code -> QA) requires human approval.
- **Shift-Left Security:** Threat modeling starts at the Architecture phase.
