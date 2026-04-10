# aws-azure-ai-architecture-compared: MVP Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Ship the MVP of the aws-azure-ai-architecture-compared repo: README, two dimension analyses (Well-Architected + GenAI Patterns), a framework comparison table, a decision guide, and a Medium article draft.

**Architecture:** Content repo with two layers. Layer 1: a decision guide that walks the reader through the choice. Layer 2: dimension docs that go deep on specific topics. Every dimension doc follows a six-section template grounded in actual AWS/Azure documentation, with honest commentary on governance value vs. open-source alternatives.

**Tech Stack:** Markdown, Mermaid (diagrams in decision guide), Git, GitHub

**Design spec:** `docs/superpowers/specs/2026-04-10-aws-azure-ai-architecture-compared-design.md`

---

## File Map

| File | Responsibility | Task |
|---|---|---|
| `README.md` | Thesis, audience, navigation, repo identity | Task 1, Task 7 |
| `LICENSE` | MIT license | Task 1 |
| `.gitignore` | Standard ignores | Task 1 |
| `tables/framework-comparison.md` | Pillar-by-pillar WAF comparison table | Task 2 |
| `dimensions/01-well-architected.md` | Deep analysis: WAF philosophy, review method, AI guidance | Task 3 |
| `dimensions/03-genai-patterns.md` | Deep analysis: RAG, agents, fine-tuning, guardrails compared | Task 4 |
| `guide/decision-guide.md` | Three-question flow: "Do I need a cloud AI platform?" | Task 5 |
| `drafts/medium-article.md` | Medium article draft distilling the thesis | Task 6 |
| `README.md` | Final polish with links to all completed files | Task 7 |

## Key Sources

These are the primary documents to research and cite throughout the dimension docs.

**AWS:**
- Well-Architected Framework: https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
- Well-Architected ML Lens: https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html
- Well-Architected GenAI Lens: https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html
- Bedrock User Guide: https://docs.aws.amazon.com/bedrock/latest/userguide/
- Bedrock reference architectures: https://aws.amazon.com/architecture/reference-architecture-diagrams/ (filter for GenAI)
- SageMaker documentation: https://docs.aws.amazon.com/sagemaker/

**Azure:**
- Well-Architected Framework: https://learn.microsoft.com/en-us/azure/well-architected/
- AI workload guidance: https://learn.microsoft.com/en-us/azure/well-architected/ai/
- Azure OpenAI Service docs: https://learn.microsoft.com/en-us/azure/ai-services/openai/
- Azure AI Studio docs: https://learn.microsoft.com/en-us/azure/ai-studio/
- Azure Architecture Center (AI): https://learn.microsoft.com/en-us/azure/architecture/ai-ml/

---

### Task 1: Repository Scaffolding

**Files:**
- Create: `README.md`
- Create: `LICENSE`
- Create: `.gitignore`
- Create: `dimensions/` (empty directory with `.gitkeep`)
- Create: `tables/` (empty directory with `.gitkeep`)
- Create: `guide/` (empty directory with `.gitkeep`)
- Create: `diagrams/` (empty directory with `.gitkeep`)
- Create: `drafts/` (empty directory with `.gitkeep`)
- Create: `assets/` (empty directory with `.gitkeep`)

- [ ] **Step 1: Initialize git repo**

```bash
cd <project-root>
git init
```

- [ ] **Step 2: Create .gitignore**

Create `.gitignore`:

```
.DS_Store
*.swp
*.swo
*~
.vscode/
.idea/
```

- [ ] **Step 3: Create LICENSE**

Create `LICENSE` with MIT license text. Use the author name "btriani" and year 2026.

- [ ] **Step 4: Create directory structure**

```bash
mkdir -p dimensions tables guide diagrams drafts assets
touch dimensions/.gitkeep tables/.gitkeep guide/.gitkeep diagrams/.gitkeep drafts/.gitkeep assets/.gitkeep
```

- [ ] **Step 5: Create initial README.md**

Create `README.md` with this content:

```markdown
# AWS vs Azure AI Architecture Compared

An honest comparison of how AWS and Azure approach AI and GenAI architecture. Not a service mapping. A comparison of how each cloud thinks about building AI systems, what governance each platform adds, and when the enterprise wrapper is worth it.

## Why This Exists

Most AWS-vs-Azure comparisons are shallow service mappings: "SageMaker = Azure ML, Bedrock = Azure OpenAI, done." That tells you nothing about which patterns to follow or why.

This project compares architectural thinking. What does each cloud recommend? Where do they agree? Where do they diverge? And for each capability: is this genuinely new, or is it open-source with a managed wrapper and governance bolted on?

Open-source stacks (Claude API + LangGraph, OpenAI API + LangChain, etc.) are the baseline. The question is always: what does the cloud platform add beyond what you could build yourself?

## Who This Is For

- Cloud architects evaluating AI platforms for their organization
- Developers and ML engineers deciding whether to move from open-source stacks to cloud-managed services
- Anyone who wants honest trade-off analysis instead of marketing

## Structure

This repo has two layers:

**Decision guide** (start here)
- [Decision Guide](guide/decision-guide.md) — "Do I need a cloud AI platform? If so, which one fits?"

**Dimension analysis** (deep dives)
- [Well-Architected Philosophy](dimensions/01-well-architected.md) — how each cloud structures architectural thinking and review
- [GenAI Architecture Patterns](dimensions/03-genai-patterns.md) — RAG, agents, fine-tuning, guardrails compared

**Quick reference**
- [Framework Comparison Table](tables/framework-comparison.md) — pillar-by-pillar WAF comparison

## How to Read This

Start with the [Decision Guide](guide/decision-guide.md) if you want the practical flow.

Jump to a dimension doc if you want depth on a specific topic.

Use the [Framework Comparison Table](tables/framework-comparison.md) as a quick reference.

## Per-Dimension Format

Every dimension doc follows the same structure:

1. **What does AWS recommend?** — grounded in actual docs, with source links
2. **What does Azure recommend?** — same treatment
3. **Where do they agree?** — convergence signals strong patterns
4. **Where do they diverge, and why?** — the most valuable section
5. **Honest take: genuine value vs. managed wrapper** — what governance does the cloud version add?
6. **Balance point** — at what organizational context is the cloud approach worth it?

## Versioning

Cloud guidance changes. Every document is date-stamped and notes which framework versions it references. If something looks outdated, check the date and open an issue.

## Status

This is a living resource. Current coverage:

| Dimension | Status |
|---|---|
| Well-Architected Philosophy | MVP |
| AI/ML Service Model | Planned |
| GenAI Architecture Patterns | MVP |
| MLOps / GenAIOps | Planned |
| Operating Model | Planned |
| Reference Architecture Style | Planned |

## License

MIT
```

- [ ] **Step 6: Commit**

```bash
git add .gitignore LICENSE README.md dimensions/.gitkeep tables/.gitkeep guide/.gitkeep diagrams/.gitkeep drafts/.gitkeep assets/.gitkeep
git commit -m "repo setup: scaffold structure and initial README"
```

---

### Task 2: Framework Comparison Table

**Files:**
- Create: `tables/framework-comparison.md`

This is the foundation piece. It's a structured, factual comparison that the dimension docs will reference. Research both frameworks before writing.

- [ ] **Step 1: Research AWS Well-Architected Framework**

Read the AWS Well-Architected Framework overview. Extract:
- The 6 pillars and their one-line descriptions
- The review methodology (how AWS recommends using the framework)
- AI/ML-specific lenses available (ML Lens, GenAI Lens)
- The Well-Architected Tool and how it works

Source: https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html

- [ ] **Step 2: Research Azure Well-Architected Framework**

Read the Azure Well-Architected Framework overview. Extract:
- The 5 pillars and their one-line descriptions
- The review methodology (Azure Well-Architected Review, Azure Advisor)
- AI workload-specific guidance
- Assessment tools and how they work

Source: https://learn.microsoft.com/en-us/azure/well-architected/

- [ ] **Step 3: Write tables/framework-comparison.md**

Create `tables/framework-comparison.md` with this structure:

