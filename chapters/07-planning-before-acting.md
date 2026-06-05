# Chapter 7 — Planning Before Acting

## Opening Scene

A manager asks an agent to "clean up the project folder and make sure everything is organized." The agent begins. Twenty minutes later, she discovers that files have been moved into new subdirectories, several items she considers active are now in an "archive" folder, and one document — the one she was just about to edit — has been renamed. Nothing is gone. But everything is where she did not expect it, and she now has a secondary task: figuring out what happened and undoing what she did not want.

A simpler version of this failure happens continuously in agentic work: the instruction was clear enough to start, not clear enough to supervise.

A plan would have changed this. Not because a plan is a guarantee of good behavior, but because a plan is the first moment at which the agent's interpretation of the task becomes visible to the human before anything changes.

## What This Chapter Lets You Do

After reading this chapter you will be able to:

- Require an agent to produce a reviewable plan before any execution begins
- Evaluate a plan for goal fit, missing context, risky steps, and absent stop conditions
- Distinguish a good plan from a plausible-sounding one
- Apply the material-plan-change rule: if the plan changes during execution, the agent must ask again
- Connect the plan to the verification evidence required in Chapter 8

---

## Why Planning Is Not Obvious

The agentic loop — observe, plan, act, check, report — has a planning step built in. So does the ReAct architecture that underlies many current agentic systems: Reasoning and Acting are interleaved, with each action generating observations that feed the next round of reasoning (Yao et al., 2023). Planning happens whether or not you ask for it explicitly.

The problem is that planning without externalizing the plan is invisible. An agent may be working from a coherent internal sequence of steps, or it may be improvising from the first available tool call. The human cannot tell the difference unless the agent states the plan in language the human can review.

Requiring an explicit plan before execution is not adding bureaucracy. It is making the delegation visible before it acts.

---

## What a Plan Does

A plan is not a commitment. It is a proposal. It says: "Here is what I understand the task to be, what I will need to complete it, what I will do, in what order, and what I will not touch." Every element is something the human can inspect and correct before any action is taken.

Research on LLM agent planning suggests a practical taxonomy of what planning accomplishes (Liang et al., 2024):

**Task decomposition** breaks a complex goal into steps that can be reviewed individually. "Organize the project folder" becomes "inventory files, propose categories, create a backup copy, move items in groups, ask before archiving anything from the active list."

**Dependency order** exposes which steps must happen before others. If the agent needs to read a source document before writing a summary, that dependency should be explicit. If the agent is planning to create a backup before moving files, that sequence matters.

**Missing information identification** surfaces what the agent does not yet know. If the task requires access to a database the agent cannot yet reach, or a decision criterion that was never stated, the plan is the right place to flag that — not mid-task.

**Stop conditions** define when the agent should pause and ask rather than proceed. These are not signs of failure; they are deliberate safety points built into the plan.

**Verification evidence** names what will show the task is complete. Every plan should end with a statement of evidence. What test will pass? What count will match? What will be different in the right way?

---

## The Clarification Question Comes First

Good plans often start with a question.

Research on proactive language agents shows that when task information is incomplete, asking before forming an execution plan produces better outcomes than filling in the gaps silently (Ask-before-Plan, 2024). This is counterintuitive for users who experience clarifying questions as friction. The friction is the point.

When an agent asks "Do you want me to include archived folders in the cleanup, or only active project folders?" before proceeding, it has surfaced a scope boundary that was implicit in the instruction. The human now makes a decision that was previously invisible. That is supervision working as intended.

An agent that fills in missing information silently — deciding on its own what "organized" means, which files count as active, what the folder taxonomy should look like — is not being helpful. It is making scope decisions that belong to the human.

The rule is simple: underspecified task, clarifying question before plan.

---

## What a Good Plan Looks Like

Here is a plan produced by an agent given the instruction "prepare a summary report on our Q2 customer feedback files":

> I understand the goal as: a written summary of patterns across Q2 customer feedback, organized by theme.
>
> I need these inputs: the files in /projects/customer-feedback/Q2/ — I count 14 documents. I will not open files outside that folder or access the CRM system.
>
> I propose these steps:
> 1. Read each document and note the main themes and any specific complaints or compliments.
> 2. Group themes across documents.
> 3. Draft a summary organized by theme, with representative quotes.
> 4. Create a source map showing which quotes come from which files.
>
> I need approval before: creating any new files, sharing the summary outside this session, or accessing any systems beyond the files listed.
>
> I will verify by: confirming I read all 14 files, providing a word count for the summary, and listing the source map at the end.
>
> I will stop if: I encounter a document I cannot open, if the themes are contradictory in ways that require a business judgment I cannot make, or if I find documents outside the Q2 scope that seem relevant.

This plan is reviewable. A human can read it and identify: the right folder is named, the scope boundary is explicit, the steps are in a sensible order, and there is a stop condition and verification method. The human can also correct it before anything is read: "Include Q1 as well" or "Skip the quotes, just aggregate themes" or "You need CRM access — I'll approve that separately."

