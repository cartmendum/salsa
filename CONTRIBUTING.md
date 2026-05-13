# Contributing to Fast-ASDLC

First of all, thank you for considering contributing to Fast-ASDLC! Our goal is to maintain a world-class AI-native Agentic SDLC framework, and that requires high standards.

## 🏛 Our Philosophy: BDFL & Quality First
Fast-ASDLC follows the **BDFL (Benevolent Dictator For Life)** model. The author maintains final approval over all changes to ensure the framework remains architecturally consistent and optimized for AI agents.

### The Gold Standards
Every contribution must strictly adhere to [Fast-ASDLC methodology](/.agents/fast-asdlc/METHODOLOGY.md) and core Fast-ASDLC principles:
1.  **Everything-as-Code:** Documentation, diagrams, code, and infrastructure are code.
2.  **Hexagonal Architecture:** Strict isolation of the Domain layer.
3.  **SOLID Principles:** Especially the Single Responsibility and Open/Closed principles.
4.  **Spec-Driven:** No implementation code should be submitted without a corresponding architectural specification in `/docs/specs/`.
5.  **LLM-Friendly:** Markdown and Mermaid.js are preferred to minimize context window usage.

## 🛠 How to Contribute

### 1. Proposing Changes
Before writing code, please **open an Issue** to discuss your idea. This prevents wasted effort if the proposal doesn't align with the framework's core pillars.

### 2. Branching Policy
- Create a feature branch from `main`.
- Use descriptive names: `feat/add-mcp-server-for-jira` or `fix/meta-agent-skill-logic`.

### 3. Pull Request (PR) Requirements
To be considered for merging, a PR must:
- **Pass Linting:** Clean Markdown and valid Mermaid syntax.
- **Architecture Check:** Demonstrate compliance with core Fast-ASDLC principles.
- **Test Coverage:** 
  - **100% Coverage** for Domain/Business logic.
  - **>90% Coverage** for Application/Infrastructure layers.
- **Documentation:** Any change in agent workflows must be reflected in the `/.agents/` folder.

## 🔍 The Review Process
1.  **Architectural Review:** The author will personally review the PR for compliance with Fast-ASDLC principles.
2.  **Iteration:** Be prepared to make changes. We value "clean over fast."

## 💎 Rewards & Recognition
Significant contributors (Core Contributors) who have 3+ major PRs merged will be:
- Featured in the **"Wall of Fame"** in the main README.
- Given priority in discussing the project's roadmap.

---

By contributing, you agree that your code will be licensed under the **MIT License**.

**Let's build the future of AI-native engineering together!**
