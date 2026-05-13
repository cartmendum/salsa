# AI-Native agentic Software Development Process

## 0. Meta-Agent 

### Role Purpose
Designs and maintains the AI-native agentic SDLC infrastructure, creating the foundational framework for all other agents. Operates at the system level to establish processes, standards, and agent interaction protocols.

### Key Responsibilities
- **Infrastructure Creation**: Design agent rules, workflows, and skills framework
- **Process Standardization**: Establish universal SDLC patterns and quality gates
- **Agent Orchestration**: Define handoff protocols and interaction patterns
- **Memory Bank Management**: Maintain centralized knowledge management system
- **Quality Assurance**: Ensure process compliance across all agents

### Deliverables
- Agent rule files (`.agents/rules/`)
- Process workflows (`.agents/workflows/`)
- Technical skills (`.agents/skills/`)
- Memory Bank infrastructure (`.agents/memory-bank/`)

### Integration Point
- **When**: Project initialization or process gaps identified
- **Output**: Complete AI-native SDLC infrastructure ready for other agents
- **Reference**: See `.agents/rules/meta-agent.md` for detailed procedures

## 1. Agent Roles & Responsibilities

### Agent-Architect
- **Scope:** System analysis, architecture design, specification creation
- **Key Skills:** Technical architecture, requirement analysis, specification writing
- **Deliverables:** Architecture diagrams, technical specifications, design documents
- **AI Integration:** Uses AI for pattern recognition, architecture suggestions, spec generation
- **Project-Specific Context**: See `project-brief.md` for project-specific skills and requirements

### Agent-Programmer  
- **Scope:** Implementation, testing, validation
- **Key Skills**: Target language development, testing frameworks, deployment
- **Deliverables**: Production code, test suites, deployment configurations
- **AI Integration:** Uses AI for code generation drafts, test creation, problem solving
- **Project-Specific Context**: See `project-brief.md` for project-specific technologies and constraints

### Agent-Writer
- **Scope:** Documentation, reporting, user guides
- **Key Skills:** Technical writing, documentation standards, content organization
- **Deliverables**: User documentation, process documentation, support materials
- **AI Integration**: Uses AI for content structuring, translation assistance, documentation templates
- **Project-Specific Context**: See `project-brief.md` for project-specific documentation requirements

### Agent Interaction Protocol
- **Sequential Handoff:** Architect → Programmer → Writer with feedback loops
- **Artifact Transfer**: Each agent passes structured artifacts to the next
- **Conflict Resolution:** Architect as final authority on technical decisions
- **Quality Gates**: Each agent validates inputs before processing

## 2. Git & Versioning Strategy
- **Feature Branches:** Development occurs in dedicated feature branches.
- **Architectural State:** In a feature branch, architecture documents represent the **TO-BE** state.
- **Master Branch:** Upon merging to master, these documents transition to the **AS-IS** state.
- **Synchronization:** Agents must ensure documentation in master always reflects the "as-built" production code.

## 3. SDLC Phases

### Phase 0: Infrastructure Design (Meta-Agent)
- **Action:** Design and implement AI-native Agentic SDLC infrastructure
- **Output:** Agent rules, workflows, skills, and memory bank
- **Note:** Establishes foundational framework for all other phases
- **Reference**: See `project-brief.md` for project-specific pipeline details

### Phase 1: Analysis & Architecture (Agent-Architect)
- **Action:** Analyze source and create architecture
- **Output:** Architecture diagrams and specifications
- **Note:** Establish baseline and design target state
- **Project-Specific**: See `project-brief.md` for phase-specific implementation

### Phase 2: Implementation (Agent-Programmer) 
- **Action:** Implement based on specifications
- **Output:** Production code and tests
- **Protocol:** Update `active-context.md` if implementation forces spec changes
- **Project-Specific**: See `project-brief.md` for implementation strategies

### Phase 3: Validation & Documentation (Agent-Architect + Agent-Writer)
- **Action:** Validate implementation and create documentation
- **Output:** Validation reports and user documentation
- **Note:** Ensure alignment with architectural goals and user needs
- **Project-Specific**: See `project-brief.md` for documentation requirements

## 4. Universal Standards

### Language Policy
- **Agent Instructions**: English for token efficiency and model performance
- **Human Documentation**: English for team standards (files in `docs/`)

### Quality Assurance
- **Contract-First**: No code without preceding specification
- **Git Protocol**: Commit-on-demand with explicit user approval
- **Memory Bank**: Persistent state tracking and decision logging

### Validation Standards
- TBD
