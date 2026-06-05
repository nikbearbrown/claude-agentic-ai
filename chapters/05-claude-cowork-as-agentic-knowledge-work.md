# Chapter 5 — Claude Cowork as Agentic Knowledge Work

## TL;DR

- Claude Cowork brings agentic AI to non-engineering work: files, documents, folders, apps, and browser sources.
- The agentic loop is identical to the engineering case; what changes is the verification method. Tests and diffs become source checks, row counts, and human review.
- A polished output is not a verified output. The capable user defines the task packet before work starts and checks claims, sources, omissions, and privacy before using the result.
- Cowork is well-suited to repetitive, multi-step, document-heavy work. It is poorly suited to tasks that require tacit judgment, involve confidential data without governance, or produce external-facing actions the human has not reviewed.

---

## Opening Scene

A program manager asks an AI agent to prepare a briefing from the past month's project documents — meeting notes, status updates, email summaries, and a few draft memos. The output arrives in twenty minutes: cleanly formatted, reasonable headings, confident bullet points. The manager shares it with leadership before reading it carefully.

Three things went wrong. The report attributed a decision to a person who had only proposed it; the final decision was never made. It dropped the one dissenting memo entirely. And it drew on a document that was clearly labeled DRAFT — NOT FOR DISTRIBUTION, which happened to be in the same folder as the others.

The output was fluent. The workflow failed. Not because the agent lied, but because "polished" and "correct" are different properties, and the manager treated the first as evidence of the second.

This chapter shows what a supervised Cowork workflow looks like instead.

---

## What This Chapter Lets You Do

By the end of this chapter you can:

- Explain what makes Cowork an agentic system rather than a document editor.
- Build a task packet that bounds what the agent can access and what it must produce.
- Apply the access hierarchy: connectors before browser before computer use.
- Identify which knowledge-work tasks are well-suited to agentic automation and which are not.
- Use a verification checklist designed for document and data outputs.
- Decide whether a Cowork output is ready to use or needs revision.

---

## What Claude Cowork Is

Claude Cowork is an agentic AI environment for desktop knowledge work [verify — current as of writing]. Where Claude Code operates in a repository with shell commands and tests, Cowork operates in the space where most professional work happens: files, folders, documents, spreadsheets, browser sources, connected services, and the applications on your computer.

Cowork can:

- Read files in a folder you designate
- Create or edit documents, spreadsheets, and other file types
- Use connected services through plugins and MCP connectors
- Browse web sources
- Interact directly with applications on your desktop through computer use
- Execute scheduled tasks without your presence

This is not a document editor that uses AI for suggestions. It is an agent with a tool set and an action surface. The Anthropic documentation frames it explicitly: Cowork brings Claude Code-level agentic capability to noncoding desktop workflows (Anthropic, "Get started with Claude Cowork") [verify — current as of writing].

The agentic loop from Chapter 2 operates unchanged: Cowork observes the files and context you provide, forms a plan, acts through tool calls, checks its progress, and reports. The differences from Claude Code are in the medium (documents instead of code) and in the verification method (human review instead of a test suite).

---

## The Knowledge-Work Action Surface

Cowork's access types follow the same ladder described in Chapter 3, with a few knowledge-work-specific notes:

| Cowork access type | What it can expose or change | Risk level | Default rule |
|---|---|---|---|
| Uploaded or attached file | Contents of that file | Moderate | Use copies; review for sensitive content |
| Designated folder | Every file in scope | Moderate–high | Use a dedicated working folder |
| Connector / plugin | Service data and actions | High | Scope narrowly; inspect before enabling |
| Browser | Web pages, forms, logins | High | Trusted public sources only |
| Computer use | Any visible app or content | High | Use only with explicit scope |
| Scheduled task | Unattended repeated actions | High | Low-risk only; review output cycle |

The opening scene's failure was a folder-access failure. When the agent could read everything in the folder, it read everything — including the draft memo marked not for distribution. The fix is simple: a dedicated working folder containing only the documents cleared for this task.

---

## The Task Packet

Effective Cowork supervision starts before the agent acts. A **task packet** is the set of decisions the human makes in advance:

**Working folder.** Which specific folder, and what is in it? The folder should contain copies of approved files, not originals. Files outside the task scope should not be in the folder.

**Allowed files.** Are all files in the folder in scope, or only named ones? If the folder contains anything that should not be read (drafts, personal files, confidential data), remove or exclude them before starting.

**Forbidden files and actions.** What should the agent not touch? This includes files containing personal data, regulated information, credentials, or anything marked as draft or confidential unless it is explicitly part of the task.

**Output artifact.** What specific file or files should the task produce? A clear output specification prevents the agent from generating extra artifacts or overwriting existing ones.

**Source-log requirement.** Should the agent list which files it drew on for each section? For any report or summary that will be shared, a source map is the minimum verification aid. Without it, checking claims requires re-reading everything.

**Approval points.** Which steps require explicit human review before proceeding? For a multi-step task — extract, then draft, then format — define where the human checks before the next step runs.

**Verification checklist.** After the task completes, what specific checks will the human perform before using the output?

---

## Worked Example: Report from Approved Files

Here is a complete supervision trace for the briefing task from the opening scene, rebuilt correctly.

**Task definition.** The program manager creates a folder called `/project-briefing-working/` and copies only the finalized, distributable documents into it: meeting notes from three sessions, two official status updates, and one approved summary memo. The draft memo and anything marked confidential remain in the original location.

**Task packet.** Allowed: all files in `/project-briefing-working/`. Output: `briefing-draft.docx`. Source log: required (each section lists its source files). Forbidden actions: no browser, no external messages, no deletion. Approval point: review the outline before drafting begins.

**Plan review.** Cowork produces a proposed outline. The manager reads it. The outline includes a "pending decisions" section — which is correct. It does not include a section on the one dissenting view from the project. The manager adds an instruction: "Include a section on the dissenting position from the March 14 notes."

**Artifact review.** The briefing draft arrives. The manager works through the verification checklist:

- *Source map.* Each section lists the documents it drew from. The "pending decisions" section cites two meeting notes — the manager checks both and confirms the agent correctly identified one decision as pending rather than made.
- *Claims check.* The manager reads the attributed-decision claim. The source note points to a specific meeting note. The manager reads that passage: it was a proposal, not a decision. The claim is wrong. The manager corrects it before sharing.
- *Omissions.* The dissenting view is now present because the manager added it to the instructions. The manager checks that the draft represents it fairly rather than dismissing it.
- *Privacy check.* The source log lists the three meeting notes, two status updates, and the approved memo — all files that were cleared for the folder. No unlisted files appear.

**Decision.** The manager revises the attributed-decision claim, reviews the revision, and shares the corrected briefing.

This is more work than accepting the first output. It is less work than recovering from a wrong claim reaching leadership.

---

## The Access Hierarchy: Connectors, Browser, Computer

Cowork offers multiple ways to reach external information and services. The Anthropic documentation recommends a hierarchy: prefer connectors over browser access, and prefer both over direct computer use where the same task can be accomplished by a lower-risk path [verify — current as of writing] (Anthropic, "Let Claude use your computer in Cowork," 2026).

**Connectors and plugins** are the lowest-risk external access. They provide defined interfaces to services — calendar, project management tool, cloud storage — with bounded scope. Before enabling a connector, check what it can read and what actions it can take. A calendar connector that can read events is different from one that can create, modify, or delete them.

**Browser access** allows the agent to load and interact with web pages. For knowledge work, this means research from public sources. The risks include: the agent may reach sites you did not intend; web page content can contain adversarial instructions (VPI-Bench, 2026); login portals and form submissions are not appropriate targets for unattended browsing. Restrict browser tasks to named trusted sources, and prohibit any form submission, login, or purchase.

**Computer use** allows the agent to observe and interact with anything on the desktop: any app, any window, any visible content. This is the broadest access level and the hardest to scope. Computer-use tasks warrant the most conservative permission design and the closest output review. The AgentDojo research shows that agents using tools across files, browsers, and services face real adversarial risk from injected instructions in documents and web content (AgentDojo) — a risk that scales with the breadth of what the agent can see and do.

---

