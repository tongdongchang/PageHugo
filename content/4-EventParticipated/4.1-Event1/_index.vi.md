---
title: "Event 1"
date: 2026-05-02
weight: 4
chapter: false
pre: " <b> 3.1. </b> "
---

### Event Purpose
- Introduce modern **Platform Engineering** trends and career pathways.
- Present methods and tools for **DevOps for Generative AI (GenAIOps)** on AWS.
- Share experiences in deploying **multimodal GenAI** at production scale.
- Explore how to leverage **Amazon CloudFront** as a foundation for any workload, from edge to origin.

### Speaker List
The event featured a number of experts from AWS and the tech community, including:
- **Mr. Phuc Dang** – Engineering Manager, GotymeX
- **Mr. Phap Nguyen** – Cloud Engineer, VPBank
- **Mr. Trinh Nguyen** – DevOps Engineer, FCAJ
- Additional guests from the AWS ecosystem.

### Highlights
The morning event was divided into five main sessions:

**1. Building Modern Platform Engineering & Career Pathways (09:00 – 09:45)**
- Explored company culture, internship opportunities, and how to interact with speakers via a Q&A platform.
- Introduced Platform Engineering – the bridge between development and operations that increases release velocity and system reliability.
- Outlined a career path: Software Engineer → Platform Engineer → Architect.

**2. GenAIOps Essential – DevOps for Generative AI Applications (09:45 – 10:15)**
- Reviewed core DevOps principles on AWS and associated learning resources.
- Presented real‑world GenAIOps patterns: using Amazon Bedrock, AgentCore Observability, EKS, and Langfuse to observe and manage the lifecycle of GenAI applications.

**3. Shipping Code in the Agentic Era (10:15 – 10:45)**
- Discussed “how to ship code quickly and safely in the age of AI agents”.
- Introduced tooling: AI code review, autonomous testing, self‑healing pipelines.
- Live demo of a CI/CD pipeline integrated with an AI agent.

**4. Production‑Grade Multimodal GenAI on AWS (11:00 – 11:30)**
- Presented the new AI application stack: multimodal search with Nova Embeddings, GraphRAG for enterprise knowledge.
- Multi‑agent workflow architectures that coordinate complex tasks.
- Ensuring safety and observability for GenAI in production.

**5. From Edge To Origin: CloudFront as Your Foundation (11:30 – 12:00)**
- Showed how Amazon CloudFront can serve as a foundation for all types of workloads, not just CDN.
- Cost‑optimization strategies: caching, compression, region selection.
- Security features: WAF, Shield, OAC; improving reliability and performance.

### What I Learned
**Platform mindset**
- Platform Engineering is not just about tools – it’s a culture of shared responsibility between Dev and Ops.
- An Internal Developer Platform (IDP) reduces cognitive load for developers, letting them focus on code.

**DevOps for AI**
- GenAIOps extends traditional DevOps principles: it requires tracking model output quality, managing prompts, and controlling inference costs.
- Tools like Langfuse and Bedrock Agents enable observability and automation.

**Agentic trend**
- AI agents are no longer just chatbots – they can plan, use tools, and call APIs to accomplish goals.
- Pipelines must be designed with automated rollback and human approval at critical steps.

**Multimodal GenAI architecture**
- Multimodal search (text, images, audio) enriches user experience.
- GraphRAG improves accuracy by combining knowledge graphs with retrieval.

**CloudFront beyond CDN**
- CloudFront can act as a reverse proxy, protect origins, and reduce backend load.
- Edge computing (Lambda@Edge, CloudFront Functions) allows logic to run at the edge.

### Application to my work
- **Music streaming project**: Applied CloudFront as a CDN for the React frontend and as a reverse proxy for the Django backend, improving load speed and security.
- **DevOps**: Integrate GenAIOps practices into future AI features (e.g., ML‑based song recommendations).
- **Platform Engineering**: Create internal development environments with CloudFormation templates so the team can quickly reproduce infrastructure.
- **Learning**: Use Langfuse to observe experimental GenAI models, gaining a deeper understanding of observability.

### Event experience
The event took place in an open and highly interactive atmosphere. The Q&A session allowed me to ask experts directly about career paths and how to get started with Platform Engineering.

The live demos – especially “Shipping Code in the Agentic Era” – gave me a clear picture of how an AI agent can automatically review code and suggest improvements right inside a pull request.

I was particularly impressed by the CloudFront talk: before, I thought of CloudFront only as a CDN, but now I understand it can serve as a foundation for security, cost optimization, and even edge computing.

### Key takeaways
- **Always start from the user’s needs**: Whether it’s GenAI or Platform Engineering, all solutions must solve real business problems.
- **Phased approach**: Don’t adopt every new technology at once. Build a roadmap, run pilots first, then expand.
- **Invest in observability**: Especially for GenAI systems, monitoring and measuring output quality is crucial.
- **Leverage managed services**: AWS offers many services that reduce operational burden and allow teams to focus on business logic.