```markdown
# Framework Comparison: AWS vs Azure Well-Architected

**Last updated:** 2026-04-10
**AWS WAF version:** [note version/date from docs]
**Azure WAF version:** [note version/date from docs]

## Pillars

| AWS Pillar | Description | Azure Equivalent | Description | Notes |
|---|---|---|---|---|
| Operational Excellence | [from docs] | Operational Excellence | [from docs] | [where they differ] |
| Security | [from docs] | Security | [from docs] | [where they differ] |
| Reliability | [from docs] | Reliability | [from docs] | [where they differ] |
| Performance Efficiency | [from docs] | Performance Efficiency | [from docs] | [where they differ] |
| Cost Optimization | [from docs] | Cost Optimization | [from docs] | [where they differ] |
| Sustainability | [from docs] | (no direct equivalent) | — | [note why Azure excludes this] |

## Review Methodology

| Aspect | AWS | Azure |
|---|---|---|
| Primary tool | Well-Architected Tool (question-based) | Azure Well-Architected Review + Azure Advisor |
| Approach | Self-assessment via structured questions | Assessment-driven with automated recommendations |
| Cadence | Recommended as recurring practice (OpsReview culture) | On-demand or triggered by Azure Advisor |
| Output | Improvement plan with prioritized actions | Recommendations with severity and impact |
| Who runs it | Team self-service, or with AWS SA | Self-service, or with Microsoft architect |

## AI/ML-Specific Guidance

| Aspect | AWS | Azure |
|---|---|---|
| Dedicated lens/guidance | ML Lens + GenAI Lens (separate documents) | AI workload guidance (integrated into main framework) |
| Scope | ML Lens covers training, inference, MLOps. GenAI Lens covers foundation models, RAG, agents. | Covers AI workloads as a workload type within the main framework pillars |
| Structure | Adds AI-specific questions to each pillar | Adds AI-specific recommendations to each pillar |
| Prescriptiveness | Question-based: "Have you considered X?" | Recommendation-based: "You should do X" |

## Key Differences

[2-3 paragraphs noting the most significant philosophical differences found during research. Focus on differences that would lead to different architectural decisions, not just different labels for the same thing.]

## Sources

- [AWS Well-Architected Framework](link)
- [AWS ML Lens](link)
- [AWS GenAI Lens](link)
- [Azure Well-Architected Framework](link)
- [Azure AI Workload Guidance](link)
```

Fill all cells with actual content from the research in Steps 1-2. No placeholders. Every cell should contain real information from the docs.

- [ ] **Step 4: Quality check**

Verify:
- Every cell in every table has real content (no TBD, no placeholders)
- Every claim has a source URL at the bottom
- Pillar mappings are accurate (don't force 1:1 where it doesn't exist)
- The "Key Differences" section contains actual analysis, not vague statements

- [ ] **Step 5: Commit**

```bash
git add tables/framework-comparison.md
git commit -m "add framework comparison table: AWS vs Azure WAF pillar-by-pillar"
```

---

### Task 3: Dimension 01 — Well-Architected Philosophy

**Files:**
- Create: `dimensions/01-well-architected.md`

This is the first full dimension doc. It follows the six-section template from the spec and goes deeper than the comparison table.

- [ ] **Step 1: Research AWS Well-Architected for AI (deep read)**

Go beyond the overview. Read:
- AWS Well-Architected ML Lens: focus on the specific questions it asks per pillar for ML workloads
- AWS Well-Architected GenAI Lens: focus on how it handles foundation model selection, RAG patterns, responsible AI
- How the Well-Architected Tool works in practice (the review flow)
- Any public writing about AWS's OpsReview culture and how it influences the framework

Extract specific examples of questions the framework asks. These are the evidence for "question-based approach."

Sources:
- https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html
- https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html

- [ ] **Step 2: Research Azure Well-Architected for AI (deep read)**

Read:
- Azure Well-Architected AI workload guidance: focus on how recommendations are structured per pillar
- How Azure Advisor integrates with the framework (automated checks vs. manual assessment)
- Azure Well-Architected Review tool and its assessment flow
- How Azure structures "design principles" vs. "recommendations" vs. "tradeoffs"

Extract specific examples of recommendations the framework makes. These are the evidence for "prescriptive approach."

Sources:
- https://learn.microsoft.com/en-us/azure/well-architected/ai/
- https://learn.microsoft.com/en-us/azure/well-architected/

- [ ] **Step 3: Write dimensions/01-well-architected.md**

Create `dimensions/01-well-architected.md` following this structure:

```markdown
# Dimension 01: Well-Architected Philosophy

**Last updated:** 2026-04-10
**AWS WAF version:** [from docs]
**Azure WAF version:** [from docs]

## What does AWS recommend?

[3-5 paragraphs covering:]
- The 6-pillar structure and what it optimizes for
- The question-based review methodology: AWS doesn't tell you what to do, it asks whether you've considered specific concerns
- The ML Lens: how it extends the base framework for ML workloads (cite 2-3 specific example questions)
- The GenAI Lens: how it handles foundation models, RAG, responsible AI (cite 2-3 specific example questions)
- The cultural context: OpsReview cadence, the idea that architecture review is an ongoing practice, not a one-time gate

[Link to sources at the bottom of this section]

## What does Azure recommend?

[3-5 paragraphs covering:]
- The 5-pillar structure and how it differs from AWS's 6
- The assessment-driven methodology: Azure provides recommendations with severity and impact ratings
- AI workload guidance: how it integrates into the main framework rather than living as a separate lens (cite 2-3 specific recommendations)
- Azure Advisor integration: automated checks that surface recommendations without manual assessment
- The enterprise context: designed for organizations that want prescriptive guidance they can hand to teams

[Link to sources at the bottom of this section]

## Where do they agree

[1-2 paragraphs identifying specific areas of convergence. Examples might include:]
- Both emphasize cost optimization as a first-class concern for AI workloads
- Both treat security and data governance as non-negotiable for production ML/GenAI
- Both recommend monitoring model performance and drift
- When both clouds say the same thing, that's a strong signal the pattern is sound regardless of platform

## Where do they diverge, and why

[2-3 paragraphs on the most significant differences. This is the most valuable section. Focus on differences that lead to different architectural decisions:]
- Question-based vs. prescriptive: AWS asks "have you considered...?" while Azure says "you should..."
  - This reflects different assumptions about the audience. AWS assumes the team has context and needs prompts to think. Azure assumes the team wants actionable recommendations.
- Separate lenses vs. integrated guidance: AWS publishes ML and GenAI as separate lenses. Azure integrates AI guidance into the main framework.
  - What this means in practice: on AWS, you run a separate review for AI workloads. On Azure, AI considerations are part of every review.
- [Any other significant divergences found during research]

## Honest take: genuine value vs. managed wrapper

[2-3 paragraphs. This is where the governance honesty lives:]
- The frameworks themselves are free and public. You can read them without using either cloud. The value isn't the framework text.
- The value is the tooling: AWS Well-Architected Tool gives you a structured review flow with tracked improvements. Azure Advisor gives you automated checks against your running infrastructure.
- But here's the thing: if you're not using the Well-Architected Tool or Azure Advisor, you're just reading a PDF. You could get similar structured thinking from the DORA framework, Google's SRE book, or your own architecture review template.
- Where the cloud tools genuinely add value: they connect the review to your actual infrastructure. AWS Well-Architected Tool can pull data from your account. Azure Advisor scans your running resources. That connection between guidance and reality is hard to replicate with open-source tools.

## Balance point

| Your context | Recommendation |
|---|---|
| Solo developer or small team, no compliance requirements | Read both frameworks for the thinking. Don't bother with the review tools. |
| Growing team, starting to care about operational maturity | Pick the framework that matches your cloud. Use the review tool quarterly. |
| Enterprise with compliance and audit requirements | The review tools earn their value here. Tracked assessments and improvement plans become audit evidence. |
| Multi-cloud organization | Read both. Use the review tool for each cloud's workloads. Consider building a unified checklist that draws from both (planned for a future update). |

## Sources

- [AWS Well-Architected Framework](link)
- [AWS ML Lens](link)
- [AWS GenAI Lens](link)
- [Azure Well-Architected Framework](link)
- [Azure AI Workload Guidance](link)
- [Azure Advisor](link)
```

Fill all sections with actual content from Steps 1-2. The structure above shows the format and tone. The actual analysis must come from the research.

- [ ] **Step 4: Quality check**

Verify:
- All six sections are present and filled with real content
- Every factual claim cites a source (linked at bottom)
- The "agree" and "diverge" sections contain specific examples, not vague statements
- The "honest take" section makes concrete claims about where cloud tools add value
- The balance point table gives actionable recommendations per context
- No em-dash chains. Short sentences. Personal tone.
- The document is scannable (tables, bullets, short paragraphs)

- [ ] **Step 5: Commit**

```bash
git add dimensions/01-well-architected.md
git commit -m "add dimension 01: well-architected philosophy comparison"
```

---

### Task 4: Dimension 03 — GenAI Architecture Patterns

**Files:**
- Create: `dimensions/03-genai-patterns.md`

This is the highest-value dimension for the current moment. It compares how each cloud recommends building GenAI workloads: RAG, agents, fine-tuning, guardrails.

- [ ] **Step 1: Research AWS GenAI patterns**

Read Bedrock documentation and AWS reference architectures for:
- **RAG:** Bedrock Knowledge Bases. How it works, what it manages, what you configure. What's the recommended architecture?
- **Agents:** Bedrock Agents. How they work, what orchestration they provide, how they compare to building your own with LangGraph.
- **Fine-tuning:** Bedrock Custom Models. What's supported, what's the workflow.
- **Guardrails:** Bedrock Guardrails. Content filtering, PII detection, topic blocking. What's configurable.
- **Orchestration:** How AWS recommends connecting these pieces (Step Functions, Lambda, custom code).

For each: note what's configurable, what's opinionated, and what the open-source equivalent would be.