## What Cowork Does Well

Knowledge-work tasks that are well-suited to agentic automation share several properties: they are repetitive or structurally consistent, they involve multiple documents or data sources, the output has a definable form, and the human can verify the result without re-doing the task from scratch.

| Cowork task | Fit | Main risk | Verification |
|---|---|---|---|
| Report from approved files | Strong | Unsupported claims, omissions | Source map; claims check |
| Spreadsheet extraction from PDFs | Strong | Wrong rows, formula errors | Row counts; sample spot-check |
| Cross-document summary | Strong | Lost minority views, contradictions | Human reading of summary + sources |
| Meeting-note synthesis | Strong | Wrong commitments, wrong attribution | Human confirmation before sharing |
| Folder organization (on copies) | Moderate | Misfiled or misnamed items | Human review before touching originals |
| Slide deck from source packet | Moderate | Visual claims, confidential content | Human review of every slide |
| External message sending | Poor | Real-world consequence before review | Human-only; never delegate |
| Sensitive or regulated data processing | Poor without governance | Privacy, legal, and compliance risk | Approved systems and processes only |

The distinction between strong-fit and poor-fit tasks is the reversibility test from Chapter 3. Reports, summaries, and extractions can be revised before use. External messages and regulated-data actions cannot be undone.

---

## The RPA Context

Office automation is not new. Robotic Process Automation (RPA) systems have automated repetitive document and data tasks since the early 2010s, changing knowledge-worker roles in measurable ways (Lacity, Willcocks, and Craig, 2020). The shift with language-driven agentic AI is that task specification changes: instead of programming every step in a workflow, a user can describe the goal and let the agent plan and use tools.

That flexibility creates different risks than scripted RPA. A scripted workflow does exactly what it was programmed to do. An agentic workflow improvises when it encounters something unexpected. Improvisation is not always wrong — it is sometimes exactly what makes flexible agents valuable. But improvisation within a broad action surface is where overreach happens. The task packet is the mechanism for converting flexible capability into bounded action (Kedziora, Siemon, and Kedziora, 2026).

---

## Scheduled Tasks and Unattended Action

Cowork supports scheduled tasks that run without your presence. The agentic properties remain; the supervision moment is compressed into the setup.

Before scheduling a recurring task:

- The task should be low-risk and reversible.
- The output should be something the human reviews before acting on.
- The folder and access scope should be as narrow as possible.
- There should be a regular review cycle — the human examines what the scheduled task has been doing, not just the most recent output.
- Unattended tasks should not send external messages, modify records, delete files, or interact with regulated data.

The Anthropic documentation on assigning tasks remotely supports the point that task delegation from a distance increases the supervision responsibility at setup time (Anthropic, "Assign tasks from anywhere in Claude Cowork") [verify — current as of writing].

---

## The Human Gate in Knowledge Work

The Microsoft Research guidelines for human-AI interaction identify transparency, recoverability, and appropriate calibration of trust as principles for AI-assisted work (Microsoft Research, 2019). In practice, the human gate for Cowork tasks has four moments:

**Before the task:** Define the task packet. Bound the folder. State the forbidden actions. Require the source log.

**Before each major step:** If the task is multi-phase, review the plan and the output of each phase before the next begins. Do not authorize drafting before reviewing the outline.

**After the task:** Run the verification checklist. Check sources, claims, omissions, and privacy before using the output.

**Before sharing or acting:** The final gate is the moment before the output leaves your control. If you are not certain the output is correct, do not share it.

The polished artifact is not the finish line. The finish line is a reviewed, verified output you are willing to put your name on.

---

## Common Misconceptions

**"Cowork is for people who do not need to think technically."** Cowork requires careful task definition, access boundary design, and substantive output verification. The supervision discipline is the same as for Claude Code; the domain is different.

**"A polished document means the workflow succeeded."** Fluency is not accuracy. Format is not correctness. The opening scene is a polished, correct-looking failure.

**"Computer use is just another connector."** Computer use gives the agent access to any visible application and content on your desktop. It is the broadest access level in the Cowork hierarchy.

