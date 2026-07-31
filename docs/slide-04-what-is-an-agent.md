# Slide 4 · So What Is an AI Agent, Actually?

An AI agent is not a chatbot. A chatbot waits. An agent acts.

![AI agent concept hero image](assets/4-agent.png){ .hero-image }

## The Core Loop: Perceive → Reason → Act → Observe

The fundamental architecture of an AI agent is a repeating loop:

1. **Perceive** - The agent takes in context: user input, retrieved documents, tool outputs, memory from previous steps, environment state. Everything relevant to the current moment is assembled into a context window.
2. **Reason** - A large language model processes this context and produces a decision: what action to take next, or what to say. This is where intelligence happens - the model reasons over the available information and chooses a path forward.
3. **Act** - The agent executes that action using tools. Tools can include: calling an external API, running a code snippet, writing to a file, querying a database, searching the web, posting a message, opening a ticket.
4. **Observe** - The outcome of the action is fed back into context. The results become part of what the model reasons over in the next iteration. The loop repeats until the goal is achieved, a limit is hit, or a human intervenes.

This loop is the defining characteristic of an agent. Everything that makes agents powerful - and everything that makes them risky - flows from it.

## What Makes This Different from a Chatbot

A chatbot operates on a single turn: user sends a message, the LLM generates a reply, the user receives it. The model does not take actions on the user's behalf. It does not access external systems autonomously. It does not make a sequence of decisions where each builds on the last.

An agent breaks all three of these constraints:

- **Multi-step actions** with no human prompt required between steps - the agent keeps going until the task is done.
- **Real tool access** with real permissions - code execution, file I/O, API calls, database writes.
- **Chained decisions** where the outcome of step N determines what happens at step N+1.

## Real-World Example: A Coding Agent

Consider a GitHub Copilot coding agent receiving the instruction: *"Fix the authentication bug described in Issue #47."*

The loop plays out like this:

1. **Perceive:** Read Issue #47. Understand the bug description. Read the referenced code files. Build a model of the repository structure.
2. **Reason:** Identify the likely root cause. Determine which files and functions need to change.
3. **Act:** Write the code changes. Create a commit. Open a pull request with a clear description of what was changed and why.
4. **Observe:** A reviewer leaves a comment requesting a change. Read the comment. Reason about the feedback. Understand what is being asked.
5. **Act again:** Update the code. Push a new commit to the PR.

No human clicked "go" between those steps. That is an agent.

## Real-World Example: A Security Operations Agent

A SOC agent receives a high-severity alert:

1. **Perceive:** Read the alert. Understand the affected system, the time window, the anomaly pattern.
2. **Reason:** Is this likely a false positive or a genuine threat? What additional evidence would confirm it?
3. **Act:** Query log aggregation system for corroborating events. Call a threat intelligence API with the suspicious IP.
4. **Observe:** Threat intel confirms the IP is associated with a known malicious actor. The log query shows lateral movement.
5. **Reason:** This is a confirmed incident. It requires escalation and containment.
6. **Act:** Create a high-priority incident ticket. Notify the on-call team via the alerting system. Propose a containment recommendation.

Minutes, not hours. That is the value proposition - and the risk surface - of agents.

## Why the Security Implications Are Profound

From a security standpoint, **every step in the loop is an attack surface**:

- **Perceive:** Can hostile content in the input manipulate the agent's instructions? This is prompt injection - the most critical vulnerability in agentic AI.
- **Reason:** Can the model be jailbroken or steered away from its intended policy by a sufficiently adversarial input?
- **Act:** Does the agent have more permissions than it needs? When manipulation succeeds at the reasoning step, the blast radius equals the agent's permission set.
- **Observe:** Can the output of a malicious tool call inject new instructions into the agent's context? This is indirect prompt injection - and it is harder to defend against than the direct variant.

Understanding the loop is not just a conceptual exercise. It is the map you use to identify where to deploy controls.

<div class="chapter-nav" markdown>
[← Back: Slide 3](slide-03-agenda.md)
[Next: Slide 5 →](slide-05-agent-spectrum.md)
</div>
