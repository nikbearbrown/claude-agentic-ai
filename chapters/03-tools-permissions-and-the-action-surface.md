# Chapter 3 — Tools, Permissions, and the Action Surface

## TL;DR

- An agent's real power is defined not by what it knows but by what it can touch — its **action surface**.
- Least privilege is the governing principle: grant only the tools, folders, and connectors the task actually requires.
- Different access types carry sharply different risk. Read is not write; write is not execute; execute is not send.
- The agent's action surface is something the human designs before work starts, not something that can be fixed after overreach.

---

## Opening Scene

You ask an AI agent to "clean up this folder." The folder is your primary working directory. It contains a current tax return, signed client contracts, a folder of unedited personal photos, and two years of draft documents. The task sounds reasonable. The agent is capable. The problem is that the action surface is wrong.

Within a few minutes, the agent has sorted, renamed, and in some cases deleted items it classified as duplicates or clutter. The tax documents are where they were. The client contracts are not.

No malice. No error in the ordinary sense. The agent did what "clean up" suggested, bounded only by what you put in front of it. The failure belongs to the person who handed it the whole directory.

This chapter is about preventing that failure at the source. Before any agentic task starts, the capable user asks: *what does this agent actually need to touch?*

---

## What This Chapter Lets You Do

By the end of this chapter you can:

- Name the access types that make up an action surface and rank them by risk.
- Apply the principle of least privilege to a real agentic task.
- Distinguish reversible from irreversible actions and adjust permissions accordingly.
- Build a permission checklist and apply it before delegating work.
- Recognize when a tool or plugin expands risk even when the task sounds simple.

---

## The Action Surface

The **action surface** is everything an agent can observe, call, edit, send, delete, execute, browse, or persist. It is not the same as what the agent will do; it is the complete set of what it could do if its reasoning, plan, or context led it there. That distinction matters because agent errors and prompt injections expand the harm in proportion to the surface, not in proportion to the intended task.

Access types in Claude's agentic surfaces [verify — current as of writing] include:

| Access type | What it can expose or change | Risk level | Default rule |
|---|---|---|---|
| Chat only | Text in the conversation | Low–moderate | Verify claims before acting on them |
| Uploaded file | Contents of that file | Moderate | Use copies; redact sensitive data |
| Local folder | Every file in that folder | Moderate–high | Use a dedicated, limited folder |
| Connector / MCP | Data and actions in a connected service | High | Grant least-privilege scope only |
| Browser | Web content, app state, form submission | High | Trusted sources only; no logins or purchases |
| Terminal / API | Shell commands, external system state | High | Require approval; log all commands |
| Computer use | Visible desktop and any running app | High | Use only with strict, defined scope |
| Scheduled task | Future unattended actions | High | Low-risk tasks only; human review cycle |

The pattern is stable even as specific products change: the more the agent can touch, the larger the blast radius of an error.

---

## Least Privilege: The Governing Principle

Jerome Saltzer and Michael Schroeder named the principle in 1975: "Every program and every user of the system should operate using the least set of privileges necessary to complete the job" (Saltzer and Schroeder, 1975). The security world has refined the language; the concept has not changed.

For agentic AI, least privilege means:

- Grant the minimum tools the task requires.
- Restrict folders to those the task needs.
- Exclude connectors the task has no business using.
- Never grant production credentials, billing access, or deletion authority for routine work.
- Expand permissions only when there is a specific need and a verification path.

The temptation runs in the other direction. A broader action surface appears to make agents more capable and less likely to need help. In practice, broad access makes errors harder to reverse, makes prompt injection more dangerous, and makes audit harder. OWASP names excessive agency as a core LLM application risk — an agent with over-permissive tooling can "perform actions or acquire resources beyond what is needed" for the task, enabling downstream harm (OWASP LLM Top 10, 2025).

---

## The Access Ladder

Think of permissions as a ladder with cost increasing at every rung. The principle is to stand on the lowest rung that lets the task proceed.

**Rung 1: Chat only.** The agent reads what you paste and produces text. It cannot reach anything outside the conversation. Low action surface; appropriate for drafting, summarizing things you paste in, and thinking through options.

**Rung 2: Uploaded file.** The agent can read a specific file you have attached. It cannot reach your disk. Appropriate for analyzing a document, checking calculations, or reviewing a draft. Use a copy, not an original containing sensitive data.

**Rung 3: Local folder.** The agent can read, create, and modify files in a folder you designate. This is where the opening scene went wrong. The safe version uses a dedicated working folder containing only the files the task needs. Source files stay in the original location; copies go into the working folder.

