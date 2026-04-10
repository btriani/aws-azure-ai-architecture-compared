# Dimension 01: Well-Architected Philosophy

**Last updated:** 2026-04-10
**AWS WAF version:** November 6, 2024 (base framework); November 19, 2025 (ML Lens and GenAI Lens)
**Azure WAF version:** March 2026 revision (base framework); April 2026 (AI workload guidance)

---

## Section 1: What does AWS recommend?

AWS structures architectural thinking around six pillars: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, and Sustainability. The first five address the qualities most teams already care about. The sixth, Sustainability, was elevated to a full pillar in late 2021. This is a deliberate choice. AWS treats environmental impact as an architectural concern on the same level as cost or security, not as a nice-to-have appendix.

The review methodology is question-based and explicitly conversational. AWS describes the review process as "a constructive conversation about architectural decisions, and is not an audit mechanism." Reviews are meant to be lightweight (hours, not days), blame-free, and run by the team that built the architecture. For cross-team reviews, AWS recommends informal conversations followed by one or two focused meetings on ambiguities. The framework distinguishes between "two-way door" decisions (reversible, review lightly) and "one-way door" decisions (hard to reverse, inspect more rigorously). The output is a prioritized list of high-risk issues with an improvement plan, not a pass/fail grade. AWS recommends near-continuous review as architectures evolve, with formal checkpoints at early design, before go-live, and after significant changes. ([Source: AWS WAF Review Process](https://docs.aws.amazon.com/wellarchitected/latest/framework/the-review-process.html))

The **Machine Learning Lens** (November 2025) extends the base framework for ML workloads. It addresses the fundamental difference between traditional software (deterministic, step-by-step instructions) and ML systems (algorithms that learn from data through iterative cycles). The lens maps best practices to all six pillars and can be imported into the AWS Well-Architected Tool as a custom lens for structured review. Key themes include high-quality input data, continuous monitoring to detect accuracy and performance issues, model retraining with refined datasets, and responsible AI practices. The ML Lens asks questions like: *How do you ensure high-quality input data for your ML models?* and *How do you continuously monitor for accuracy and performance issues?* ([Source: AWS ML Lens](https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html))

The **Generative AI Lens** (November 2025) handles foundation models, RAG architectures, prompt engineering, and AI agents. It covers the full lifecycle: scoping, model selection, customization, development, deployment, and continuous improvement. The lens is organized by pillar and asks specific questions per focus area. Examples from the documentation:

- **Operational Excellence:** "How do you achieve consistent model output quality?" and "How do you maintain traceability across the AI lifecycle?"
- **Security:** "How do you protect generative AI endpoints?" and "How do you remediate model poisoning risks?"
- **Cost Optimization:** "How do you select cost-optimized models?" and "How do you engineer prompts for cost efficiency?"

The GenAI Lens also addresses responsible AI through a shared-responsibility model among model producers, providers, and consumers. It covers harmful output prevention, excessive AI agency, and prompt security. ([Source: AWS GenAI Lens](https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html))

The cultural context matters. AWS positions the review as an ongoing practice, not a compliance gate. The framework documentation emphasizes that architecture evolves with new features and technology changes, requiring "continuous hygiene practices." The Well-Architected Tool tracks milestones over time so teams can measure progress. Reviews can be shared with up to 300 IAM users or across an AWS Organization. The intent is to embed architectural thinking into the team's routine, not to create a bottleneck before deployment.

**Sources:**
- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
- [AWS WAF Review Process](https://docs.aws.amazon.com/wellarchitected/latest/framework/the-review-process.html)
- [AWS Machine Learning Lens](https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html)
- [AWS Generative AI Lens](https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html)

---

## Section 2: What does Azure recommend?

Azure structures its framework around five pillars: Reliability, Security, Cost Optimization, Operational Excellence, and Performance Efficiency. There is no Sustainability pillar. Azure treats sustainability as a workload type with its own design methodology and assessment, developed in partnership with the Green Software Foundation. The practical difference: AWS asks sustainability questions during every architectural review. Azure provides sustainability guidance only when teams explicitly opt into the sustainability workload track.

The methodology is assessment-driven and prescriptive. Azure provides a web-based Well-Architected Review tool where teams answer questions tied to pillar checklists. The output is a scored result with prioritized recommendations, each linked to specific Microsoft Learn documentation. Where AWS asks "Have you considered X?" and waits for a conversation, Azure says "Do X, and here's the severity level." Azure's AI workload design principles page, for example, provides tables where each principle is paired with specific considerations and trade-off callouts. The recommendations come with explicit architectural guidance rather than open-ended questions. ([Source: Azure WAF](https://learn.microsoft.com/en-us/azure/well-architected/))

The **AI workload guidance** is integrated into the main framework as a workload type, not a separate lens. It covers both discriminative (traditional ML) and generative AI in a single body of guidance. The structure includes a design methodology, five AI-specific design principles, technical design areas (application design, application platform, training data, grounding data, data platform), and operational design areas (operations, MLOps/GenAIOps, testing, responsible AI). The five AI design principles are genuinely AI-native:

1. **Design with an experimental mindset** -- achieve relevancy through iterative, statistically driven processes
2. **Design responsibly** -- embed ethical functionality and prevent unacceptable behaviors like manipulation, content toxicity, and fabricated responses
3. **Design for explainability** -- trace the origins of data, inference processes, and the journey of data from source to serve layer
4. **Stay ahead of model decay** -- detect and address quality deterioration through automated monitoring and user feedback
5. **Design for adaptability** -- recognize that what you build today might become obsolete quickly

These are not restatements of the base pillars. They are specific to the nature of AI systems. ([Source: Azure AI Design Principles](https://learn.microsoft.com/en-us/azure/well-architected/ai/design-principles))

Specific recommendations from the AI guidance include: "Use platform as a service (PaaS) over self-hosted options to simplify design and automate workflow orchestration" (Operational Excellence), "Implement role-based access control (RBAC) and/or attribute-based access control (ABAC) for both control and data planes" (Security), and "Prefer elastic compute options for orchestration tools to minimize utilization costs, because they're always-on. Avoid serverless compute for full-time operations because it can escalate costs" (Cost Optimization). These are concrete, opinionated recommendations, not questions to discuss. ([Source: Azure AI Design Principles](https://learn.microsoft.com/en-us/azure/well-architected/ai/design-principles); [Source: Azure AI Application Design](https://learn.microsoft.com/en-us/azure/well-architected/ai/application-design))

**Azure Advisor** adds an automated layer that has no direct equivalent in the AWS Well-Architected ecosystem. Advisor is a digital cloud assistant that analyzes resource configuration and usage telemetry continuously and proactively. It provides actionable recommendations across five categories that map directly to the WAF pillars: Reliability, Security, Performance, Cost, and Operational Excellence. Recommendations are personalized to the actual resources deployed. Teams get a baseline of architectural recommendations passively, without initiating a review. The Advisor Score aggregates recommendations into a single number. This means Azure teams discover some architectural issues automatically, while AWS teams must actively initiate a review to surface them. ([Source: Azure Advisor](https://learn.microsoft.com/en-us/azure/advisor/advisor-overview))

**Sources:**
- [Azure Well-Architected Framework](https://learn.microsoft.com/en-us/azure/well-architected/)
- [Azure AI Workload Guidance](https://learn.microsoft.com/en-us/azure/well-architected/ai/)
- [Azure AI Design Principles](https://learn.microsoft.com/en-us/azure/well-architected/ai/design-principles)
- [Azure AI Design Methodology](https://learn.microsoft.com/en-us/azure/well-architected/ai/design-methodology)
- [Azure Advisor Overview](https://learn.microsoft.com/en-us/azure/advisor/advisor-overview)

---

## Section 3: Where do they agree

Both frameworks treat cost optimization as a first-class concern for AI workloads. This is notable because AI costs can escalate faster and less predictably than traditional compute costs. Both explicitly address model selection as a cost lever, monitoring resource utilization to avoid waste, and choosing the right compute tier for the task at hand. Both also treat security and data governance as non-negotiable for production AI. AWS asks "How do you protect generative AI endpoints?" Azure says "Require authentication for all inferencing endpoints, including system-to-system calls. Avoid anonymous endpoints." Different phrasing, same floor: you do not ship an unprotected model endpoint to production.

Both frameworks also converge on monitoring model performance and drift as ongoing operational requirements. AWS emphasizes continuous monitoring to detect accuracy and performance issues, with model retraining as data evolves. Azure frames this through the "Stay ahead of model decay" design principle: "The quality of AI model outputs can deteriorate over time without any changes to the code." Both land in the same place: you need automated detection of quality degradation, and you need a process to respond to it. When both clouds independently arrive at the same architectural recommendation, that is a strong signal the pattern is sound. These are not marketing positions. They are hard-won operational lessons from running AI at scale.

---

## Section 4: Where do they diverge, and why

**Question-based vs. prescriptive approach.** This is the most consequential divergence. AWS asks questions: "How do you achieve consistent model output quality?" "How do you select cost-optimized models?" The implicit message is: you know your system, we provide the checklist, you figure out the answer through discussion. Azure provides directives: "Use PaaS over self-hosted options." "Prefer elastic compute for orchestration tools." "Implement RBAC and ABAC for both control and data planes." The implicit message is: we have seen enough systems to know what works, here is what to do.

Why do they diverge? Different assumptions about audience. AWS's conversational model assumes the team includes experienced architects who benefit from structured reflection. The review is designed to surface architectural context that only the builders know. Azure's prescriptive model assumes many teams want concrete guidance they can act on immediately, especially in enterprise settings where architecture teams may not be embedded in every project. Neither is wrong. But they produce different outcomes. AWS reviews surface team-specific risks that prescriptive guidance might miss. Azure guidance reduces the baseline of architectural mistakes, even when teams lack deep expertise.

**Separate lenses vs. integrated guidance.** AWS splits AI guidance into two parallel documents: the ML Lens for traditional machine learning (classification, regression, clustering, anomaly detection) and the GenAI Lens for foundation models, RAG, and agents. Each maps to all six pillars using the same structural pattern. Azure unifies all AI guidance into a single workload type covering both discriminative and generative AI. Azure also introduces five AI-native design principles (experimental mindset, responsible design, explainability, model decay, adaptability) that cut across pillars. AWS organizes AI principles within the existing pillar taxonomy.

This matters when teams build systems that combine traditional ML and generative AI. A recommendation engine (ML) feeding a generative summary (GenAI) requires consulting two separate AWS lenses. Azure addresses that intersection in one place. However, AWS's lens model lets teams scope reviews precisely. A team running only traditional ML never encounters GenAI guidance. Azure's unified approach means all AI teams see all AI guidance, which can be either comprehensive or noisy depending on the workload.

**Automated vs. human-initiated review.** Azure Advisor runs continuously, analyzing resource configuration and telemetry without human initiation. It surfaces recommendations mapped to WAF pillars. AWS has no equivalent always-on advisor tied to its Well-Architected Framework. AWS Trusted Advisor exists but is a separate service with different scope, and it does not generate Well-Architected review findings. This means Azure teams get a passive safety net: misconfigured resources, underutilized compute, and missing security controls are flagged automatically. AWS teams must actively decide to run a review. The trade-off: AWS's human-driven reviews may surface architectural context and design intent that automated tools cannot detect. Azure's automated approach catches configuration drift that teams might overlook between reviews. The strongest posture uses both -- automated checks for hygiene, human reviews for design judgment.

---

## Section 5: Honest take: genuine value vs. managed wrapper

Both frameworks are free and public. You can read every page of both without an AWS or Azure account. The architectural thinking in them is genuinely valuable. If you read nothing else, read the GenAI Lens and the Azure AI design principles page. They capture real lessons about building AI systems at scale: monitor for model decay, protect endpoints, treat cost as a design constraint, plan for the models you use today being obsolete tomorrow. This thinking is not proprietary. You can apply it on any cloud or on bare metal.

The real value proposition is the tooling, not the documentation. The AWS Well-Architected Tool provides structured reviews with milestone tracking: you answer questions, get a prioritized improvement plan, track progress over time, and share results across your organization. Azure Advisor provides automated, continuous analysis of your actual deployed resources. The Azure Well-Architected Review provides scored assessments linked to specific documentation. If you are not using these tools, you are reading a PDF. Similar structured thinking exists in the DORA research program, the Google SRE book, the NIST AI Risk Management Framework, and the ISO/IEC 42001 standard for AI management systems. The cloud frameworks are one source among many.

Where the cloud tools genuinely add value: connecting review to actual infrastructure. Azure Advisor can tell you that your GPU compute is underutilized because it can see the telemetry. The AWS WA Tool can track that you resolved a high-risk issue identified in last quarter's review because it stores the milestone. A PDF cannot do either of these things. The governance layer -- the ability to track, measure, and prove that you are following architectural best practices over time -- is where the cloud platform earns its keep. This matters most in regulated industries where "we follow best practices" needs evidence, not just intention. For teams without compliance requirements or audit pressure, the frameworks are useful reading but the tooling is optional.

---

## Section 6: Balance point

| Your context | Recommendation |
|---|---|
| Solo developer or small team, no compliance requirements | Read both frameworks for the thinking. The AWS GenAI Lens and Azure AI design principles are the highest-value pages. Skip the review tools. Your time is better spent building. |
| Growing team, operational maturity matters | Pick the framework matching your primary cloud. Use the review tool quarterly. AWS WA Tool for structured conversations. Azure WAF Review for scored assessments. Track improvement over time. |
| Enterprise with compliance and audit requirements | Review tools earn their value here. Tracked assessments become audit evidence. AWS milestone snapshots show remediation over time. Azure Advisor Score gives a continuous compliance signal. Use both if multi-cloud. |
| Multi-cloud organization | Read both frameworks. Use each cloud's review tool for its respective workloads. Azure Advisor runs automatically; make sure someone reads its output. AWS reviews need to be scheduled; put them on the calendar. Consider building a unified internal checklist that maps to both frameworks (planned for a future update in this repo). |
| Team building its first AI workload | Start with Azure's AI design principles for the five things that make AI workloads different from traditional workloads. Then read the AWS GenAI Lens for specific questions to pressure-test your design. The combination gives you both the "what to think about" and the "have you considered..." perspectives. |

---

## Sources

1. AWS Well-Architected Framework (main): https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
2. AWS Well-Architected Review Process: https://docs.aws.amazon.com/wellarchitected/latest/framework/the-review-process.html
3. AWS Machine Learning Lens: https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html
4. AWS Generative AI Lens: https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html
5. Azure Well-Architected Framework (main): https://learn.microsoft.com/en-us/azure/well-architected/
6. Azure AI Workload Guidance: https://learn.microsoft.com/en-us/azure/well-architected/ai/
7. Azure AI Design Principles: https://learn.microsoft.com/en-us/azure/well-architected/ai/design-principles
8. Azure AI Design Methodology: https://learn.microsoft.com/en-us/azure/well-architected/ai/design-methodology
9. Azure Advisor Overview: https://learn.microsoft.com/en-us/azure/advisor/advisor-overview
10. Azure AI Responsible AI: https://learn.microsoft.com/en-us/azure/well-architected/ai/responsible-ai
11. Azure AI Application Design: https://learn.microsoft.com/en-us/azure/well-architected/ai/application-design
