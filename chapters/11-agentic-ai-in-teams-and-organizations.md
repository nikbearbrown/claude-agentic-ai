# Chapter 11 — Agentic AI in Teams and Organizations

## TL;DR

- Individual good habits do not scale. A team deploying agentic AI needs shared policies, defined roles, tool approvals, audit logs, and escalation paths — not just cautious individuals.
- Governance is not bureaucracy for its own sake. It is the mechanism that makes accountability visible and checkable when agents act across shared systems.
- A team AI-use register — who owns each use case, what data is allowed, what tools are approved, what the human gate is — is a minimum viable governance document.
- Meaningful oversight requires real authority, time, and evidence. Assigning someone to skim output is not a gate.

---

## Opening Scene

Picture a five-person marketing team six months into using Claude. Here is what their actual practice looks like on a Friday afternoon:

Person A has Cowork connected to the client contracts folder and uses it to draft status reports. Person B uses a personal Claude account on their laptop and pastes in excerpts from internal Slack messages. Person C refuses to use AI on anything client-facing and is skeptical the others are being careful. Person D set up a Cowork scheduled task that sends a weekly digest — no one else knows exactly what data it pulls. Person E asked IT to block Cowork and was told to figure it out on their own.

No one has done anything catastrophically wrong. But there is no shared understanding of what data is allowed, which tools are approved, who reviews what before it leaves the building, what a mistake would look like, or who is accountable if a client report contains a hallucinated figure.

This is the chapter's problem. Individual discipline is necessary but not sufficient. A team that deploys agents without shared governance has an inconsistency problem that grows proportionally with the number of people using agents and the breadth of what those agents can touch.

---

## What This Chapter Lets You Do

By the end of this chapter you will be able to:

- Explain why team-level governance adds requirements beyond individual supervision.
- Identify the shared assets and risks that create organizational exposure.
- Build a team AI-use register with use cases, owners, data boundaries, tool approvals, and human gates.
- Describe the role of audit trails in making agent actions accountable.
- Draft a lightweight escalation path for novel or sensitive situations.

This chapter applies the individual supervision concepts from Chapters 3, 8, and 10 to the organizational level. The principles — scope, permissions, approval gates, verification — remain the same. The difference is that a team must make those rules explicit, shared, and durable.

---

## Why Individual Caution Is Not Enough

A single practitioner managing their own agentic work can hold the scope, tool choices, and approval logic in their head. When agents act across shared systems — shared folders, shared repositories, shared connectors, team communication channels, external-facing documents — the scope and the risk are no longer individual.

Three problems emerge at scale:

**Inconsistency.** When every team member has different rules, there is no predictable boundary. Data that one person thinks is approved may be prohibited under another person's reading. A connector that one person runs against sensitive files may have been added to the team account and is now visible to others.

**Accountability gaps.** If an agent produces a flawed output — an incorrect figure in a client deliverable, an unauthorized data disclosure, an external message sent prematurely — it is not clear who owned that task, who approved the data scope, and who verified the output. Individual practice does not answer these questions at the organizational level.

**Governance drift.** Without shared documentation, the team's actual practice diverges from what anyone would endorse if asked. The scheduled task no one remembers setting up is an audit risk. The connector someone added for convenience last quarter may have permissions that extend beyond the original use case.

NIST's AI Risk Management Framework (NIST AI RMF 1.0, 2023) addresses this directly: organizational governance requires not just individual risk awareness but explicit management functions — govern, map, measure, and manage — applied to AI systems. ISO/IEC 42001:2023 frames AI governance as a management system, the same way organizations manage quality or security. The point is not formality for its own sake. The point is that shared governance makes accountability possible.

---

## Core Concepts

### The Team Operating Model

A team operating model for agentic AI is a set of shared decisions about:

- **Approved use cases.** What tasks can agents be used for? A use-case inventory prevents unreviewed expansion.
- **Prohibited data and actions.** What must never enter an agent context? Credentials, PII, unpublished confidential data, and production system access are common prohibitions.
- **Tool and connector approvals.** Which Claude surfaces, MCP servers, and connectors are approved for team use? Who can add a new one? Who reviews the tool's permissions and removes it when no longer needed?
- **Role boundaries.** Who can initiate an agentic task? Who can approve high-risk actions? Who owns verification before external use?
- **Audit trails.** What is logged? Who can access the log? How long is it retained?
- **Escalation paths.** What triggers a human escalation — unexpected data, an action outside the defined scope, a sensitive output, an agent request for access it was not designed to have?
- **Review cadence.** When does the team revisit its use-case inventory, tool approvals, and policy? AI capabilities and organizational needs change; a static policy becomes stale.