---

## What a Bad Plan Looks Like

Here is a different response to the same instruction:

> I'll read through the Q2 customer feedback files and prepare a comprehensive summary with actionable insights.

This is not a plan. It is a caption for a plan. It names the output but shows none of the inputs, steps, boundaries, or verification method. The human who approves this has not approved anything concrete — they have approved the agent's judgment about all of the questions the plan above made explicit.

Research on LLM planning limitations confirms that agents can produce confident-sounding plans that omit critical constraints, especially when those constraints are not salient in the initial instruction (Barriers in Planning, 2024). The agent is not lying. It is providing what it expects the user wants: an efficient, reassuring description of work about to happen. The human must learn to ask for more.

---

## The Plan Review Checklist

When an agent presents a plan, review it against these elements:

| Plan Element | Review Question |
|---|---|
| Goal | Does this match your actual objective, or a plausible-sounding substitute? |
| Inputs | Are the sources, files, or data named precisely and completely? |
| Tools | Is each tool necessary for this specific task? |
| Sequence | Are dependencies in the right order? Would any step fail if done before another? |
| Permissions | What requires explicit approval before the agent proceeds? |
| Reversibility | Which steps can be undone? Which cannot? |
| Stop condition | When should the agent pause and ask rather than continue? |
| Evidence | How will success be verified? Is the evidence method named? |

If the plan is thin on any of these, ask the agent to revise before proceeding. A plan that lacks stop conditions is a plan without brakes. A plan that lacks evidence is a plan without a completion criterion.

---

## Risk-Tiered Planning

Not every task needs the same plan depth. The research and the prior misconceptions suggest two failure modes: too little planning for high-risk tasks, and so much required structure for low-risk tasks that practitioners stop asking for plans at all.

A useful heuristic:

**Light plan** (low-risk, reversible, narrow): The agent names the goal, the specific inputs it will use, and what the output will be. No write access to external systems, no communication tools, no changes to shared resources.

**Standard plan** (moderate risk, some persistence): The agent provides the full plan template — goal, inputs, exclusions, steps, permissions, stop conditions, evidence. Write access is limited to a designated folder or sandbox. One tool class may require approval.

**Strict plan** (high risk, irreversible, or external-facing): The agent produces the plan, pauses for explicit approval before each action class, names approval requirements for every tool call involving external systems, and documents evidence requirements in advance. Changes to production systems, external communications, and financial records fall here.

Parasuraman, Sheridan, and Wickens (2000) characterized this as levels of human interaction with automation — the human may approve, modify, or veto plans before automated execution, and the right level depends on risk. The same logic applies here: the approval mechanism should match the consequence of error.

---

## The Material-Plan-Change Rule

Agents do not always follow the plan they stated. A tool fails. A file is missing. A new piece of context changes the apparent path to the goal. The agent adapts.

Adapting within the scope of the approved plan is appropriate. An agent that encounters a file formatted differently than expected and adjusts its parsing method is doing its job.

But when an agent changes the plan materially — uses a different tool, accesses a source not in the approved list, changes the destination of an output, alters the risk level of an action — it must stop and ask. Not report after. Ask before.

This rule is non-negotiable for high-risk tasks. The plan the human approved was specific. A materially different plan requires a new approval. Reporting a scope change after the fact is not transparency; it is an audit log, not supervision.

The practical instruction to give an agent: "If at any point you need to deviate from this plan in a way that changes the tools you use, the data you touch, or the risk level of an action, stop and tell me before proceeding."

---

## Worked Walkthrough: Folder Cleanup

Recall the opening scene. Here is the same task with a proper planning requirement.

**Instruction given:** "Clean up the project folder and make sure everything is organized."

**Agent response (first move):** "Before I proceed, I have a few questions: What counts as 'organized' — do you have a folder structure in mind, or should I propose one? Are there any files you'd like me to not move? What should I do with items that look inactive — propose them for archive, or leave them in place?"

**After clarification:** The agent produces a plan stating the target folder path, the proposed folder taxonomy, which items it will not touch without explicit approval, and the stop condition: "I will pause before moving any file that has been modified in the last 30 days or that I cannot classify confidently."

**Before any action:** The human reviews and adjusts: "Include files from the last 60 days in active, not 30. And don't rename anything — only move."

**Execution:** The agent now works within a bounded scope. Any item it is uncertain about is listed in a "review required" section rather than moved.

**After execution:** The agent produces a move log, a list of items it held for review, and the before/after folder structure.

This took longer to begin. It cost nothing that could not be recovered. The first version — immediate action from a vague instruction — required recovery work that was harder than the original task would have been with a plan.

---

## Common Misconceptions

**"A longer plan is a better plan."** Length is not quality. A plan that covers all eight elements in concise, specific language is better than a four-page list that still does not name the stop condition.

**"The agent's plan proves it understood."** A plan proves the agent has a coherent description of a path. It does not prove that path is correct, that the constraints are right, or that the agent will not encounter a situation its plan did not anticipate. The plan is a proposal, not evidence of comprehension.

