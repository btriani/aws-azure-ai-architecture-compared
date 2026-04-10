# Beyond Service Mapping: How AWS and Azure Actually Think About AI Architecture

> Working title. Finalize before publishing.

---

## The problem (2-3 paragraphs)

Most AWS-vs-Azure content for AI is shallow service mapping. SageMaker = Azure ML. Bedrock = Azure OpenAI Service. Done. This tells you which button to click on which console, but nothing about which patterns to follow or why.

The real question is not which cloud has which service. It is how each cloud thinks about building AI systems. And more importantly: when does the enterprise cloud platform add genuine value over what you could build yourself with a direct API call and open-source tools like LangGraph or LangChain?

I spent [time period] going deep on both clouds' architecture frameworks, GenAI service documentation, and reference architectures. This article is the distilled version. The full analysis, with source links and structured comparison tables, lives in the GitHub repo: [aws-azure-ai-architecture-compared](https://github.com/btriani/aws-azure-ai-architecture-compared).

## The thesis (1-2 paragraphs)

AWS and Azure both wrap open-source AI capabilities with enterprise governance: identity management, network isolation, guardrails, monitoring, cost controls, compliance certifications. The value of each platform is proportional to the governance you actually adopt.

That last sentence is the key. Choosing Bedrock or Azure OpenAI Service does not automatically give you enterprise governance. It gives you the option. If you are on a cloud AI platform and have not configured identity controls, network isolation, or content safety, you are paying a cloud tax on top of what a direct API call already does.

## Example 1: How they think about architecture review (3-4 paragraphs)

AWS and Azure both publish Well-Architected Frameworks with AI-specific guidance. The frameworks address the same concerns (security, reliability, cost, operations) but approach them differently.

AWS uses a question-based model. The GenAI Lens asks things like: "How do you protect generative AI endpoints?" and "How do you select cost-optimized models?" The implicit message: you know your system, we give you the checklist, you figure out the answer through discussion. Reviews are explicitly described as "not an audit."

Azure uses a prescriptive model. The AI workload guidance says things like: "Use PaaS over self-hosted options" and "Implement RBAC and ABAC for both control and data planes." The implicit message: we have seen enough systems to know what works, here is what to do. Azure also introduces five AI-native design principles (experimental mindset, responsible design, explainability, model decay, adaptability) that cut across the base pillars.

Neither approach is wrong. AWS's works better for experienced teams who benefit from structured reflection. Azure's works better for teams that want concrete guidance they can act on immediately. The choice tells you something about how each cloud sees its audience. For the full pillar-by-pillar comparison: [Well-Architected Philosophy](link to dimension doc).

## Example 2: RAG architecture, honestly (3-4 paragraphs)

Both clouds offer managed RAG services. AWS has Bedrock Knowledge Bases. Azure has AI Search with the "On Your Data" feature. Both handle the same pipeline: ingest documents, chunk them, generate embeddings, store vectors, retrieve relevant chunks, augment the prompt, generate a response.

Here is the honest take: a LangChain pipeline with Pinecone or pgvector does the same retrieval job. The cloud managed service is convenient (one fewer thing to operate) but the retrieval quality depends on chunking strategy, embedding model choice, and prompt design. None of which the cloud makes better by default.

Where the cloud RAG services genuinely help: access control and multi-source ingestion. Azure AI Search supports document-level security trimming. Bedrock Knowledge Bases integrates with IAM for data source access and connects to SharePoint, Confluence, and databases without custom connectors. If your data is already in S3 or Blob Storage and your access control requirements are simple, the open-source path is equally viable.

Now compare that to guardrails. Bedrock Guardrails and Azure AI Content Safety provide audit trails, compliance reporting, PII detection calibrated for regulatory frameworks, and specialized capabilities like protected material detection (Azure) and automated reasoning checks (AWS). Building this from scratch with Guardrails AI or NeMo is a real project, and you still will not get the audit trail or compliance certifications. This is where the cloud platform earns its cost. For the full pattern-by-pattern breakdown: [GenAI Architecture Patterns](link to dimension doc).

## The balance point (2-3 paragraphs)

Not every team needs the cloud AI platform. Here is the spectrum:

- **Prototype or POC:** Direct API + open-source. Do not add cloud overhead to something that might get thrown away.
- **Small team, no compliance:** Probably direct API. Consider cloud guardrails if you are shipping to real users.
- **Production with compliance needs:** Cloud platform earns its cost. Guardrails, logging, IAM/Entra integration, audit trails. But turn on the governance.
- **The test:** If you are on a cloud AI platform and cannot name three governance features you are actively using, reconsider why you are there.

The strongest position is not all-cloud or all-open-source. It is using the cloud for governance (identity, network isolation, content safety, monitoring) while using open-source tools for orchestration (LangGraph on top of Bedrock). The layers are separable. Use each where it adds the most value.

## Closing (1-2 paragraphs)

The full analysis lives in the repo, with source links to every AWS and Azure document referenced. It is a living resource, not a snapshot. Start with the [Decision Guide](link) if you want the practical flow. Jump to a specific dimension if you want depth.

If this framing resonated or if you disagree with any of it, I would like to hear about it. The whole point is to think honestly about these platforms, not to market them.

---

**Repo:** [github.com/btriani/aws-azure-ai-architecture-compared](https://github.com/btriani/aws-azure-ai-architecture-compared)

**Target length when fully written:** 1200-1800 words

**Notes for final version:**
- Replace [time period] with actual time spent
- Replace link placeholders with actual GitHub URLs once repo is published
- Review tone for personal voice before publishing
- Consider adding a header image or diagram