**"Folder access is low risk."** A folder containing documents can also contain sensitive contracts, draft communications, confidential data, and personal information. The risk level of folder access depends on what the folder contains.

**"Meeting summaries can be shared without review."** Meeting summaries produced by an agent can misattribute statements, record proposals as decisions, omit dissenting views, and lose nuance. Always confirm commitments and attributions before sharing.

**"If Cowork made the file, it checked the file."** The agent produces an output. Verification is a separate step that the human performs. Production and verification are not the same.

---

## Try This

**Exercise 1: Build a task packet.**
Choose a multi-step document task from your work: assembling a report, synthesizing meeting notes, extracting data from several sources. Write a task packet for it: working folder, allowed files, forbidden files or actions, output artifact, source-log requirement, approval points, and verification checklist. What decisions did the task packet force you to make that you would have left implicit otherwise?

**Exercise 2: Verify an output.**
Take any AI-generated document — one you made, one from a colleague, or one from a public example. Apply the following checks: identify every claim that can be verified from the stated sources; find at least one claim that needs source confirmation; identify what the document does not include that a careful human reader would expect. What did the verification exercise reveal?

---

## What Would Change My Mind

This chapter's verification-first stance would soften for outputs where the stakes are low and the verification cost is high relative to the harm of an error. For internal working documents used as rough inputs to human judgment — draft outlines, exploratory summaries, first-pass extractions — the argument for exhaustive review before every use is weaker. The chapter's caution is strongest for outputs that will be shared, acted on, or used as the basis for decisions. If your Cowork output stays internal and tentative, lighter review is defensible. If it leaves your control, treat it as a claim that needs a source.

---

## Still Puzzling

How do nontechnical users reliably detect what an AI agent has omitted? Missing information is harder to catch than incorrect information, because there is nothing to point at. Research on how users supervise agentic office workflows and identify omissions in summaries is still limited (Research gap noted in Cowork research file). This is a real open problem for knowledge-work supervision: the omission may be the most consequential failure and the hardest to see.

---

## Bridge to Chapter 6

Chapters 3, 4, and 5 cover what an agent can do with its built-in tool surface. Chapter 6 asks what happens when that surface expands through MCP — the Model Context Protocol — which connects agents to external systems, databases, APIs, and services beyond what ships in the product. MCP changes the capability calculation and the permission calculation simultaneously. The same principles apply; the action surface grows in ways that require explicit review.

---

## Sources Used

- Anthropic. "Get started with Claude Cowork." *Claude Help Center*. https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork [verify — current as of writing]
- Anthropic. "Use Claude Cowork safely." *Claude Help Center*. https://support.claude.com/en/articles/13364135-use-cowork-safely [verify — current as of writing]
- Anthropic. "Let Claude use your computer in Cowork." *Claude Help Center*, April 24, 2026. https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork [verify — current as of writing]
- Anthropic. "Organize your tasks with projects in Claude Cowork." *Claude Help Center*. https://support.claude.com/en/articles/14116274-organize-your-tasks-with-projects-in-cowork [verify — current as of writing]
- Anthropic. "Assign tasks from anywhere in Claude Cowork." *Claude Help Center*. https://support.claude.com/en/articles/13947068-assign-tasks-to-claude-from-anywhere-in-cowork [verify — current as of writing]
- Lacity, M., Willcocks, L., and Craig, A. "Robotic Process Automation and Consequences for Knowledge Workers: a Mixed-Method Study." 2020. https://pmc.ncbi.nlm.nih.gov/articles/PMC7134300/
- Kedziora, D., Siemon, D., and Kedziora, D. "Identifying and Overcoming Challenges in Intelligent Process Automation." *California Management Review*, 2026. https://journals.sagepub.com/doi/10.1177/00081256261434509
- VPI-Bench. "Visual Prompt Injection Attacks for Computer-Use Agents." *arXiv*, 2025/2026. https://arxiv.org/abs/2506.02456
- AgentDojo. "A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents." https://agentdojo.spylab.ai/
- Microsoft Research. "Guidelines for Human-AI Interaction." *CHI*, 2019. https://www.microsoft.com/en-us/research/project/guidelines-for-human-ai-interaction/publications/