Sources:
- https://docs.aws.amazon.com/bedrock/latest/userguide/
- AWS GenAI reference architectures
- AWS Well-Architected GenAI Lens (for recommended patterns)

- [ ] **Step 2: Research Azure GenAI patterns**

Read Azure OpenAI and AI Studio documentation for:
- **RAG:** Azure AI Search + "On Your Data." How it works, what it manages, the integrated path vs. custom.
- **Agents:** Azure AI Agent Service. How it works, what orchestration it provides.
- **Fine-tuning:** Azure OpenAI Fine-tuning. What's supported, what's the workflow.
- **Guardrails:** Azure AI Content Safety. Content filtering, prompt shields, groundedness detection.
- **Orchestration:** Prompt Flow, Semantic Kernel. How Azure recommends connecting these pieces.

For each: note what's configurable, what's opinionated, and what the open-source equivalent would be.

Sources:
- https://learn.microsoft.com/en-us/azure/ai-services/openai/
- https://learn.microsoft.com/en-us/azure/ai-studio/
- Azure Architecture Center AI reference architectures

- [ ] **Step 3: Research open-source equivalents**

For each pattern, identify the open-source baseline:
- **RAG:** LangChain/LlamaIndex + Pinecone/Weaviate/Chroma + any LLM API
- **Agents:** LangGraph, CrewAI, AutoGen
- **Fine-tuning:** Direct API fine-tuning (Anthropic, OpenAI), or open-source with Hugging Face + custom compute
- **Guardrails:** Guardrails AI, NeMo Guardrails, custom prompt engineering
- **Orchestration:** LangGraph, custom Python, Prefect/Airflow for pipelines

This establishes the baseline for the "genuine value vs. managed wrapper" analysis.

- [ ] **Step 4: Write dimensions/03-genai-patterns.md**

Create `dimensions/03-genai-patterns.md` following this structure:

```markdown
# Dimension 03: GenAI Architecture Patterns

**Last updated:** 2026-04-10
**Bedrock version/features noted:** [from docs]
**Azure OpenAI version/features noted:** [from docs]

## What does AWS recommend?

[Organized by pattern, not as a wall of text:]

### RAG
[2-3 paragraphs on Bedrock Knowledge Bases. How it works. What it manages (ingestion, chunking, embedding, retrieval). What you configure. The recommended architecture from the GenAI Lens.]

### Agents
[2-3 paragraphs on Bedrock Agents. Orchestration model. How it handles tool use, memory, multi-step reasoning.]

### Fine-tuning
[1-2 paragraphs on Bedrock Custom Models. Supported models. The workflow.]

### Guardrails
[2-3 paragraphs on Bedrock Guardrails. Content filtering, PII detection, topic blocking, denied topics. How configurable it is.]

### Orchestration
[1-2 paragraphs on how AWS recommends connecting these. Step Functions for pipelines. Lambda for glue. Custom code for flexibility.]

[Source links]

## What does Azure recommend?

[Same sub-pattern structure:]

### RAG
[2-3 paragraphs on Azure AI Search + On Your Data. The integrated path through AI Studio. What it manages vs. what you build.]

### Agents
[2-3 paragraphs on Azure AI Agent Service. How it works. Semantic Kernel integration.]

### Fine-tuning
[1-2 paragraphs on Azure OpenAI Fine-tuning. Supported models. The workflow.]

### Guardrails
[2-3 paragraphs on Azure AI Content Safety. Content filtering, prompt shields, groundedness detection. Built-in vs. configurable.]

### Orchestration
[1-2 paragraphs on Prompt Flow and Semantic Kernel. How Azure recommends connecting these.]

[Source links]

## Where do they agree

[1-2 paragraphs. Both clouds converge on certain patterns for GenAI. Identify them. Example: both recommend retrieval-augmented generation over fine-tuning for most knowledge-grounding use cases. Both emphasize content safety as a requirement, not an option.]

## Where do they diverge, and why

[2-3 paragraphs on the most significant architectural differences:]
- AWS offers RAG as composable components (you pick the vector store, the embedding model, the retrieval strategy). Azure offers RAG as an integrated feature ("On Your Data" handles it).
- AWS Guardrails are a standalone feature you attach to any Bedrock call. Azure Content Safety is more deeply integrated into the platform.
- Orchestration philosophy: AWS says "use Step Functions or write code." Azure says "use Prompt Flow or Semantic Kernel."
- [Other divergences found during research]

## Honest take: genuine value vs. managed wrapper

[This section is the heart of the document. For each pattern, answer: what does the cloud add over open-source?]

| Pattern | Cloud version | Open-source equivalent | What the cloud actually adds | Is it worth it? |
|---|---|---|---|---|
| RAG | Bedrock Knowledge Bases / Azure AI Search | LangChain + Pinecone | Managed ingestion, chunking, sync. If you're not using the managed pipeline, it's just a more expensive vector search. | Worth it if you want managed data ingestion. Not worth it if you're building custom retrieval. |
| Agents | Bedrock Agents / Azure AI Agent Service | LangGraph, CrewAI | Integrated logging, IAM/AD permissions per agent, managed state. Less flexible than LangGraph. | Worth it if you need audit trails and access control per agent. Not worth it if you need complex orchestration patterns. |
| Fine-tuning | Bedrock Custom Models / Azure OpenAI FT | Direct API fine-tuning | Managed compute, data governance (data stays in your cloud account). | Worth it if data residency matters. Otherwise, direct API fine-tuning is simpler. |
| Guardrails | Bedrock Guardrails / Azure Content Safety | Guardrails AI, NeMo, custom | **This is where cloud genuinely adds the most value.** Production-grade content filtering with managed updates, integrated into every API call. Building this well from scratch is a real project. | Worth it for almost any production workload. |
| Orchestration | Step Functions, Prompt Flow | LangGraph, Prefect | Managed execution, retry logic, visual debugging. But less flexible for complex agent patterns. | Depends on complexity. Simple chains: cloud is fine. Complex agents: open-source gives more control. |

## Balance point

| Your context | Recommendation |
|---|---|
| Building a prototype or POC | Direct API + LangGraph/LangChain. Don't add cloud overhead to something that might get thrown away. |
| Single-model, simple RAG app | Cloud platform is fine but you're not using much of it. Direct API + a vector DB might be simpler. |
| Production app with compliance needs | Cloud platform earns its cost here. Guardrails, logging, IAM/AD integration, audit trails. |
| Complex agent system with multi-step reasoning | Use LangGraph for orchestration. You can still run it on top of Bedrock/Azure OpenAI for the governance layer. |
| Multi-model strategy (different LLMs for different tasks) | Bedrock's model garden helps here. Azure is more OpenAI-centric. Or go direct-to-API for maximum flexibility. |

## Sources

- [Bedrock Knowledge Bases](link)
- [Bedrock Agents](link)
- [Bedrock Guardrails](link)
- [Azure AI Search](link)
- [Azure AI Agent Service](link)
- [Azure AI Content Safety](link)
- [LangGraph](link)
- [AWS GenAI Lens](link)
- [Azure AI reference architectures](link)
```