This is not a new governance bureaucracy. For a five-person team, this can be a shared document, a brief onboarding checklist, and a regular ten-minute team review. For a regulated enterprise, it maps onto formal compliance requirements. The governance ladder scales:

| Level | What it looks like |
|---|---|
| Personal rule | Individual judgment about what to delegate |
| Team norm | Shared verbal agreement on approved uses |
| Documented workflow | Written use-case list with data boundaries |
| Approved tool list | Formal review before adding connectors or MCP servers |
| Audit trail | Logs of what agent did, who approved, what changed |
| Formal risk management | NIST AI RMF or ISO/IEC 42001 implementation |
| Enterprise compliance | Legal, IT, and privacy review of all agentic workflows |

Most readers of this book are operating at levels 2–5. The chapter's goal is to help them do that deliberately.

### Shared Assets and Risk Surface

When an agent can access shared assets, individual risk becomes team risk. The shared assets that most commonly appear in agentic workflows:

- **Shared file systems.** A Cowork connector to a team folder gives the agent access to everything in that folder, not just the files one person intends to use.
- **Shared repositories.** Claude Code on a team repository touches code that multiple people depend on.
- **Shared communication channels.** An agent with access to Slack, email, or calendar can read and potentially draft messages across team communications.
- **Shared MCP servers.** An MCP server enabled for a team account is available to anyone with access to that account. OWASP's Top 10 for Model Context Protocol (2025) specifically names server trust, tool permission scope, and credential exposure as risks in shared deployments. [verify — current as of writing]
- **External-facing systems.** Any agent action that reaches outside the organization — sending email, updating a public document, posting to an external system — requires a higher gate than internal-only work.

The first governance task is mapping the team's actual shared assets and asking which ones agents can currently reach. The answer is often more than the team expects.

### The Team AI-Use Register

The team AI-use register is the practical governance document. It answers: for each use case, what is allowed, who is responsible, and what does the human gate look like?

| Field | Example entry |
|---|---|
| Use case | Draft client status report from project files |
| Owner | Project manager |
| Claude surface | Cowork |
| Data allowed | Sanitized project folder only |
| Data forbidden | Contracts, PII, credentials, financial terms |
| Tools / connectors | Approved project folder connector only |
| Human gate | Source and privacy review before sending |
| Log | Prompt used, files accessed, output produced, reviewer name |
| Escalation | Legal/privacy lead if sensitive data appears in output |

A use-case register does not have to be long. Three to ten entries covering the team's regular agent uses is a starting point. The key is that the team has agreed on the boundaries, not that the document is comprehensive.

### Meaningful Oversight

Zhu et al. (2026), in research on designing meaningful human oversight, identify a recurring failure mode: nominal oversight. A reviewer is assigned, but they lack the time, the context, the authority, or the evidence to actually evaluate the output. The result is an oversight role that provides accountability on paper but no real check on what the agent did.

Meaningful oversight requires:

- **Time.** A reviewer who has thirty seconds to skim a ten-page report is not reviewing it.
- **Context.** A reviewer who does not know what data the agent used, what instructions it was given, or what it was supposed to produce cannot catch fabrications, omissions, or scope violations.
- **Authority.** A reviewer who cannot reject or revise the output — because the deadline has passed, because the requester outranks them, because the culture treats agent output as default-approved — is not a gate.
- **Evidence.** A reviewer who sees only the final output cannot check whether the agent used approved data, whether sources were verified, or whether the scope stayed within bounds.

The audit trail makes meaningful oversight possible. When the log records what prompt was used, what files the agent accessed, what tools ran, and what the output was, the reviewer has the evidence to actually review. Without that log, oversight is a formality.

---

## Worked Walkthrough: A Software Team's Agent Policy

Consider a software team of eight engineers using Claude Code for development work. Without a policy, the practice varies: some engineers use Claude Code on feature branches, some use it directly on main, some have given it read access to production configuration files, and one recently asked it to help write a database migration without running tests.

The team works through the following exercise:

**Step 1: Use-case inventory.** They list what agents are actually used for: feature branch development, test writing, documentation, code review assistance, migration planning.

