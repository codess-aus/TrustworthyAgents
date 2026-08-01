# Demo Runbook · Slide 17

Use this runbook to build and rehearse the two-part demo described in `context.md`: a live GitHub walkthrough first, with a standalone Python backup if the live environment is slow or unavailable.

## Demo Goal

Keep the message narrow:

- The point is **not** that the agent is perfect.
- The point is that **the controls catch mistakes**.
- Repeat the defence-in-depth framing throughout the demo.

## Part 1 · Live GitHub Demo

### Environment Checklist

Prepare a disposable test repository with:

- GitHub Advanced Security enabled
- a GitHub Copilot coding agent available on github.com
- branch protection requiring at least one human review
- required status checks that include code scanning
- secret scanning with push protection enabled
- a pre-prepared audit log export or screenshot

Also prepare:

- a tiny code change for the agent to implement
- a safe mock secret strategy for the demo
  - use a provider-issued test credential or another intentionally fake pattern in the disposable test repository
  - do **not** use a real secret value
- browser tabs opened in advance for:
  - the repository
  - the pull request view
  - the checks tab
  - the security findings view
  - the audit log evidence

### Live Flow

Run the live demo in this order:

1. Ask the agent to make the small code change.
2. Show the pull request opening under the GitHub App identity.
3. Show code scanning starting automatically on the PR.
4. Introduce the safe mock secret and show secret scanning or push protection catching it.
5. Show that the PR still cannot merge without a human reviewer.
6. Finish by showing the audit log evidence for the agent's actions.

### What to Say at Each Beat

| Beat | What to show | Message to land |
|---|---|---|
| Agent identity | PR author is the agent app, not a human user | Agent actions are attributable |
| Code scanning | Checks start without human intervention | The pipeline is the guardrail |
| Secret scanning | The mock secret is blocked or flagged | The controls catch high-volume agent mistakes |
| Reviewer gate | Merge remains blocked pending review | Human oversight is enforced, not optional |
| Audit log | Timestamped record of agent activity | Governance and compliance evidence already exist |

## Part 2 · Backup Python Demo

The repository includes `/home/runner/work/TrustworthyAgents/TrustworthyAgents/demo_agent_security.py` as a backup or companion demo.

### What It Demonstrates

- input sanitisation for obvious prompt injection attempts
- output validation before an agent action executes
- high-risk actions being blocked pending human approval

### How to Run It

```bash
python /home/runner/work/TrustworthyAgents/TrustworthyAgents/demo_agent_security.py
```

### Expected Outcome

The script should show:

- a safe input being accepted
- a prompt injection attempt being blocked
- an in-scope action being allowed
- a high-risk action being blocked

Use it when the live GitHub flow is unavailable, or as a short follow-up after the live demo to reinforce the runtime guardrail concept from Slide 14.

## Rehearsal Checklist

Slide 17 is budgeted for about four minutes, so rehearse for short, visible checkpoints:

- [ ] Agent prompt ready with the small code change
- [ ] Test repository and PR view open
- [ ] Checks tab open and refreshable
- [ ] Secret scanning evidence prepared
- [ ] Audit log screenshot or export ready
- [ ] Backup Python demo runnable from a terminal
- [ ] Closing line prepared: "Trust, but verify. Preferably just verify."

## On-Screen Narrative Anchor

Use `/home/runner/work/TrustworthyAgents/TrustworthyAgents/docs/slide-17-live-demo.md` as the narrative checklist while building or rehearsing. It already mirrors the same five demo beats and keeps the talk aligned with `context.md`.