Fill all sections with actual content from Steps 1-3. The structure above shows the format, tone, and level of specificity expected. The actual analysis must come from the research.

- [ ] **Step 5: Quality check**

Verify:
- All six template sections are present and filled
- The sub-pattern structure (RAG, Agents, Fine-tuning, Guardrails, Orchestration) is consistent between AWS and Azure sections
- The "honest take" table has concrete assessments, not hedging
- Every "is it worth it?" answer specifies for whom and under what conditions
- Open-source equivalents are named specifically (not "open-source tools" but "LangGraph, CrewAI")
- Source links are present for every factual claim
- No em-dash chains. Short sentences. Scannable.

- [ ] **Step 6: Commit**

```bash
git add dimensions/03-genai-patterns.md
git commit -m "add dimension 03: GenAI architecture patterns comparison"
```

---

### Task 5: Decision Guide

**Files:**
- Create: `guide/decision-guide.md`

This is the entry point for readers. It walks through the three-question decision flow and links to dimension docs for depth.

- [ ] **Step 1: Write guide/decision-guide.md**

Create `guide/decision-guide.md`:

```markdown
# Decision Guide: Do You Need a Cloud AI Platform?

**Last updated:** 2026-04-10

This guide walks through three questions, in order. Each one narrows the decision. If you want the deep analysis behind any answer, follow the links to the dimension docs.

---

## Question 1: Do I need a cloud AI platform at all?

The cloud AI platforms (AWS Bedrock, Azure OpenAI Service) wrap model APIs with enterprise governance: identity management, network isolation, guardrails, monitoring, cost controls, compliance.

If you're not using that governance, you're paying a cloud tax on top of what a direct API call already does.

### Use a cloud AI platform if:

- Your organization has compliance requirements (data residency, audit trails, regulated industry)
- Multiple teams will share the AI infrastructure (you need centralized identity and access control)
- You need production-grade guardrails without building them yourself
- Your operations team needs the AI system integrated into existing cloud monitoring (CloudWatch, Azure Monitor)

### Go direct-to-API (Claude API, OpenAI API) + open-source if:

- You're prototyping or building a POC
- You're a small team without compliance overhead
- You need maximum flexibility (latest model features, multi-model strategy, custom orchestration)
- You have the engineering capacity to build your own monitoring and guardrails

### The honest middle ground:

You can use the cloud platform for governance (IAM/AD, network isolation, content safety) while using open-source tools for orchestration (LangGraph on top of Bedrock). The layers are separable. Don't assume it's all-or-nothing.

For more depth: see [GenAI Architecture Patterns](../dimensions/03-genai-patterns.md), especially the "Honest take" section.

---

## Question 2: Which cloud's philosophy fits your context?

If you've decided a cloud AI platform makes sense, the next question is which approach fits.

| | AWS | Azure |
|---|---|---|
| Philosophy | Building blocks. You compose. | Integrated platform. Guided workflows. |
| AI identity | Bedrock + SageMaker: broad model garden, composable services | Azure OpenAI + AI Studio: OpenAI-first, integrated environment |
| Governance style | IAM-native, VPC-native, you configure what you need | Azure AD-native, more defaults turned on, more prescriptive |
| Architectural guidance | Well-Architected ML Lens + GenAI Lens: asks questions, you decide | Well-Architected AI guidance: gives recommendations, you follow |
| Best fit for | Teams that want control and are willing to assemble | Teams that want a guided path and faster time to first result |

### Decision factors:

**Existing cloud footprint matters most.** If your organization is already on AWS, Bedrock integrates with your existing IAM, VPC, and monitoring. Same for Azure. Switching clouds for AI alone rarely makes sense.

**Team composition matters.** If your team has strong infrastructure skills and wants flexibility, AWS's composable approach works. If your team wants to focus on the AI application and not the plumbing, Azure's integrated path removes friction.

**Model strategy matters.** If you want broad model access (Claude, Llama, Mistral, Cohere), Bedrock's model garden is wider. If your primary model is GPT, Azure's OpenAI partnership gives you tighter integration and faster feature access.

For more depth: see [Well-Architected Philosophy](../dimensions/01-well-architected.md).

---

## Question 3: What governance should I actually turn on?

Choosing a cloud platform is not the same as using its governance. This is the most common gap: teams adopt Bedrock or Azure OpenAI but skip the governance features that justify the platform in the first place.

### Minimum governance for production workloads:

| Feature | AWS | Azure | Why it matters |
|---|---|---|---|
| Identity and access | IAM roles per model/resource | Azure AD RBAC | Who can invoke which model? You need an answer to this. |
| Network isolation | VPC endpoints for Bedrock | Private endpoints for Azure OpenAI | Keep model traffic off the public internet. |
| Content safety | Bedrock Guardrails | Azure AI Content Safety | Filter harmful content, detect PII, block off-topic use. |
| Monitoring | CloudWatch metrics + CloudTrail logs | Azure Monitor + App Insights | Know when your AI system is failing before your users do. |
| Cost controls | AWS Budgets + model invocation quotas | Azure Cost Management + PTU provisioning | AI costs can spike fast. Set guardrails on spend. |

### The test:

If you're on a cloud AI platform and haven't configured at least identity, network isolation, and content safety, ask yourself: what am I getting from this platform that I wouldn't get from a direct API call?

If the answer is "not much," either turn on the governance or reconsider the platform choice.
```

