# Slide 20 · The Only Question That Matters

Before you deploy, answer one question.

![Closing hero image](assets/20-close.png){ .hero-image }

## The Question

> *If this agent does something unexpected - can you detect it, stop it, explain it, and fix it - fast?*

**If yes:** deploy with confidence.

**If no:** that is your security roadmap.

---

## Why This Question Works

Every governance framework, every threat model, every checklist item, every layer of the Trustworthy Agent Stack - they all exist to make the answer to this question *yes*. Strip away the detail, the acronyms, the tooling, and the frameworks, and that is the test. Can you respond effectively when the agent fails? Because at sufficient scale and over sufficient time, agents will occasionally fail. The question is whether your system is designed to catch it.

## Can You Detect It?

Detection requires observability. If you do not know what the agent is doing in real time - which tools it is calling, how many tokens it is consuming, what patterns are emerging - you cannot detect a failure until it surfaces as a user complaint, a breach notification, or a compliance finding.

The controls that enable detection:
- Audit logging on the agent identity - every action, timestamped and attributed.
- Tool call tracing - what was called, when, with what parameters, producing what outcome.
- Token usage monitoring with anomaly alerting.
- ASSERT or equivalent automated evaluations running on schedule.

**The test:** Simulate an agent failure in your staging environment. How quickly does your monitoring surface it? If the answer is "we would find out from a user complaint," your detection capability needs investment.

## Can You Stop It?

Stopping requires that the agent has clear boundaries - technically enforced, not just stated in policy - and that you have a known procedure to disable it immediately when those boundaries are violated.

The controls that enable stopping:
- Required PR review gates - the human can simply not approve.
- Rate limits and session timeouts - the agent cannot run indefinitely.
- Revocable agent identity - revoking the GitHub App installation or disabling the service account stops all activity immediately.
- Action allow-lists - the agent cannot take actions outside its registered tool set, regardless of what the model produces.

**The test:** Know today, in specific steps, how you would disable your most critical agent in under five minutes. If you cannot state those steps, closing that gap is this week's task.

## Can You Explain It?

Explanation requires a complete, reproducible audit trail in a form that is human-readable and presentable to a non-technical audience.

The controls that enable explanation:
- Complete input-to-action tracing - for any agent action, you can retrieve the full chain: what the user asked, what the agent retrieved, what the model reasoned, what it decided, what it did.
- Structured action logging - entries that make the causal chain explicit, not just a list of API calls.
- Session replay capability - the ability to reconstruct a full session's reasoning from logs.

**The test:** Pick any action the agent took last week. Can you produce a two-paragraph narrative explaining what triggered it, what the agent did, and why - in language suitable for a regulatory inquiry? If not, your logging is insufficient.

## Can You Fix It?

Fixing requires both technical capability (rollback, patch, redeploy) and process (tested incident response plan, communication templates, root cause analysis framework).

The controls that enable fixing:
- Version-pinned model deployments - you can roll back to a previous model version if an update introduces a regression.
- Tested incident response procedure - not just written, but exercised before the incident.
- Root cause analysis template - a defined framework for investigating what went wrong and what systemic change prevents recurrence.
- Communication playbook - what you tell affected users, when, and in what format.

**The test:** Run a tabletop incident exercise for an agent failure scenario. Walk through detection, containment, explanation, and remediation. The gaps you find in the exercise are far cheaper to close than the gaps you find in a real incident.

## Trustworthy AI Is Not Perfection

The question does not ask: *"Will this agent never make a mistake?"* Because the answer, for any autonomous system operating at real-world scale, is no. Agents will encounter edge cases their designers did not anticipate. Models will drift. Inputs will occasionally be adversarial. Errors will happen.

The question is whether the system around the agent is designed to respond well when errors occur. Detection, containment, explanation, and recovery - this is incident response. It is not a new discipline. You already know how to do it. Apply it to agents.

**Trustworthy AI is not an AI that never fails. It is an AI that fails safely.**

## You Are Not Behind

This session closes the same way it opened: **you are not behind.**

The security fundamentals you already know - threat modelling, least privilege, identity management, observability, and incident response - are the exact disciplines required to build trustworthy agents. The attack surface is new. The autonomy is new. The speed is new. The discipline required to address it is not.

The security profession is not catching up to AI agents. The security profession is the most critical set of practitioners for getting this right. And the organisations that pair development velocity with genuine security rigour - that make the secure path the default path, that embed controls in the workflow rather than bolting them on afterward - are the ones that will earn the right to deploy more capable agents, in more sensitive contexts, with greater confidence.

**Thank you.**

---

## Resources

- **Microsoft Security Blog:** [microsoft.com/security/blog](https://microsoft.com/security/blog) - Build 2026 security guidance for agents
- **OWASP Top 10 for LLM Applications:** [owasp.org/www-project-top-10-for-large-language-model-applications](https://owasp.org/www-project-top-10-for-large-language-model-applications)
- **GitHub Copilot Documentation:** [docs.github.com/copilot](https://docs.github.com/copilot)
- **Microsoft Open Trust Stack:** [devblogs.microsoft.com/foundry/build-2026-open-trust-stack-ai-agents](https://devblogs.microsoft.com/foundry/build-2026-open-trust-stack-ai-agents)

---

**Want to continue the conversation?** [Get in touch](https://www.scaling-guacamole.com/about.html)

<div class="chapter-nav" markdown>
[← Back: Slide 19](slide-19-checklist.md)
[Home →](index.md)
</div>