**Step 2: Data and access boundary.** They agree: Claude Code may access the repository but not production credentials, environment files, or external secrets management. They add a `.claudeignore` file listing excluded paths. [verify — current as of writing]

**Step 3: Approval structure.** Feature branch work: engineer reviews the diff before committing. Test-requiring changes: tests must pass before merge. Production-adjacent work (migrations, configuration changes): senior engineer review required before any execution.

**Step 4: Audit trail.** The team uses the existing PR review history as their primary audit artifact. For agent-assisted work, the PR description includes a note: what the agent was asked to do, what tests were run, what the human verified.

**Step 5: Escalation.** If Claude Code requests access to a path outside its defined scope, or proposes an action the engineer does not recognize as part of the approved task, they stop and bring it to the team.

**Step 6: Review cadence.** Monthly retro includes a standing agenda item: any agent incidents, any policy questions, any new use cases to evaluate.

This is not a heavy process. It takes the team an hour to draft and ten minutes a month to maintain. It converts informal individual caution into a shared, auditable practice.

---

## Application Domain Examples

The team operating model adapts across domains. The core structure — use case, data boundary, tool approval, human gate, log — stays constant; the specific rules change.

**Research group.** Approved: literature assembly from open-access sources. Restricted: any unpublished data, collaborator work shared in confidence. Prohibited: uploading peer-review materials to commercial AI accounts. Gate: researcher verifies all claims against original sources before manuscript inclusion.

**Marketing team.** Approved: Cowork drafts from approved brand and project folders. Restricted: client contracts, pricing data, anything under NDA. Gate: brand and legal review before any external publication.

**Education team.** Approved: rubric drafting and example generation from anonymized course materials. Prohibited: student records, identifiable student work, anything protected under FERPA. Gate: instructor owns all feedback before delivery.

**Operations team.** Approved: scheduled Cowork summaries of controlled operational folders. Prohibited: external messages, purchasing actions, system changes. Gate: human sends all external communication; agent output is internal draft only.

The shared pattern: the team has named the boundary, not just assumed individuals will figure it out.

---

## MCP Governance at the Team Level

MCP servers compound the governance challenge. A single MCP server added to a team account can give every team member's agent access to an external system, a database, a calendar, or an API. OWASP's Top 10 for LLM Applications (2025) and its parallel Top 10 for MCP identify tool permission scope and server trust as organizational risks, not just individual ones. [verify — current as of writing]

A minimal team MCP governance policy covers:

- **Approved server list.** Which servers are approved for team use? Who maintains the list?
- **Owner per server.** Each server has a named owner responsible for understanding its permission scope and keeping it current.
- **Documented tools.** What tools does each server expose? What systems can it reach? What actions can it take?
- **Access scope.** Is the server available to all team members, or to specific roles?
- **Logs.** Does the server produce logs of tool calls? Who can access them?
- **Decommissioning.** When a server is no longer needed, who removes it and confirms removal?

The principle of least privilege (Chapter 3) applies at the team level: approve the minimum tool set for the defined use case and revisit when the use case changes.

---

## Common Misconceptions

**"Team policy is just a list of banned tools."** A prohibition list without approved uses and ownership is incomplete. People will work around bans when they have a legitimate need and no approved path.

**"If individuals are careful, governance is unnecessary."** Individual care does not produce consistent practice, does not create accountability when something goes wrong, and does not prevent the shared-asset risks that emerge when multiple people use agents against common infrastructure.

**"Audit trails are only for regulated industries."** Audit trails are how you answer "what happened and who is responsible" when an agent output causes a problem. That question is not limited to regulated industries.

**"Human oversight means assigning someone to skim the output."** Meaningful oversight requires time, context, authority, and evidence. Nominal assignment is not a control (Zhu et al., 2026).

**"Shared prompts are enough."** Shared prompts standardize instructions but do not establish data boundaries, tool approvals, ownership, or verification requirements.

**"Enterprise settings automatically solve privacy and accountability."** Enterprise tier controls, memory management, and audit features reduce some risks, but they do not substitute for a use-case register, role boundaries, and human gates. [verify — current as of writing]

---

## Try This

**Exercise 1: Map your team's current agent use.**
List every agent-assisted workflow your team or organization actually uses today — not what is officially approved, but what is actually happening. For each one, answer: what data does the agent access? Who owns the task? What is the human gate before the output is used? How many of these are documented?