- [ ] **Step 2: Quality check**

Verify:
- The three questions flow logically (each narrows the decision)
- Links to dimension docs are correct relative paths
- Recommendations are specific and context-dependent (not "it depends")
- The tone is direct and practical
- The "honest middle ground" and "the test" sections add the governance honesty angle
- No marketing language. No fluff.

- [ ] **Step 3: Commit**

```bash
git add guide/decision-guide.md
git commit -m "add decision guide: three-question flow for cloud AI platform choice"
```

---

### Task 6: Medium Article Draft

**Files:**
- Create: `drafts/medium-article.md`

The article distills the thesis and links to the repo. It's not a copy of the README. It's a narrative that makes the argument, uses 2-3 concrete examples, and points readers to the repo for depth.

- [ ] **Step 1: Write drafts/medium-article.md**

Create `drafts/medium-article.md`:

```markdown
# Beyond Service Mapping: How AWS and Azure Actually Think About AI Architecture

[Working title. Finalize before publishing.]

---

## The hook (2-3 paragraphs)

[Open with the problem: most AWS-vs-Azure content for AI is shallow service mapping. SageMaker = Azure ML. Bedrock = Azure OpenAI. Done. This tells you nothing useful.

The real question isn't which cloud has which service. It's how each cloud thinks about building AI systems. And more importantly: when does the cloud platform add genuine value over what you could build yourself with a direct API call and open-source tools?]

## The thesis (1-2 paragraphs)

[AWS and Azure both wrap open-source AI capabilities with enterprise governance. The value of each platform is proportional to the governance you actually adopt. If you're on Bedrock but haven't configured Guardrails or IAM, you're paying a cloud tax for nothing.

This article summarizes a longer comparison (link to repo) that maps what each cloud recommends, where they agree, where they diverge, and when the enterprise wrapper is worth it.]

## Example 1: How they think about architecture review (3-4 paragraphs)

[Use the Well-Architected comparison as the first concrete example.
- AWS: question-based ("Have you considered...?"). Assumes you have context, gives you prompts to think.
- Azure: recommendation-based ("You should..."). Assumes you want actionable guidance.
- What this means in practice: AWS's approach works better for experienced teams. Azure's works better for teams that want guardrails on their decisions.
- Link to the full dimension doc for depth.]

## Example 2: RAG architecture, honestly (3-4 paragraphs)

[Use the RAG pattern as the second example. This is where the governance honesty is most concrete.
- Both clouds offer managed RAG. Bedrock Knowledge Bases. Azure AI Search + On Your Data.
- Both are managed versions of what LangChain + Pinecone already do.
- The cloud versions add: managed ingestion, monitoring, IAM/AD integration.
- The honest question: are you using the managed ingestion and monitoring? If not, you have a more expensive, less flexible RAG pipeline.
- But: Guardrails/Content Safety on top of RAG is where cloud genuinely earns its cost. Building production-grade content filtering from scratch is hard.
- Link to the full dimension doc for depth.]

## The balance point (2-3 paragraphs)

[Not every team needs the cloud platform. Lay out the spectrum:
- Prototype/POC: direct API + open-source. Don't over-engineer.
- Small team, no compliance: probably direct API. Maybe cloud for guardrails only.
- Enterprise with compliance: cloud platform earns its cost. But turn on the governance.
- The test: if you're on a cloud AI platform and can't name three governance features you're actively using, reconsider why you're there.]

## Closing (1-2 paragraphs)

[Point to the repo. Explain it's a living resource. Invite readers to check the full analysis for any dimension they care about. Note it's an ongoing project and link to the GitHub repo.]

---

**Repo link:** [github.com/btriani/aws-azure-ai-architecture-compared](link)
```

