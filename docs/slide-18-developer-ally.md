# Slide 18 · The Developer Is Your Ally

Security professionals and developers are not adversaries. They are solving the same problem from different angles, and the best security outcomes happen when they solve it together.

## The False Dichotomy

There is a persistent narrative that positions security teams and development teams in opposition. Security slows developers down with bureaucratic gates. Developers cut corners on security to meet deadlines. Each views the other as an obstacle.

This narrative is wrong. It is counterproductive in any software context. It is especially counterproductive when building AI agents - where the pace of deployment is high, the attack surface is new, and the cost of getting it wrong is significant.

**The reality:** The best security outcomes happen when security is *embedded in the developer's workflow* - not imposed on it from outside. When security checks surface in the IDE before code is committed. When vulnerability findings appear in the PR, not in a quarterly audit. When the secure configuration is the default configuration. When the secure path is the easiest path.

## Where Security Lives in the Developer's World

### The IDE: Where Code and Agent Designs Are Created

GitHub Copilot surfaces security-relevant suggestions at the point of creation. When a developer writes an SQL query, Copilot knows that parameterised queries are safer than string concatenation and suggests accordingly. This is security shifting left past the PR, past the branch, all the way to the moment of writing.

For agent development, the equivalent is: security thinking happens when the system prompt is designed, when the tool list is assembled, when the permission scopes are defined - in the planning and design phase, with security expertise available *in the tooling*, not locked in a separate team that reviews things weeks later.

### The Pull Request: Where Code and Agent Configurations Are Reviewed

The PR is the natural integration point for automated security checks. Code scanning, secret scanning, dependency scanning - all of these run automatically on every PR, including agent-opened PRs. They produce findings in a format developers understand, in the context where they are already reviewing code.

This is not friction bolted onto the developer workflow. It is part of the PR experience they already use every day. The security gate and the quality gate are the same gate.

### The Pipeline: Where Code and Agent Actions Are Validated

GitHub Actions workflows are the developer's definition of "done." Code is not ready until the pipeline passes. By making security checks required status checks in that pipeline, you make security part of the developer's definition of done - the same definition, the same workflow, no separate process.

For agents specifically: the pipeline is the guardrail. An agent cannot merge code that fails a required code scan. An agent cannot push a commit containing a detected secret. An agent cannot merge without a human reviewer's approval. These are all pipeline controls. They require no additional process from the developer - they run automatically as part of the existing workflow.

### The Audit Log: Where Trust Is Proven

Developers tend not to think about audit logs. Security and compliance teams do. But the audit log is what makes the other three layers credible. It proves the controls ran. It proves what the agent did. It is the evidence that converts developer velocity into demonstrable, auditable trust.

**GitHub connects all four layers.** IDE → PR → Pipeline → Audit log. A complete, integrated security workflow that developers already live in. The agent operates within that same workflow - and so the security infrastructure already applies to everything the agent does.

## The Message to Security Professionals

If you are in a security role, the single most impactful thing you can do for agent security is not to build a complex control framework that development teams must navigate. It is to make the secure configuration the **default configuration**.

**Default branch protection** - require reviews and code scanning on every repository from day one, so agents working in those repositories are immediately subject to those controls.

**Default secret scanning with push protection** - enabled organisation-wide, not opt-in. Secret exposure from agent-generated code is a when-not-if problem at sufficient volume.

**Default agent identity patterns** - create internal accelerators, templates, and starter kits that use GitHub Apps with minimum required permissions by default. When developers reach for the template, they get the secure pattern automatically.

**Default pipeline templates** - Actions workflow templates that include code scanning as a required check, provided as the standard starting point for new projects.

When the secure path is the easy path, developers take it without thinking about security. That is the goal. Security that requires developer effort to maintain is security that will degrade over time. Security that is the default requires no effort to maintain - it simply is.

## The Message to Developers

If you are building AI agents: your security colleagues are not trying to slow you down. They are trying to give you a faster path to production - a path that does not end with a last-minute security review halt a week before launch because the agent was built without the controls required for production deployment.

The Trustworthy Agent Stack is not a bureaucratic checklist. It is the architecture of an agent that you can actually ship - one that will pass the security review, satisfy the CISO, meet the privacy requirements, and earn the user's trust.

Build it in from the beginning. Threat model before you code. Define permissions before you implement. Enable logging before you deploy. It is significantly easier to build security in from the start than to retrofit it into an agent that is already in production and that users are depending on.

## The Shared Goal

Security professionals want the organisation to be secure. Developers want to ship useful software. AI agents - when built correctly - make both teams' jobs easier: more automation, higher quality, faster delivery, with the controls in place to demonstrate trust.

The question is not whether to use agents. It is how to build them so that when they ship, everyone - the developer, the security team, the user, the regulator - can answer *yes* to the question on the next slide.

<div class="chapter-nav" markdown>
[← Back: Slide 17](slide-17-live-demo.md)
[Next: Slide 19 →](slide-19-checklist.md)
</div>