**Exercise 2: Draft a team AI-use register entry.**
Take one use case from your list and fill out the register template from this chapter: use case, owner, Claude surface, data allowed, data forbidden, tools/connectors, human gate, log, escalation. Share it with one colleague and ask what is missing or wrong. Revise it once.

**Exercise 3: Evaluate a proposed MCP server.**
Find or imagine an MCP server your team might add (a calendar connector, a database connector, a file-search server). Walk through the governance checklist: What tools does it expose? What systems does it reach? Who is the owner? What is the access scope? What would go in the log? How would you decommission it? Decide whether to approve, restrict, or reject it.

---

## What Would Change My Mind

The chapter argues that informal individual practice is insufficient once agents act on shared assets, and that a lightweight team governance model — use-case register, data boundaries, approval gates, audit trail — is the minimum viable structure.

This argument would weaken if:

- Evidence showed that teams with no explicit governance had materially fewer agent-related incidents than teams with documented practices. No such evidence currently exists.
- Tools emerged that automatically enforced data boundaries, permission scopes, and audit logging at the platform level in ways that eliminated the need for human-designed governance. Current platform controls reduce but do not eliminate governance requirements. [verify — current as of writing]
- The costs of team governance consistently exceeded its benefits across small teams. In practice, a use-case register takes an afternoon to draft and prevents inconsistencies that take far longer to resolve.

---

## Still Puzzling

**How much governance is appropriate for a two-person team?** The chapter provides a ladder, but the minimum viable governance for very small teams is worth continued refinement. Too little is insufficient; too much becomes its own obstacle to adoption.

**Who owns AI governance in organizations where IT, legal, and operational teams have competing authority?** The chapter focuses on team-level practice, but the organizational politics of AI governance ownership are genuinely contested and not resolved by frameworks alone.

**How do audit trails interact with data-retention and privacy obligations?** Keeping logs of what data an agent accessed may itself create retention obligations or privacy risks in some jurisdictions. This tension requires legal guidance specific to context.

**How should teams handle "shadow AI" — agent use that bypasses official channels?** The marketing example in the opening scene is not unusual. Teams that ban tools without providing alternatives typically see higher shadow use. The policy question of how to bring shadow use into a governable structure is not fully solved.

---

## AI Wayback Machine

![Elinor Ostrom](../images/elinor-ostrom-5bi.png)

*Puppet Art by [Nik Bear Brown](https://www.nikbearbrown.com/).*

**Run this:**

```
Who was Elinor Ostrom, and how does her work on governing the commons connect to how teams should manage shared AI tools and agent access? Keep it to three paragraphs. End with the single most surprising thing about her career or ideas.
```

Search **"Elinor Ostrom"** on Wikipedia, then try it with Claude.

**Now make the prompt better:**

- Ask it to apply Ostrom's design principles for commons governance to a specific shared AI resource — a team Cowork account, a shared MCP server, or a team repository with Claude Code access.
- Ask whether "the tragedy of the commons" applies to AI tool use on a team. Does it, or does the analogy break down?

What changes? What gets more useful? Where does the analogy fail?

---

## Sources Used

NIST. "Artificial Intelligence Risk Management Framework (AI RMF 1.0)." 2023. https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10

NIST. "Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile." 2024. https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf

ISO/IEC 42001:2023. "Artificial Intelligence Management System." https://www.iso.org/standard/42001

Zhu et al. "Designing Meaningful Human Oversight in AI." AI and Ethics, 2026. https://link.springer.com/article/10.1007/s43681-026-01147-7

"AAGATE: A NIST AI RMF-Aligned Governance Platform for Agentic AI." arXiv, 2025. https://arxiv.org/abs/2510.25863

"Policy-Aware Generative AI for Safe, Auditable Data Access Governance." arXiv, 2025. https://arxiv.org/abs/2510.23474

OWASP. "Top 10 for LLM Applications 2025." https://owasp.org/www-project-top-10-for-large-language-model-applications/

OWASP. "Top 10 for Model Context Protocol." https://owasp.org/www-project-mcp-top-10/

Anthropic. "Use Claude Cowork safely." Claude Help Center. https://support.claude.com/en/articles/13364135-use-cowork-safely

Anthropic. "Use Claude's chat search and memory to build on previous context." Claude Help Center. https://support.claude.com/en/articles/11817273-using-claude-s-chat-search-and-memory-to-build-on-previous-context