**"Clarifying questions are inefficiency."** Missing information at the start of a task produces errors at the end. A clarifying question that takes two minutes is almost always cheaper than recovery work after a failed or misdirected execution.

**"If the first step is safe, the whole plan is safe."** Plans cascade. A first step that reads files may feed a second step that sends a message. Review the whole sequence.

**"Plans do not need verification steps."** A plan without a verification method is a plan without a completion criterion. The agent reports done; you have no method for checking. Build the evidence into the plan.

**"Changing the plan mid-task is harmless."** It may be harmless in low-stakes work. In anything involving write access, external systems, or shared resources, a mid-task plan change that was not re-approved is a supervision gap.

---

## The Human Gate: Before Execution Begins

The approval gate for planning is not a signature on a document. It is an active review against the plan checklist, followed by a deliberate decision: "I've read this plan, I've verified the scope matches my intent, and I'm approving this specific set of steps, tools, and permissions."

If you cannot say that — if the plan is too vague, too broad, or still missing stop conditions — the right move is to send the plan back for revision. The agent can revise a plan quickly. Undoing an action takes longer.

Roth et al. (2004), in research on mixed-initiative planning for UAV teams, found that effective human oversight depends on the human having clear levers to modify or veto plans before execution. For agentic AI, those levers are: the plan review, the clarifying question, the explicit approval, and the material-plan-change rule.

---

## Try This

**Exercise 1: Plan Analysis**
Give an agent an open-ended task instruction relevant to your work (e.g., "prepare a brief on the latest updates in our product category" or "organize the files in this folder"). When the agent responds, do not let it proceed. Instead, rate the response against the plan checklist: does it name inputs, steps, permissions, stop conditions, and verification evidence? Ask the agent to revise the plan until all eight elements are present.

**Exercise 2: The Bad Plan Rewrite**
Write a deliberately bad plan for a task you know well — one that sounds confident but leaves out scope boundaries, stop conditions, and evidence. Then rewrite it as a strict plan. Compare the two. What would have happened if the bad plan had run?

---

## What Would Change My Mind

The emphasis on explicit planning before execution would relax if:

- Agentic systems reliably surfaced all assumptions, scope decisions, and tool choices in a structured, reviewable format automatically — without being asked
- Research showed that implicit agent planning consistently produced better outcomes than explicit, human-reviewed plans in real workflow settings
- Stop conditions and material-plan-change rules became enforced structural features of the agentic runtime, rather than practices dependent on human instruction

None of those conditions currently hold, and the research on LLM planning limitations suggests they are some distance away (Barriers in Planning, 2024).

---

## Still Puzzling

- How much of the planning burden should the prompting infrastructure carry, versus what individual users must remember to require?
- At what level of task complexity does the plan itself become so long that meaningful review is impractical?
- How should teams standardize plan templates across different agent surfaces — Claude Code, Cowork, and MCP-connected tools — when the workflows are structurally different?

---

## Bridge to Chapter 8

A plan with a verification method is a plan that can be closed. A plan without one is a plan that ends when the agent says it does. Chapter 8 makes verification the center of the argument: not a final check, not a courtesy review, but the control system that makes the whole delegation safe to trust.

---

## Sources Used

- Liang, Wenliang et al. "Understanding the Planning of LLM Agents: A Survey." arXiv, 2024. https://arxiv.org/abs/2402.02716
- "Ask-before-Plan: Proactive Language Agents for Real-World Planning." Findings of EMNLP, 2024. https://arxiv.org/abs/2406.12639
- "Revealing the Barriers of Language Agents in Planning." arXiv, 2024. https://arxiv.org/abs/2410.12409
- Yao, Shunyu et al. "ReAct: Synergizing Reasoning and Acting in Language Models." ICLR 2023. https://arxiv.org/abs/2210.03629
- Shinn, Noah et al. "Reflexion: Language Agents with Verbal Reinforcement Learning." NeurIPS 2023. https://papers.nips.cc/paper_files/paper/2023/hash/1b44b878bb782e6954cd888628510e90-Abstract-Conference.html
- Parasuraman, R., Sheridan, T. B., and Wickens, C. D. "A Model for Types and Levels of Human Interaction with Automation." 2000. https://pubmed.ncbi.nlm.nih.gov/11760769/
- Roth, E. M. et al. "Human-in-the-Loop Evaluation of a Mixed-Initiative System for Planning and Control of Multiple UAV Teams." 2004. https://journals.sagepub.com/doi/pdf/10.1177/154193120404800301
- Microsoft Research. "Guidelines for Human-AI Interaction." CHI 2019. https://www.microsoft.com/en-us/research/project/guidelines-for-human-ai-interaction/publications/
- Anthropic. "Claude Code Overview." Claude Code Docs. https://code.claude.com/docs
- Anthropic. "Get Started with Claude Cowork." Claude Help Center. https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork
