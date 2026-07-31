# Slide 3 · What We're Covering Today

![Agenda hero image](assets/3-agenda.png){ .hero-image }

Three things. No vague platitudes. Concrete and practical - things you can take back to your team on Monday.

## 1. How to Build and Deploy Safe, Effective AI Agents

This is about architecture and process. Before a line of agent code is written, there are decisions to make: about identity, about permissions, about what the agent is allowed to do and explicitly not allowed to do.

We will cover the **Trustworthy Agent Stack** - a five-layer framework that maps to how we already think about securing systems, extended for the specific challenges of autonomous AI. The layers are:

1. Secure design and threat modelling
2. Identity and least privilege
3. Runtime controls and guardrails
4. Observability and monitoring
5. Governance and compliance

**Why this matters:** Many teams are deploying agents without any security framework at all, or with the assumption that the LLM provider's content filters are a sufficient safeguard. They are not. Content filters are one thin layer of a system that needs defence in depth.

## 2. Security Considerations When Developing AI Agents

This covers the threat landscape: the specific attack classes that target AI agents, the OWASP Top 10 for LLM Applications, and - most critically - what prompt injection really looks like in practice and why it is categorically different from injection attacks against traditional applications.

**Why this matters:** OWASP's LLM threat list is not theoretical. Prompt injection attacks have been demonstrated against production agents at major organisations. An agent with write access to sensitive systems and a prompt injection vulnerability is not an embarrassment - it is a breach. Understanding the threat is the prerequisite for defending against it.

## 3. Maintaining Data and User Privacy in AI Agents

Agents handle data differently from traditional applications. They may access broad context windows, retrieve documents dynamically through RAG, and take actions that affect multiple data stores simultaneously. The privacy implications are significant - especially under frameworks like the EU AI Act, which may classify certain autonomous agents as high-risk AI systems requiring comprehensive logging, explainability, and human oversight.

**Why this matters:** Data minimisation, purpose limitation, and the right to explanation are not optional for regulated industries. If your organisation is subject to GDPR, HIPAA, the EU AI Act, or similar frameworks, these are compliance requirements that must be designed in from the start, not retrofitted after deployment.

## And One More Thing: A Live Demo

If it doesn't run in real life, it doesn't count. We will show a GitHub Copilot coding agent working in a real repository, with every security layer active - identity, code scanning, secret scanning, required review gates, and audit logging - all visible in real time.

<div class="chapter-nav" markdown>
[← Back: Slide 2](slide-02-vibe-shift.md)
[Next: Slide 4 →](slide-04-what-is-an-agent.md)
</div>
