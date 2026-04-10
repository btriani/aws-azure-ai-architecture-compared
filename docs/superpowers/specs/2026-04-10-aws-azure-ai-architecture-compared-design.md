# Design Spec: aws-azure-ai-architecture-compared

**Date:** 2026-04-10
**Status:** Draft

---

## 1. What This Is

A GitHub repo that compares how AWS and Azure approach AI/GenAI architecture at the thinking level, not the service catalog level.

Each comparison is grounded in what each cloud actually recommends (Well-Architected guidance, reference architectures, official documentation) with honest commentary on top: what's genuinely new, what's open-source with a managed wrapper, and where the enterprise governance justifies its cost.

Open-source stacks (Claude API + LangGraph, OpenAI API + LangChain, etc.) are referenced throughout as the baseline. The question is always: "What does the cloud platform add beyond what you could build yourself?"

## 2. Core Thesis

AWS and Azure wrap open-source AI capabilities with enterprise governance. The value of each platform is proportional to the governance you actually adopt. This project maps what each cloud recommends, where they agree, where they diverge, and when the enterprise wrapper is worth it.

## 3. Audience

- Cloud architects evaluating AI platforms for their organization
- Developers and ML engineers deciding whether to move from open-source stacks to cloud-managed services
- The author (learning artifact that earns its value by being rigorous enough for others to use)

## 4. What This Is NOT

- A service-to-service mapping table (included as appendix, not the point)
- A tutorial on how to use Bedrock or Azure OpenAI
- Certification prep material
- A recommendation of one cloud over the other

## 5. Approach: Hybrid (Analytical Core + Decision Layer)

The repo has two layers:

**Layer 1: Decision guide (top-level).** The README and a decision guide walk the reader through the actual decision journey: "Do I need a cloud AI platform? If so, which philosophy fits?" This is the entry point.

**Layer 2: Dimension analysis (core content).** Deep, structured comparisons organized by architectural dimension. Each document stands alone as a reference. These are the substance.

The decision guide links into the dimension docs. Readers can follow the journey or jump to a specific topic.

## 6. Repo Structure

```
aws-azure-ai-architecture-compared/
├── README.md
├── CONTRIBUTING.md
├── LICENSE
├── CHANGELOG.md
│
├── guide/
│   ├── decision-guide.md              # "Do I need a cloud AI platform?" flow
│   └── architecture-review-checklist.md # Unified checklist from both WAFs
│
├── dimensions/
│   ├── 01-well-architected.md
│   ├── 02-ai-ml-service-model.md
│   ├── 03-genai-patterns.md
│   ├── 04-mlops-genaiops.md
│   ├── 05-operating-model.md
│   └── 06-reference-architectures.md
│
├── tables/
│   ├── service-mapping.md              # Appendix: service-level mapping
│   └── framework-comparison.md         # Pillar-by-pillar WAF comparison
│
├── diagrams/
│   └── (Mermaid diagrams, architecture visuals)
│
└── assets/
    └── (images, sources)
```

## 7. Per-Dimension Document Structure

Every dimension doc follows the same template:

### 7.1 What does AWS recommend?
Cite actual guidance: Well-Architected lenses, reference architectures, official docs. Link to sources.

### 7.2 What does Azure recommend?
Same treatment. Cite Azure Well-Architected workload guidance, reference architectures, official docs. Link to sources.

### 7.3 Where do they agree?
When both clouds converge on a pattern, that's a strong signal the pattern is sound regardless of platform. Call it out.

### 7.4 Where do they diverge, and why?
The most valuable section. Explain the philosophical reason behind the divergence, not just the difference.

### 7.5 Honest take: genuine value vs. managed wrapper
For each capability in the dimension: is this something the cloud built from scratch, or is it open-source with governance bolted on? What specific governance does it add? If you don't use that governance, what are you paying for?

### 7.6 Balance point
At what organizational context (team size, compliance requirements, operational maturity) does the cloud approach justify its cost over the open-source baseline?

## 8. Dimension Details

### Dimension 01: Well-Architected Philosophy

**Focus:** How each cloud structures architectural thinking and review.

| Aspect | AWS | Azure |
|---|---|---|
| Framework | Well-Architected Framework, 6 pillars | Well-Architected Framework, 5 pillars + workload lenses |
| Review method | Question-based self-assessment via Well-Architected Tool | Assessment-driven with Azure Advisor integration |
| AI-specific guidance | ML Lens, GenAI Lens | AI workload guidance integrated into framework |
| Culture | OpsReview cadence, internal mechanisms made public | Enterprise assessment model, more prescriptive |

**Key question:** Do the frameworks lead you to different architectural decisions for the same workload? Where?

### Dimension 02: AI/ML Service Model

**Focus:** The overall approach to AI/ML services. Composable toolkit vs. integrated platform.

| Aspect | AWS | Azure |
|---|---|---|
| Core platform | SageMaker (broad toolkit of capabilities) | Azure AI Studio (integrated development environment) |
| Philosophy | Primitives you wire together | Integrated platform with guided workflows |
| Customization | High flexibility, higher assembly cost | Lower flexibility, faster time to first result |

**Key question:** When does "assemble your own" beat "use the integrated platform," and vice versa?

### Dimension 03: GenAI Architecture Patterns

**Focus:** How each cloud recommends building RAG, agents, fine-tuning, and prompt engineering workflows.

Specific patterns to compare:
- RAG: Bedrock Knowledge Bases vs. AI Search + On Your Data
- Agents: Bedrock Agents vs. Azure AI Agent Service
- Fine-tuning: Bedrock Custom Models vs. Azure OpenAI Fine-tuning
- Orchestration: Step Functions / custom code vs. Prompt Flow / Semantic Kernel
- Guardrails: Bedrock Guardrails vs. Azure AI Content Safety

