# Slide 14 · Layer 3: Runtime Controls and Guardrails

The policy layer that enforces what the agent can and cannot do - at execution time, regardless of what the model decides.

![Runtime Controls hero image](assets/14-controls.png){ .hero-image }

## The Critical Insight: Infrastructure Controls Beat Prompt Controls

An agent's system prompt says: *"You must never send emails."* That is a prompt-level policy statement. The model reads it. The model will generally respect it. But a sufficiently adversarial input, a model reasoning error, or a carefully crafted jailbreak can cause the model to disregard it.

Runtime controls are categorically different. They enforce policy at the infrastructure layer - outside the model, after the model has produced its output, before any action executes.

**If the email tool is not registered in the agent's tool definition, the agent literally cannot send an email.** No model reasoning, no adversarial prompt, no jailbreak can cause it to take an action it architecturally cannot take.

This is the same principle as the difference between "the application code checks if the user is an admin before allowing this operation" (application-level control, bypassable) and "the database connection this service uses only has SELECT permissions on this table" (infrastructure-level control, not bypassable by the application). Infrastructure controls are more reliable.

## The Microsoft Agent Control Specification (ACS)

Announced at Build 2026, the **Agent Control Specification (ACS)** is a portable, framework-agnostic policy layer for agent runtime enforcement. Its key properties:

- **Framework-agnostic:** Works with LangChain, Semantic Kernel, CrewAI, AutoGen, OpenAI Assistants, and other frameworks. The policy travels with the agent configuration, not embedded in framework-specific code.
- **Portable:** If you migrate the agent from one orchestration framework to another, the ACS policy continues to apply.
- **Declarative:** You define what the agent *can* and *cannot* do in structured configuration, not in prose instructions to the model.

**Illustrative ACS policy:**

```yaml
agent_policy:
  allowed_tools:
    - name: search_knowledge_base
      max_calls_per_session: 20
    - name: post_comment
      targets: [issues, pull_requests]
  blocked_actions:
    - send_email
    - execute_code
    - access_external_url
  human_approval_required:
    - merge_pull_request
    - deploy_to_production
    - delete_resource
  session_limits:
    max_tokens: 100000
    max_tool_calls: 50
    timeout_seconds: 300
```

In this policy, the agent's capabilities are exhaustively enumerated. Everything not in `allowed_tools` is blocked. High-impact actions require explicit human approval. Resource consumption is bounded.

## Practical Runtime Controls

### Output Filtering and Action Validation

Before the agent executes any action based on model output, apply a validation step:

- **Is the proposed action in the allowed tool list?** If not, block it and log the attempt as a security signal.
- **Do the action's parameters match expected patterns?** An agent that should only post comments should not be proposing code commits. A file-reading agent should not be proposing file writes.
- **Does the output contain sensitive data patterns?** Credential formats (API keys, tokens), PII patterns (email addresses, SSNs), or internal system identifiers should be detected and blocked or redacted before the action is executed.

Output validation is a second line of defence that catches model outputs that fall outside scope - regardless of whether they were produced by a normal reasoning error or adversarial manipulation.

### Action Confirmation for High-Risk Operations

Some actions are irreversible, high-blast-radius, or both: merging code to a production branch, deleting resources, sending communications to external parties, deploying to production environments, making financial transactions.

These should require explicit human confirmation before execution, at every autonomy level except the most carefully constrained autonomous deployments. This is not bureaucracy - it is the engineering equivalent of the "Are you sure? This cannot be undone." dialog applied to consequential agent actions.

**Implementation pattern:** When the agent proposes a high-risk action, instead of executing it, the agent surfaces it to a human review queue. The human reviews the proposed action with full context - what input prompted it, what the agent reasoned - and approves or rejects it. Only on approval does the action execute.

### Rate Limiting and Cost Controls

An agent consuming unlimited tokens, making unlimited tool calls, or spawning unlimited sessions is an availability risk and a cost risk. A prompt injection attack that causes the agent to enter an infinite reasoning loop will exhaust your LLM budget and potentially your compute resources before any human notices.

Enforce:
- **Maximum tokens per session** - define this based on the expected task size; set the limit at 3-5× the typical usage to allow for complexity while bounding abuse.
- **Maximum tool calls per session** - an agent that needs to call 200 tools to complete a "summarise this document" task has something wrong with it.
- **Maximum concurrent sessions per identity** - prevents a single compromised input from spawning unbounded parallel sessions.
- **Spend alerts** - budget alerts at defined thresholds (50%, 80%, 100% of expected spend) provide early warning of anomalous usage before it becomes a budget incident.

### Jailbreak and Injection Detection in the Input Pipeline

Before user input reaches the LLM, apply a pre-processing step that uses pattern matching, classifier models, or dedicated safety services to identify likely adversarial inputs.

**Microsoft Prompt Shields** and **Azure AI Content Safety** provide this capability at scale - they evaluate input against known jailbreak and injection patterns, and can be integrated into the agent's input pipeline as a blocking or flagging step.

For simpler deployments, a heuristic approach - blocking inputs that contain known injection phrases like "ignore previous instructions," "you are now DAN," or role-play framings that attempt to override identity - eliminates the majority of commodity attacks.

No detection system catches everything. A determined adversary will probe for gaps. But a well-tuned detection layer raises the cost of attack significantly and eliminates the bulk of automated, commodity attempts.

## GitHub as a Native Runtime Guardrail

For agents that work in GitHub repositories, GitHub's built-in features function as runtime controls that require no additional implementation:

**Required PR reviews:** Every agent-opened PR must be reviewed by a human before it merges. The merge button is disabled until approval is granted. The agent cannot bypass this - it is enforced by GitHub's API, not by the agent's cooperation.

**Code scanning as a required status check:** GitHub Advanced Security automatically scans every PR for vulnerabilities. Making this a required status check means the agent's code cannot merge until the scan passes. There is no fast lane for agent-generated code.

**Secret scanning with push protection:** Any agent-generated commit that contains a credential matching a known secret pattern is blocked before the push completes. The agent cannot push a commit containing a leaked secret, even accidentally.

**Protected branches:** Main and release branches cannot receive direct pushes, even from identities with write access. All changes must go through the pull request workflow - which includes all the controls above.

When agents work within GitHub's existing security infrastructure, the infrastructure enforces policy on every action the agent takes. That is the definition of a runtime guardrail: it applies regardless of the agent's configuration, the model's output, or the content of the input.

<div class="chapter-nav" markdown>
[← Back: Slide 13](slide-13-identity-least-privilege.md)
[Next: Slide 15 →](slide-15-observability.md)
</div>
