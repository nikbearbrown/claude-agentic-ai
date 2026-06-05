# Chapter 10 — Designing Human Approval Gates

## TL;DR

- An approval gate is not a permission dialog. It is a decision. To make a real decision, you need to know: what action, on what target, for what reason, at what risk, with what reversibility, and what evidence to check afterward.
- Gate design has two failure modes: too few gates let dangerous actions through; too many create fatigue that turns gates into theater.
- Classify actions by risk and reversibility before the agent starts. Place gates at the right points in the agentic loop, not at every step.
- Four gate responses: approve, redirect, pause, stop.

---

## Opening Scene

A prompt appears in the corner of a researcher's screen: "Claude wants to run a command. Allow?"

She clicks Allow without reading further. She has clicked it forty times in the last two days. Each time, the task completed fine. Each time, she does not know what command ran.

This is a gate. It is not functioning as one.

A gate that is always clicked is not supervision. It is a ritual. It reduces the human's legal exposure ("I was asked") while providing none of the actual protection gates are designed for: catching wrong actions, scope creep, and irreversible consequences before they happen.

This chapter teaches gate design, not gate presence. The question is not whether the dialog appeared. The question is whether the human understood what they approved.

---

## What This Chapter Lets You Do

After this chapter, you can:

- Define what information a functional approval gate must contain
- Classify tasks by risk and reversibility to determine gate placement
- Map gates across the five phases of an agentic workflow
- Apply four gate responses: approve, redirect, pause, stop
- Identify the difference between human-in-the-loop and human-only

This chapter is the operational payoff of Chapter 9. Failure modes tell you what can go wrong. Gate design tells you where to stand to catch it.

---

## What an Approval Gate Actually Is

An approval gate is a moment in the agentic workflow where execution pauses and the human decides whether to continue, revise, or stop.

It is not:
- A dialog box the user dismisses
- A trust signal ("the agent asked, so it must be okay")
- A plan review at the start that covers everything afterward
- A final check after consequential action has already occurred

It is:
- A real decision point, with enough information to decide
- Tied to a specific action, not a general workflow approval
- Placed before the action takes effect, not after

Parasuraman, Sheridan, and Wickens (2000) established a foundational model for human-automation interaction that distinguishes where in a decision sequence the human is involved: in information acquisition, analysis, action selection, or action execution. An approval gate can sit at any of these points. The question is which point matters most for the specific risk.

For agentic AI, the highest-value gate placement is usually action selection — before the agent decides to use a specific tool — and action execution — before that tool call fires. Reviewing information the agent gathered is less critical than reviewing what it plans to do with that information.

---

## The Information a Gate Requires

A gate that contains only "Allow?" is not a gate. It is a speed bump.

A functional approval gate must tell the human:

1. **What action** the agent wants to take (delete, send, move, run, submit, write, call)
2. **What the target is** (which files, which address, which command, which API, which record)
3. **Why the agent thinks this action is needed** (connection to the task)
4. **What the risk is** (what could go wrong if this action is wrong)
5. **Whether it is reversible** (can it be undone, and how easily)
6. **What to check afterward** (what evidence to inspect to confirm the action was correct)

This is the gate prompt the research recommends and that Chapter 9 previewed:

> "Before you do this, state the exact action, target files or tools, why it is needed, what could go wrong, whether it is reversible, and what evidence I should inspect afterward."

A gate that includes that information gives the human the material needed to approve, redirect, pause, or stop. A gate that omits most of it collapses into ritual.

The Microsoft Research CHI 2019 guidelines on human-AI interaction identify related requirements: users need to know what the system is doing (status visibility), why (explanation), what went wrong if it fails (correction path), and how to take back control (dismissal and override). These are not interface preferences; they are what makes a gate function as supervision rather than performance.

---

## Classifying Work Before Placing Gates

Not every action needs the same gate. The goal is not gate maximalism — placing gates at every step — but gate appropriateness: placing them where the action's risk and irreversibility warrant human decision.

The classification has two axes.

**Risk axis:** What is the consequence if this action is wrong? Risk is roughly proportional to blast radius — how many things are affected — and sensitivity: financial, personal, regulatory, reputational, or relationship consequences.

**Reversibility axis:** If this action is wrong, how hard is it to undo? Reversibility is not binary. Some actions are fully reversible (drafts that are not sent), some are partially reversible (files in a backup), some are practically irreversible (emails sent to a large list, records submitted to a regulatory system, database deletions without backup).

Place the two axes in a simple grid:

| | Low risk | High risk |
|---|---|---|
| **Reversible** | Light gate (review before use) | Approval gate (explicit sign-off) |
| **Irreversible** | Approval gate (explicit sign-off) | Human-only (agent may prepare; human initiates) |

The most important category is the lower right: irreversible, high-risk actions are not candidates for agent execution, even with approval. They belong to a class called **human-only**: the agent can draft, prepare, or recommend, but the human is the one who presses send, submits the form, or executes the command. The approval is not "allow the agent to do this"; it is "I am doing this; the agent prepared it."

This distinction matters because approval fatigue and automation bias (Chapter 9) make rubber-stamping likely in long workflows. If the human clicks Allow on a high-risk irreversible action, the gate has failed. Designing the action as human-initiated removes the rubber-stamping risk entirely.

---

## The Gate Matrix

| Action type | Example | Gate type |
|---|---|---|
| Drafting | Memo text, report section, email draft | Review before use |
| Transforming a copy | Spreadsheet cleanup on a duplicate | Approve copy; verify counts and formulas |
| Editing source files | Code changes, document revisions | Approve edits; review diff |
| Running a command | Tests, installs, scripts | Approve specific command before execution |
| Moving or deleting | Folder reorganization, archive cleanup | Backup required; explicit approval per action |
| External action | Email send, form submit, API call with effects | Human-only final action |
| Sensitive data | Health, finance, student, client records | Organizational approval before any access; otherwise human-only or use synthetic/redacted data |

This table encodes risk-reversibility classification into action types. Use it to classify the actions in any planned agentic task before the agent starts [verify — current as of writing as tool interfaces evolve].

---

## Mapping Gates Across the Agentic Loop

The agentic loop has five phases where gates apply:

**1. Tool and permission approval (before the task starts)**

Which tools does the agent have access to for this task? Every enabled tool is a potential action channel. The Anthropic Claude Code permissions system, for example, allows users to set tool allowlists — specifying which commands and file operations the agent can execute automatically versus which require explicit approval (Anthropic, Claude Code Docs) [verify — current as of writing]. Cowork safety guidance similarly distinguishes which connectors, apps, file scopes, and external actions require user confirmation (Anthropic, Claude Help Center, 2026) [verify — current as of writing].

This is a design gate, not an action gate. Its question is: does the agent need all of these tools for this task, or can we reduce the tool surface before starting?

**2. Plan approval (before execution begins)**

The agent proposes a plan: steps, tools, order of operations, expected outputs. This is the right moment to review the plan against the task's risk classification and catch scope problems, missing steps, or unwarranted tool use before any action occurs.

Plan approval does not cover later changes. If the scope, tool, target, or risk changes during execution, a new gate is required. A common error is treating plan approval as a blanket authorization for the session.

**3. Action approval (before high-risk or irreversible actions execute)**

This is the gate most people picture when they hear "human-in-the-loop." For low-risk reversible actions in an approved plan, this gate can be lightweight or waived — the agent proceeds within defined bounds. For actions that are irreversible or that change scope, the gate fires with full information.

Claude Code's permission tiers [verify — current as of writing] implement a version of this: some operations run automatically within the session's defined permissions; others pause and require explicit user confirmation; others are blocked entirely.

**4. Verification gate (after action, before use)**

The agent has acted. Before the output is used — sent, published, merged, submitted, applied — the human verifies it against the pre-defined evidence criteria. The verification gate is not optional on consequential work. This is the check that catches plausible summaries, silent omissions, and fabricated completion claims (Chapter 9) before they leave the workflow.

**5. External-effect gate (before the output reaches outside the system)**

Sending, publishing, submitting, merging to production, or sharing with a third party. This gate is always human-initiated for anything irreversible or external-facing, regardless of how good the prior verification looked. Cowork safety guidance (Anthropic, 2026) specifically identifies browser form submission and external app actions as requiring this level of control [verify — current as of writing].

---

## Four Gate Responses

Approval gates are decision points, and decisions have more than two options.

**Approve:** The action is consistent with the task, the target is correct, the risk is acceptable, and the reversibility is understood. Continue as planned.

**Redirect:** The action is on the right track but something is wrong: wrong target, wrong scope, wrong tool, wrong output format, output that failed verification. Give the agent a revised instruction and let it try again before the next gate.

**Pause:** You do not have enough information to approve or redirect. The agent needs to provide more detail — a fuller log, a source list, a completed inventory — before the decision can be made. This is not a stop; it is a request for more evidence.

**Stop:** The task is unsafe, unverifiable, outside sanctioned scope, or the risk has changed since the plan was approved. Stop execution. The agent does not proceed. You determine whether and how to re-scope before trying again.

