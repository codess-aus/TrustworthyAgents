# Slide 5 · The Agent Spectrum

Not all agents are equal. Your security posture must match the autonomy level.

![The Agent Spectrum hero image](assets/5-spectrum.png){ .hero-image }

## The Four Levels of Agent Autonomy

### Level 1 — Assisted: Human Decides Everything

**What it looks like:** GitHub Copilot suggests a line of code in your IDE. The suggestion appears; you press Tab to accept it or keep typing to ignore it. The agent has generated a proposal; you have made every decision.

**Real-world example:** A developer is writing a function to hash a password. Copilot suggests `bcrypt.hash(password, 10)`. The developer reviews it, accepts it, and commits the code. At no point did the agent take an action without explicit human approval.

**Security posture:** Low risk. The agent has no runtime permissions — it only reads your open files. If the suggestion is wrong (including if it is subtly insecure), the human review gate catches it before the code runs.

**Risk to watch:** Training data poisoning. If the model has learned from code repositories containing vulnerabilities, its suggestions may include insecure patterns. The antidote is developer education combined with code scanning on every commit — humans and automation working together.

---

### Level 2 — Supervised: Agent Acts, Human Approves Before It Matters

**What it looks like:** An agent drafts a pull request, but a human must review and approve it before it merges. An agent composes an email response, but the user clicks Send. The agent has real write access and takes real actions — but every action with external consequences requires a human checkpoint first.

**Real-world example:** A dependency update agent runs weekly, identifies outdated packages, creates a PR with the updated `package.json` and lockfile, and requests review from the team. The team reviews the changes and either approves or requests modifications. The agent cannot merge without approval.

**Security posture:** Medium risk. The agent has write access (it creates commits, opens PRs, drafts content). If manipulated or misconfigured, it can create problematic output — but the human checkpoint prevents that output from having external effect without review.

**Risk to watch:** Review fatigue. If agents are opening a high volume of PRs or drafts, humans may stop reviewing carefully and rubber-stamp agent output. The guardrail exists architecturally but fails in practice. Mitigate by ensuring agents only open PRs when meaningful — not for every trivial change — and by making agent-generated PRs visually distinct so reviewers know to apply extra scrutiny.

---

### Level 3 — Autonomous: Agent Decides and Acts Without Supervision

**What it looks like:** An agent monitors a repository, detects dependency vulnerabilities, creates a patch PR, and auto-merges it if all CI checks pass — without any human in the loop. Or an agent that monitors infrastructure metrics and automatically scales resources based on load — no human approval required between detection and action.

**Real-world example:** A DevSecOps team deploys an agent that automatically patches known CVEs in dependencies. The agent is trusted to merge changes to non-critical configuration files when the change is small, well-defined, and all automated tests pass.

**Security posture:** High risk. The agent has end-to-end execution permissions. A compromised, manipulated, or misconfigured agent can make breaking changes to production systems without a human review gate. Every vulnerability in the agent's decision-making has a blast radius equal to its permission set.

**Risk to watch:** Excessive agency. If the agent's permissions exceed what any single task requires, a prompt injection or logic flaw can have consequences far larger than intended. An autonomous dependency patching agent should not have write access to application source code or deployment configuration.

---

### Level 4 — Multi-Agent: Orchestrators and Sub-Agents

**What it looks like:** A top-level orchestrator agent receives a high-level goal and decomposes it, delegating sub-tasks to specialist agents. The orchestrator communicates with a threat intelligence sub-agent, a remediation sub-agent, and a ticketing sub-agent — coordinating their outputs into a coherent result.

**Real-world example:** A security compliance pipeline where an orchestrator agent processes a new regulatory requirement, delegates to a code analysis sub-agent to scan the codebase for gaps, delegates to a policy drafting sub-agent to propose remediation steps, and then creates a tracked work item with both findings and proposed actions.

**Security posture:** Very high risk. Trust chains become complex. A compromised sub-agent can poison the orchestrator's context. Permissions granted to the orchestrator may be inherited by sub-agents that should not have them. The "confused deputy" problem — where one agent tricks another into using its elevated permissions — is a real attack in multi-agent systems.

**Risk to watch:** Trust boundary confusion. In most current agent frameworks, there is no cryptographic or structural mechanism for an orchestrator to verify that a sub-agent's output has not been manipulated. Treat sub-agent outputs as untrusted inputs — validate and sanitise before acting on them.

## The Human-in-the-Loop Dial

Think of it as a dial that runs from Assisted on the left to Multi-Agent on the right. As you turn it rightward, three things increase in parallel:

1. **Capability** — the agent can accomplish more complex tasks with less human effort.
2. **Risk** — the blast radius of a failure or compromise grows.
3. **Required controls** — the security and governance framework must scale to match.

The goal is never to prevent the dial from being turned. Autonomous agents deliver real value. The goal is to ensure that your controls are calibrated to your autonomy level. A Level 1 security posture applied to a Level 3 agent is a serious misconfiguration.

<div class="chapter-nav" markdown>
[← Back: Slide 4](slide-04-what-is-an-agent.md)
[Next: Slide 6 →](slide-06-cloud-native-sdlc.md)
</div>