**Rung 4: Connector or MCP server.** The agent can call an external service — a calendar, database, project tool, or API — through a defined interface. Before enabling a connector, inspect: What data can it read? What actions can it take? Can it send messages, book things, or modify records? OWASP's MCP Top 10 highlights excessive permissions, tool poisoning, and command injection as specific risks when connectors are enabled (OWASP MCP Top 10, 2025).

**Rung 5: Browser.** The agent can load and interact with web pages and web applications. Screen-visible content can contain instructions that manipulate the agent's behavior — a category of attack called visual prompt injection, documented in recent benchmark research (VPI-Bench, 2026). Browser access should be restricted to trusted public sources; login portals, form submissions, purchases, and message sending require explicit human approval.

**Rung 6: Terminal or API with commands.** The agent can run shell commands or call APIs with side effects. Command access is the highest common-case risk level for engineering work: packages can be installed, files can be deleted, external systems can be modified. Every command should require explicit approval or a carefully constructed policy that logs all actions.

**Rung 7: Computer use.** The agent can observe and interact with anything visible on the desktop — any app, any field, any button. This is the broadest surface. The Anthropic Cowork safety documentation recommends preferring connectors and browser access over direct computer use where alternatives exist, because the scope of possible action is hardest to bound at this level [verify — current as of writing] (Anthropic, "Let Claude use your computer in Cowork," 2026).

**Rung 8: Scheduled tasks.** The agent acts without a human present to observe. The same permission rules apply with stricter defaults: scheduled tasks should handle only low-risk, reversible work, with a human review of outputs before any consequential downstream action.

---

## Reversibility and Blast Radius

Every tool decision should account for two questions:

**Is this action reversible?** Moving a file to trash is reversible. Deleting permanently is not. Drafting an email is reversible. Sending it is not. Editing a copy is reversible. Overwriting an original is not. The harder an action is to undo, the more it deserves a human approval gate before it executes.

**What is the blast radius?** If the agent's plan is wrong, or if untrusted content in a document or web page manipulates the agent's reasoning, how much damage can result? An agent with read access to one folder and write access to one output file has a small blast radius. An agent with broad folder access, terminal access, and an active connector to an email service has a large one. Scale the approval friction to the blast radius, not to the plausibility of the plan.

Recent work on tool risk mitigation for agentic AI formalizes this intuition: the AgenTRIM approach proposes least-privilege tool filtering and validation of tool calls as a risk-reduction layer, because tool selection is itself a security surface (AgenTRIM, 2026).

---

## Plugins and Permission Bundles

A plugin bundles tools, connectors, skills, and sometimes sub-agents into a single installable package. The convenience is real: one installation and the agent gains multiple capabilities. The risk is that users evaluate plugins by their advertised function, not by their permission footprint.

Before enabling a plugin, ask the same questions you would ask about any tool: What can it read? What can it write or send? What external systems can it touch? Anthropic's plugin documentation notes that plugins extend what Cowork can do — the corollary is that they extend the action surface [verify — current as of writing] (Anthropic, "Use plugins in Claude Cowork," 2026).

The same principle applies to MCP servers added by an organization or a developer. The MCP protocol is designed to give agents controlled access to external capabilities. "Controlled" is a design goal, not a guarantee. Every new server is a new action surface that must be evaluated.

---

## The Human Gate: Permission Design Before the Task

The action surface is the human's responsibility, not the agent's. The agent uses what it is given. The user decides what to give.

Before any agentic task that involves more than chat:

**Tool needed?** Does the task actually require this access type, or is a lower rung sufficient?

**Scope limited?** Is the folder, connector, or API access as narrow as it can be while still enabling the task?

**Sensitive data excluded?** Are credentials, personal information, client records, financial data, or regulated data outside the working scope?

**Action reversible?** If the agent makes an error, can it be undone without data loss or external consequence?

**Human approval point?** For irreversible, external-facing, or consequential actions, is there a step where a human reviews and approves before execution?

**Output and action log?** Will the agent record what it did, what files it changed, and what commands it ran, so that review is possible?

**Verification evidence?** What will confirm that the action was correct — row counts, before/after snapshots, test results, a source log?

**Stop condition?** If the agent encounters something unexpected, does it pause and ask rather than improvising with broader access?

NIST's AI Risk Management Framework describes the need for documentation of controls and residual risk for AI systems in deployment (NIST AI RMF 1.0, 2023). The permission checklist above is the practitioner version of that discipline for single-user agentic work.

---

## Common Misconceptions

**"A tool is harmless if the task is harmless."** The task does not bound the tool. An agent that can read a folder can read every file in that folder, including those irrelevant to the task.

**"Permission prompts mean the system is safe."** A prompt that says "Claude wants to access your Documents folder" is not a safety guarantee. It is an approval request. The user must decide whether to grant it, not merely click past it.

**"More connectors mean better results."** More connectors expand the action surface. They may improve results for a specific task; they always increase the scope of possible harm.

**"Read access is always low risk."** Read access can expose credentials stored in files, personal health records, confidential client data, or anything else in the accessible scope. Information exposure is real harm.

**"Browser access is the same as source lookup."** Browser access means the agent can interact with any reachable page, including login portals, purchase flows, and forms. Content on those pages may contain adversarial instructions that redirect agent behavior (VPI-Bench, 2026).

**"A plugin is just a convenience feature."** A plugin is a permission bundle. Evaluate it as such.

---

## Try This

**Exercise 1: Narrow the surface.**
Take a task you might ask an agent to do — compile a report from documents, organize a folder, extract data from files — and list every access type it would need if given broad permissions. Then reduce the list to the minimum. What can you move to a dedicated working folder? What requires a connector, and what would a connector need to be restricted from?

**Exercise 2: Rate the reversibility.**
For each of the following actions, decide whether it is reversible, partially reversible, or irreversible, and what approval step you would require:
- Moving a file to a temporary folder
- Renaming 200 files according to a naming convention
- Sending an email on your behalf
- Running a script that processes a CSV and overwrites the original
- Scheduling a weekly summary task

Compare your answers with a colleague. Where do you disagree? That disagreement is where your permission policy needs to be explicit.

---

## What Would Change My Mind

This chapter argues for conservative default permissions because errors and prompt injections are more damaging on broader surfaces. If future agentic systems develop reliable sandbox isolation that provably prevents an agent's tool calls from reaching outside a defined scope, the argument for restrictive access becomes less urgent inside that sandbox. Reliable, verifiable isolation would change the calculus. We do not have that routinely in 2026; check the state of sandboxing before relaxing defaults.

---

## Still Puzzling

How much approval friction is right? The tradeoff between safety and usability is genuinely contested. Too many approval gates make agents annoying and underused; too few create silent overreach. The field has not converged on a principled way to calibrate per-task friction. Risk-tiered defaults (reversible/internal = low friction; irreversible/external-facing = high friction) are the current practitioner heuristic, but they are heuristics.

---

## Bridge to Chapter 4

The action-surface framework applies everywhere an agent operates. The next two chapters show it in specific contexts: Chapter 4 in software engineering, Chapter 5 in knowledge work. In both cases, the agentic loop is the same — observe, plan, act, check, report — and the human gate is the same — define the task, bound the tools, verify the output. What changes is the medium and the verification method. In engineering, the primary verifier is tests and diffs. In knowledge work, it is sources and review. Let's look at the engineering case first.

---

## Sources Used

- Saltzer, J. H. and Schroeder, M. D. "The Protection of Information in Computer Systems." *Proceedings of the IEEE*, 1975. https://web.mit.edu/Saltzer/www/publications/protection/
- OWASP. "Top 10 for LLM Applications 2025." https://owasp.org/www-project-top-10-for-large-language-model-applications/
- OWASP. "Top 10 for Model Context Protocol." https://owasp.org/www-project-mcp-top-10/
- Anthropic. "Configure permissions." *Claude Code Docs*. https://code.claude.com/docs/en/permissions [verify — current as of writing]
- Anthropic. "Use Claude Cowork safely." *Claude Help Center*. https://support.claude.com/en/articles/13364135-use-cowork-safely [verify — current as of writing]
- Anthropic. "Let Claude use your computer in Cowork." *Claude Help Center*, April 24, 2026. https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork [verify — current as of writing]
- Anthropic. "Use plugins in Claude Cowork." *Claude Help Center*, April 9, 2026. https://support.claude.com/en/articles/13837440-use-plugins-in-cowork [verify — current as of writing]
- AgenTRIM. "Tool Risk Mitigation for Agentic AI." *arXiv*, 2026. https://arxiv.org/abs/2601.12449
- VPI-Bench. "Visual Prompt Injection Attacks for Computer-Use Agents." *arXiv*, 2025/2026. https://arxiv.org/abs/2506.02456
- NIST. *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*. 2023. https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10
