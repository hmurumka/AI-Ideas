# Spec: Requirements & Workflow

## Purpose
Consolidated, authoritative specification for requirement gathering, impact analysis, JIRA artifact generation, approval workflow, and agent execution.

## 1. Requirement Gathering

Inputs: Customer feedback, Sales updates, Market context.

AI Role:
- Provide a centralized intake portal where Customer/Sales can asynchronously log requirements.
- Auto-classify inputs into Known vs Unknown:
  - Known → mapped to existing repos/components (Stories).
  - Unknown → flagged for JIRA Spike (POC / research / discussion).

## 2. Impact Analysis

- AI scans the codebase & services to identify impacted repos/components.
- Generates a dependency graph (component-level).
- Highlights cross-team dependencies and risk areas.

## 3. Epic & Story Creation

- Business Epics -> Quarterly roadmap chunks.
- Technical Epics -> Component-level breakdown.
- Stories -> Known tasks, created as "Ready for Approval".
- Spikes -> Unknowns requiring exploration.

## 4. Approval Workflow

- Every story starts as Ready for Approval.
- AI generates approval checklist (Architect, QA Lead, Product Owner by default).
- Agents remain locked until all required approvers mark ✅.
- Once fully approved, Epic Agent orchestrates sub-agents.

## 5. Agent Execution

- Epic Agent: orchestrator per business Epic. Responsibilities include monitoring JIRA, filtering Approved stories, triggering sub-agents and consolidating progress.
- Sub-agents:
  - Coding Agent — implements repo changes and creates commits/PRs.
  - Testing Agent — prepares and runs regression/unit tests and triggers CI/CD.
  - Documentation Agent — updates Confluence pages and generates HLD/LLD diagrams.

Agents should report progress back to the Epic Agent and write audit entries to the DB/Confluence.

## 6. Governance & Traceability

- Approval gates and demo/review checkpoints enforced before execution.
- Audit trail recorded (who approved, when, and what changed).
- Confluence pages generated per Epic/Story for traceability.

## 7. Weekly Async Sync

- AI prepares weekly digest dashboards: progress vs plan, risks & unknowns, upcoming demos and reviews.
- Shared asynchronously with stakeholders.

## 8. Example Flow (summary)

1. Customer logs requirement → AI tags impacted repos.
2. AI generates dependency graph → identifies impacted components.
3. Known tasks → Stories; Unknowns → Spikes.
4. Business Epic created → Technical Epics + Stories.
5. Confluence auto-doc (HLD + LLD).
6. Approval checklist sent → on approval Epic Agent triggers sub-agents.
7. Weekly digest produced and shared.

## 9. JIRA Workflow (Known Work Stories)

Workflow States:
- Story Created → Ready for Approval (auto-assigned approvers, AI generates checklist)
- Approval Pending → agents are locked until all approvals ✅
- Approved → Agent Execution (Coding, Testing, Documentation)
- In Progress → Demo/Review
- Done → Closed (dependency graph and Confluence updated)

---

For Confluence templates and approval checklist, see: ../templates/confluence-story-template.md and ../templates/approval-checklist.md