This is a structural draft with writing directions for each section. The final article should be written in the author's voice based on these directions. Total target length: 1200-1800 words.

- [ ] **Step 2: Quality check**

Verify:
- The article makes one clear argument (governance value, not service mapping)
- It uses exactly 2 concrete examples (Well-Architected + RAG) to ground the argument
- It links to the repo at least twice (after each example and at the end)
- The tone is personal, not generated-sounding
- It doesn't try to cover everything. It makes the reader want to check the repo.
- Target length: 1200-1800 words when fully written

- [ ] **Step 3: Commit**

```bash
git add drafts/medium-article.md
git commit -m "add medium article draft: structural outline with writing directions"
```

---

### Task 7: Final README Polish and Review

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Update README links**

Verify all links in the README point to files that now exist. Update the Status table:

```markdown
## Status

This is a living resource. Current coverage:

| Dimension | Status |
|---|---|
| Well-Architected Philosophy | Complete |
| AI/ML Service Model | Planned |
| GenAI Architecture Patterns | Complete |
| MLOps / GenAIOps | Planned |
| Operating Model | Planned |
| Reference Architecture Style | Planned |
```

- [ ] **Step 2: Full repo review**

Read through every file in order:
1. README.md (entry point, navigation)
2. guide/decision-guide.md (the journey)
3. dimensions/01-well-architected.md (deep dive)
4. dimensions/03-genai-patterns.md (deep dive)
5. tables/framework-comparison.md (quick reference)

Check:
- Links between files work (relative paths are correct)
- No contradictions between files (decision guide claims match dimension doc analysis)
- Tone is consistent across all files (direct, scannable, personal)
- Every factual claim has a source link
- No placeholders, TBDs, or empty sections remain

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "finalize README: update links and status for MVP"
```

- [ ] **Step 4: Tag the MVP**

```bash
git tag -a v0.1.0 -m "MVP: Well-Architected + GenAI Patterns dimensions, decision guide, framework table"
```