For each pattern: what does each cloud recommend, what's the open-source equivalent, and what governance does the cloud version add?

### Dimension 04: MLOps / GenAIOps

**Focus:** How each cloud operationalizes ML and GenAI workloads.

| Aspect | AWS | Azure |
|---|---|---|
| ML pipelines | SageMaker Pipelines | Azure ML Pipelines |
| Model registry | SageMaker Model Registry | Azure ML Model Registry |
| Monitoring | SageMaker Model Monitor, CloudWatch | Azure ML Monitoring, App Insights |
| GenAI-specific ops | Bedrock model management, prompt versioning | AI Studio prompt flow versioning, content safety monitoring |
| CI/CD patterns | CodePipeline + SageMaker, or custom | Azure DevOps + Azure ML, or GitHub Actions |

**Key question:** How much of MLOps/GenAIOps is genuinely cloud-specific vs. patterns you'd follow on any stack (MLflow, Weights & Biases, etc.)?

### Dimension 05: Operating Model

**Focus:** Governance, cost management, security, identity, responsible AI.

This is where the enterprise value is most concrete. Topics:
- Identity and access: IAM vs. Azure AD/Entra ID
- Network isolation: VPC endpoints vs. Private endpoints
- Cost management: AWS billing + quotas vs. Azure Cost Management + PTU
- Responsible AI: Bedrock Guardrails vs. Azure Responsible AI tooling
- Data residency and compliance

**Key question:** Which of these governance features do teams actually use, and which sit unconfigured?

### Dimension 06: Reference Architecture Style

**Focus:** How each cloud publishes and structures its guidance.

A meta-comparison: how do you evaluate the guidance itself?
- Where does each cloud publish reference architectures?
- How prescriptive vs. flexible is the guidance?
- How often is it updated?
- How do you tell if guidance is current?

## 9. Decision Guide

The top-level decision guide walks through this flow:

```
1. Do I need a cloud AI platform at all?
   ├── What are you building? (complexity, scale, compliance needs)
   ├── What's your team's operational maturity?
   └── Answer: threshold where cloud platform earns its cost

2. If yes, which cloud's philosophy fits?
   ├── Do you want building blocks or an integrated platform?
   ├── What's your existing cloud footprint?
   ├── What compliance/identity requirements do you have?
   └── Answer: not "which is better" but "which fits your context"

3. What governance should you actually turn on?
   ├── Map your organizational maturity to governance features
   └── Answer: if you're not using these features, reconsider the platform choice
```

## 10. MVP Scope

Ship this first. Everything else is expansion.

**MVP deliverables:**
1. README with thesis, audience, structure, and navigation
2. `dimensions/01-well-architected.md` (full template, grounded in actual docs)
3. `dimensions/03-genai-patterns.md` (full template, grounded in actual docs)
4. `tables/framework-comparison.md` (pillar-by-pillar structured comparison)
5. `guide/decision-guide.md` (the three-question flow above)
6. One Medium article distilling the thesis and linking to the repo

**MVP does NOT include:**
- Dimensions 02, 04, 05, 06 (expansion)
- Architecture review checklist (expansion)
- Diagrams (expansion)
- Hands-on labs (future)
- Service mapping appendix (expansion)

## 11. Expansion Roadmap (Post-MVP)

**Phase 2: Complete dimensions**
- Write dimensions 02, 04, 05, 06
- Add service mapping appendix

**Phase 3: Visual and actionable artifacts**
- Mermaid decision trees in decision guide
- Architecture diagrams for key patterns (RAG, agents, MLOps pipeline)
- Architecture review checklist synthesizing both WAFs

**Phase 4: Hands-on (ambitious)**
- Mini reference architectures: same workload on AWS, Azure, and open-source
- IaC templates (Terraform) for key patterns
- Cost comparison for running the same workload on each platform

## 12. What Makes It Useful to Others

1. **Grounded in actual docs, not opinions.** Every claim links to the AWS or Azure source.
2. **The governance honesty.** Nobody else says "this service is basically open-source + a billing wrapper." People need to hear it.
3. **The balance point in every dimension.** Not "it depends" but "at this level of organizational maturity, this is worth it."
4. **The decision guide.** A practical flow someone can use in a real architecture review.

## 13. What Makes It Portfolio-Worthy

1. **Original analysis.** Not a rehash of documentation. A framework for thinking.
2. **Demonstrates architectural thinking.** Shows you operate at the "why" level, not just the "what" level.
3. **Honest and opinionated.** Willingness to say "this adds no value over open-source for most teams" shows confidence and credibility.
4. **Well-structured and maintained.** Date-stamped, version-noted, source-linked.

## 14. Risks and Mitigations

| Risk | Mitigation |
|---|---|
| Scope creep beyond MVP | MVP is 5 files + 1 article. Don't touch expansion until those ship. |
| Staleness | Date-stamp every document. Note framework versions. Accept it's a living resource. |
| Too much narrative, not enough structure | Follow existing repo style: tables, bullets, progressive disclosure. If a section is longer than one screen, restructure it. |
| False equivalence | When something doesn't map 1:1, say so. "Azure has no equivalent because..." is more valuable than a forced mapping. |
| Governance claims without evidence | Cite specific features and link to docs. "Bedrock adds IAM integration" must link to the IAM doc, not be a vague claim. |

## 15. Tone Guidelines

- Direct and practical. Short sentences. Periods over dashes.
- Match the tone of existing repos (ai-300-lab-guide, databricks-genai-lab-guide): scannable, no filler.
- Opinionated but grounded. Every opinion links to evidence.
- Personal voice, not generated-sounding. Avoid em-dash chains and polished-but-hollow phrasing.
