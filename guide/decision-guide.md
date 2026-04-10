# Decision Guide: Do You Need a Cloud AI Platform?

**Last updated:** 2026-04-10

This guide walks through three questions, in order. Each one narrows the decision. If you want the deep analysis behind any answer, follow the links to the dimension docs.

---

## Question 1: Do I need a cloud AI platform at all?

The cloud AI platforms (AWS Bedrock, Azure OpenAI Service) wrap model APIs with enterprise governance: identity management, network isolation, guardrails, monitoring, cost controls, compliance.

If you are not using that governance, you are paying a cloud tax on top of what a direct API call already does.

### Use a cloud AI platform if:

- Your organization has compliance requirements (data residency, audit trails, regulated industry)
- Multiple teams will share the AI infrastructure (you need centralized identity and access control)
- You need production-grade guardrails without building them yourself
- Your operations team needs the AI system integrated into existing cloud monitoring (CloudWatch, Azure Monitor)

### Go direct-to-API + open-source if:

- You are prototyping or building a POC
- You are a small team without compliance overhead
- You need maximum flexibility (latest model features, multi-model strategy, custom orchestration)
- You have the engineering capacity to build your own monitoring and guardrails

### The honest middle ground

You can use the cloud platform for governance (IAM/Entra ID, network isolation, content safety) while using open-source tools for orchestration (LangGraph on top of Bedrock). The layers are separable. It is not all-or-nothing.

For more depth: see [GenAI Architecture Patterns](../dimensions/03-genai-patterns.md), especially the "Honest take" section.

---

## Question 2: Which cloud's philosophy fits your context?

If you have decided a cloud AI platform makes sense, the next question is which approach fits.

| | AWS | Azure |
|---|---|---|
| Philosophy | Building blocks. You compose. | Integrated platform. Guided workflows. |
| AI identity | Bedrock + SageMaker: broad model garden, composable services | Azure OpenAI + Microsoft Foundry: OpenAI-first, integrated environment |
| Governance style | IAM-native, VPC-native, you configure what you need | Entra ID-native, more defaults turned on, more prescriptive |
| Architectural guidance | Well-Architected ML Lens + GenAI Lens: asks questions, you decide | Well-Architected AI guidance: gives recommendations, you follow |
| Best fit for | Teams that want control and are willing to assemble | Teams that want a guided path and faster time to first result |

### Decision factors

**Existing cloud footprint matters most.** If your organization is already on AWS, Bedrock integrates with your existing IAM, VPC, and monitoring. Same for Azure. Switching clouds for AI alone rarely makes sense.

**Team composition matters.** If your team has strong infrastructure skills and wants flexibility, AWS's composable approach works. If your team wants to focus on the AI application and not the plumbing, Azure's integrated path removes friction.

**Model strategy matters.** If you want broad model access (Claude, Llama, Mistral, Cohere, and others), Bedrock's model catalog is wider. If your primary model is from OpenAI, Azure's partnership gives you tighter integration, more deployment options, and faster feature access for GPT models.

For more depth: see [Well-Architected Philosophy](../dimensions/01-well-architected.md).

---

## Question 3: What governance should you actually turn on?

Choosing a cloud platform is not the same as using its governance. This is the most common gap: teams adopt Bedrock or Azure OpenAI but skip the governance features that justify the platform in the first place.

### Minimum governance for production workloads

| Feature | AWS | Azure | Why it matters |
|---|---|---|---|
| Identity and access | IAM roles per model/resource | Entra ID RBAC | Who can invoke which model? You need an answer to this. |
| Network isolation | VPC endpoints for Bedrock | Private endpoints for Azure OpenAI | Keep model traffic off the public internet. |
| Content safety | Bedrock Guardrails | Azure AI Content Safety | Filter harmful content, detect PII, block off-topic use. |
| Monitoring | CloudWatch metrics + CloudTrail logs | Azure Monitor + Application Insights | Know when your AI system is failing before your users do. |
| Cost controls | AWS Budgets + model invocation quotas | Azure Cost Management + provisioned throughput units | AI costs can spike fast. Set guardrails on spend. |

### The test

If you are on a cloud AI platform and have not configured at least identity, network isolation, and content safety, ask yourself: what am I getting from this platform that I would not get from a direct API call?

If the answer is "not much," either turn on the governance or reconsider the platform choice.