The research on overreliance (Stanford SCALE Initiative, 2025; Springer AI & Society, 2025) suggests that approval gates default toward approve in ordinary use, especially when the agent has been reliable and time pressure is present. Designing gates to make redirect, pause, and stop equally natural — not just available but prompted — reduces approval drift.

One design move that helps: build redirect and stop into the gate UI or prompt at the same level as approve. If the only visible button is "Allow," the other responses require extra effort and will be underused.

---

## Worked Walkthrough: The Folder Cleanup

A communications director wants to reorganize three years of project folders. She asks her agent to propose a new folder structure, identify files to archive, and flag duplicates.

**Risk-reversibility classification:** Moving and deleting files is irreversible without a backup. Some files may be shared with external collaborators. Risk is moderate; reversibility is low.

**Gates she designs:**

1. **Tool gate (before start):** Agent gets read access to folders and write access to a staging folder only. No delete access. No access to shared drives.

2. **Plan gate:** She asks the agent to produce a proposed folder map and a list of files flagged for archiving, with reasons for each flag. She reviews this list before any files move.

3. **Action gate:** Each batch of moves — not each file — requires her approval. She reviews each batch's contents, confirms the destination, and gives explicit approval per batch.

4. **Human-only deletion:** The agent never deletes. It moves files to a staging folder labeled "PENDING-DELETE." She makes the final deletion decision herself after reviewing the staged files.

5. **Verification gate:** After each batch moves, she checks that the file count in the destination matches the expected count. She spot-checks three files per batch to confirm they opened correctly.

**Result:** The reorganization takes longer than a fully automated approach. She catches one batch where the agent had included an active client file in the archive list because the client name matched an older project. The design prevented that from executing automatically.

This is not a worst-case scenario with a near miss. It is ordinary agentic task design. The gates did not catch a dramatic failure; they provided the human decision points that make the work supervisable.

---

## The Human Gate: Knowing Consequences

Approval gates require human expertise, and the expertise is not technical. It is consequential: knowing what the action would mean if it went wrong.

The agent may know how to click, delete, or submit. The human decides whether that action should happen. This is what Bainbridge (1983) identified as the core problem of automation: routine automation makes human expertise atrophy, so the moment when a human is most needed — when the system reaches the edge of its scope — is exactly when the human is least practiced at intervening.

Approval gates are one design response to Bainbridge's irony. By placing real decisions at real points in the workflow, they keep the human practiced at evaluating the agent's actions, even when most of those decisions are straightforward approvals. The habit of genuine evaluation does not survive workflows where every gate is "Allow without reading."

NIST's AI Risk Management Framework (2023) codifies a related principle: risk-tiered governance means that high-stakes, irreversible, or regulated actions require qualitatively different oversight than low-stakes, reversible work. Gate design is the mechanism through which that principle becomes practice.

OWASP's guidance on excessive agency (2025) recommends that agentic systems request only necessary permissions, avoid storing sensitive information beyond immediate need, and follow least-privilege principles in tool access. Approval gates are the enforcement layer for those principles: the human at the gate is the one who can actually say no.

---

## Common Misconceptions

**"Approval means I trust the agent."** Approval means the action is consistent with the task as you understand it at that moment. Trust in the agent's general competence is separate from the judgment that a specific action on a specific target is correct.

**"Clicking Allow is supervision."** Clicking is not supervision. Supervision is the deliberate evaluation of what is being proposed against what should happen. A gate that is clicked without reading provides no protection.

**"Only destructive actions need gates."** Sending, publishing, and submitting are often not destructive in the narrow sense — they do not delete anything — but they are irreversible and external-facing. The gate classification should include irreversibility and external-effect, not only data destruction.

**"A plan approval covers all later changes."** Plans change during execution. If the scope expands, the tool set changes, or the target shifts from what was approved, a new gate is required. A plan approval covers what was in the plan, not what the agent later decides is necessary.

**"Human-in-the-loop equals safe."** Being in the loop is a precondition for supervision, not a guarantee of it. Rubber-stamping a gate is being in the loop. It is not supervision. Safety comes from genuine evaluation at genuine gates.

**"High-risk work is okay if the agent asks first."** Asking first is necessary but not sufficient. For irreversible, high-blast-radius, or regulated actions, asking is the minimum. The question is whether the human can make a real decision from what they were shown, and whether the action class belongs in agent execution at all or in the human-only category.

---

## Try This

**Exercise 1: Gate design for a task you already run**

Choose one agentic task you have run or plan to run. Classify each significant action in the task using the risk-reversibility grid. For each action that falls in the "approval gate" or "human-only" category, design the gate: what information will you require before approving? Write out the gate prompt you would use.

Then run the task using the gate design you specified. Did any gate provide information that changed your decision? Did any gate reveal something you had not expected?

**Exercise 2: Redesign a weak gate**

Find a workflow — yours or a described one — where the only gate is "Allow?" or equivalent. Redesign it: what action, what target, what risk, what reversibility, what post-action evidence should this gate display? What would you need to see to redirect or stop rather than approve?

---

## What Would Change My Mind

This chapter recommends human-only as the gate classification for irreversible, high-risk actions. I would revise this if controlled research showed that well-informed approval gates — with full action, target, risk, and reversibility information — produced genuinely different human decisions than human initiation, and that those decisions were reliably correct. Current evidence on automation bias (Stanford SCALE Initiative, 2025; Springer AI & Society, 2025) suggests the opposite: approval gates on high-stakes actions collapse toward approval, especially under time pressure. Human-only initiation changes the action's risk profile in a way that gate design cannot fully replicate.

I would also reconsider the five-phase gate structure if agentic platforms developed reliable, practitioner-accessible scope containment that reduced the need for action-level gates — for example, provably sandboxed execution where no external action can fire without explicit invocation of a separate, non-agentic send mechanism. That would shift the gate design burden from the user to the platform.

---

## Still Puzzling

Approval fatigue in longer agentic workflows is not well understood. Research on automation bias gives us the overall pattern; it does not tell us precisely when gates begin to function as rubber stamps, or which design interventions restore genuine evaluation most reliably. The field of human factors in automation has relevant methods, but they have not been systematically applied to knowledge-work agentic systems.

The relationship between individual gate practice and team gate policy also needs development. Individual practitioners can design gates for their own work; team governance requires shared classification frameworks, shared gate prompts, and shared expectations about which actions require organizational approval rather than individual approval. Chapter 11 takes up that question.

---

## Bridge to Chapter 11

Individual approval gate design is where supervised delegation becomes personal practice. You know your tasks, your risks, and your tolerance for agent action.

When multiple people use the same agents, shared workflows, or shared data — and when the consequences of agent actions extend beyond one person's work — gate design becomes team policy. Chapter 11 examines how agentic AI works inside teams and organizations, and how individual supervision habits translate into shared governance.

---

## Sources Used

1. Parasuraman, Sheridan, and Wickens, "A Model for Types and Levels of Human Interaction with Automation," 2000. https://pubmed.ncbi.nlm.nih.gov/11760769/
2. Bainbridge, "Ironies of Automation," Automatica, 1983. https://doi.org/10.1016/0005-1098(83)90046-8
3. Microsoft Research, "Guidelines for Human-AI Interaction," CHI 2019. https://www.microsoft.com/en-us/research/project/guidelines-for-human-ai-interaction/publications/
4. NIST, "Artificial Intelligence Risk Management Framework (AI RMF 1.0)," 2023. https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10
5. Anthropic, "Configure permissions," Claude Code Docs. https://code.claude.com/docs/en/permissions
6. Anthropic, "Use Claude Cowork safely," Claude Help Center. https://support.claude.com/en/articles/13364135-use-cowork-safely
7. Anthropic, "Let Claude use your computer in Cowork," Claude Help Center, April 24, 2026. https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork
8. OWASP, "Top 10 for LLM Applications 2025." https://owasp.org/www-project-top-10-for-large-language-model-applications/
9. OWASP, "Top 10 for Model Context Protocol." https://owasp.org/www-project-mcp-top-10/
10. Stanford SCALE Initiative, "Overreliance on AI: Literature Review." https://scale.stanford.edu/ai/repository/overreliance-ai-literature-review
11. Springer AI & Society, "Exploring automation bias in human-AI collaboration: a review and implications for explainable AI," 2025. https://link.springer.com/article/10.1007/s00146-025-02422-7

---

## AI Wayback Machine

**Run this:**

```
Who was James Reason, and how does his Swiss cheese model of accident causation connect to the approval gate design we covered in this chapter? Keep it to three paragraphs. End with the single most surprising thing about his career or ideas.
```

→ Search **"James Reason Swiss cheese model"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to map each layer of the Swiss cheese model onto one of the five gate phases in this chapter.
- Ask it whether the Swiss cheese model suggests gates should be redundant or sequential, and why that distinction matters for agentic workflows.

What changes? What becomes more precise? What becomes harder to argue?
