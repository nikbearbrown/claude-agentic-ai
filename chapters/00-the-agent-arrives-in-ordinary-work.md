# The Agent Arrives in Ordinary Work

**Capability built:** Recognize why agentic AI changes the user's responsibility.

---

## A Tuesday Afternoon

It starts simply enough. You have a folder of quarterly reports from three departments, a deadline before end of day, and no time to read forty-three PDFs. You open Claude, describe the task, and tell it to pull the key numbers into a summary table.

You come back twenty minutes later. There is a table. It looks right. The formatting is clean. The numbers appear reasonable. You feel relieved.

Then you notice a figure that looks off — a revenue total that does not match what you remember from the finance call. You check the source document. The agent had read the correct file but misread a row: it confused a subtotal for a grand total. Every downstream figure in the table is wrong.

The artifact was fluent. The work was wrong. And you almost sent it.

This scenario is not unusual, and it is not primarily a story about AI failure. It is a story about a user who delegated work without designing supervision. The agent had access to files, produced plausible output, and reported completion. No step in that sequence was designed to catch a misread row.

This book is about designing the steps that catch the errors — before the output leaves the screen.

---

## What This Chapter Lets You Do

After this chapter, you will be able to:

- Explain in plain terms why agentic AI is different from a chatbot
- Name the three-part operating rule that governs all agentic work in this book
- Identify at least one concrete surface where Claude agents can take action in ordinary workflows
- Recognize why more capability creates more supervisory responsibility, not less

---

## The Shift: From Generated Content to Delegated Action

For most of AI's public history, the user relationship with an AI system was conversational. You asked; it answered. It produced text, and you decided what to do with that text. The AI had no reach into the world beyond the response on your screen. If the answer was wrong, the cost was the time you spent acting on it. The AI itself had not moved anything.

That relationship has changed.

Modern AI systems — and Claude in particular — can now be given tools. A tool, in this context, is a capability that lets the system act on something outside the conversation: read a file, write a file, run a command, search the web, fill a spreadsheet, open a browser, use an application. When an AI system has tools, it is no longer just producing text. It is operating in an environment. It can change the state of things.

When a system can change the state of things, the user's relationship to that system changes fundamentally. You are no longer evaluating a response. You are supervising a process that is reaching into your work, your files, your connected services, and potentially your colleagues' work.

This is what the research community calls an **agent**: a system that can observe a context, form a plan, use tools to act, check the results, and report back (Tang et al., 2023; Li et al., 2024). The observation-action-feedback cycle is what distinguishes an agent from an answering machine.

Claude Code and Claude Cowork are Anthropic's concrete implementations of this idea for everyday use [verify — current as of writing]. Claude Code can inspect a codebase, run tests, edit files, and report the results of those changes (Anthropic, "Claude Code overview"). Claude Cowork can work across documents, spreadsheets, and browser sessions — gathering, transforming, and producing artifacts in a file system you own (Anthropic, "Get started with Claude Cowork"). Both systems can do things that persist after the conversation ends. That is the operative difference.

---

## Agents Are Not Magic Autonomy

The word "agent" can mislead. It sounds like the system is self-directing, autonomous, operating on its own initiative. That is not what a useful agent is. A useful agent is a system that can execute delegated work within defined boundaries, with human supervision at key points.

The analogy is closer to delegation than to independence. When you delegate work to a capable colleague, you do not simply hand them the task and disappear. You describe the scope, you tell them what they can and cannot do, you agree on how they will check with you if something unexpected comes up, and you review the result before it goes out. The colleague's capability does not reduce your responsibility; it changes the form your responsibility takes.

An agent works the same way. You define what it can observe. You define what it can do. You require it to surface its plan before acting. You review what it changed. You verify the output. The agent's capability can be large — and Claude Cowork operating in computer-use mode, where it can see and interact with the desktop, is genuinely powerful (Anthropic, "Let Claude use your computer in Cowork") [verify — current as of writing]. But the capability does not replace your judgment. It relocates your judgment: upstream, into design; and at checkpoints, into verification.

The automation research literature has known this for decades. Lisanne Bainbridge described it precisely in 1983: the more capable the automated system, the more demanding the supervisory role becomes, not less (Bainbridge, "Ironies of Automation," 1983). More automation creates new monitoring demands, new failure modes, and new intervention responsibilities. Parasuraman, Sheridan, and Wickens formalized this further: autonomy is a design variable, and the human role changes — but does not disappear — at every level (Parasuraman, Sheridan, and Wickens, 2000). These findings apply directly to AI agents.

---

## The Control Triad: Scope, Approval, Verification

This book builds everything on three concepts. They appear in every chapter. They apply to every agentic workflow. They are the answer to the question: what does a user need to do differently when AI can act?

**Scope** is the boundary you draw before the agent starts. What files can it read? What can it write? What services can it touch? What is outside the task? Scope is not just about safety — it is about quality. An agent given too broad a scope will attempt things it is not equipped to handle, and the resulting errors will be harder to trace. An agent given a clear scope can be supervised more precisely.

**Approval** is the checkpoint where the human decides whether the planned action should proceed. This may happen before the first action, between major steps, or both. It is not a formality. It is the point where you read the plan, assess whether the proposed steps match the task, and decide whether the agent should proceed, revise, or stop. Approval is not a final polish; it is part of the control system.

**Verification** is the discipline of checking whether the output is correct, complete, and trustworthy — not just whether it looks finished. A verified output has been checked against its sources, tested for accuracy in at least a sample, and compared against the expected result. Verification is not the same as reading over something. It is the discipline of asking: what would have to be true for this to be wrong, and did I check that?

These three — scope, approval, verification — are the operating rule of this book. Every chapter will add detail to one or more of them. But they are stated here, at the beginning, because they apply from the first task forward.

The Anthropic help documentation for using Cowork safely articulates the same principle at the product level: real risk surfaces include files, apps, browser, plugins, MCP servers, scheduled tasks, and computer use, and each requires considered access decisions (Anthropic, "Use Claude Cowork safely"). The triad provides the framework for making those decisions across any surface.

---

## Where Agents Work in Ordinary Practice

Agentic AI is not primarily a tool for specialized technical work. It arrives in ordinary professional work: report assembly, data extraction, file organization, research compilation, document drafting, code maintenance. Here are four examples that will recur throughout this book:

**Code repair.** Claude Code observes failing tests, edits the relevant files, reruns the tests, and reports the diff. The human defines what the issue is, approves the proposed changes, and reviews whether the fix works without breaking something else.

**Report assembly.** Claude Cowork reads source documents in a designated folder, extracts relevant facts, and builds a draft memo. The human confirms which sources are authoritative, checks for omissions, and verifies any figures before the memo is sent.

**Spreadsheet extraction.** Claude Cowork reads a set of PDFs and populates a data table. The human checks the row count matches the source documents, samples a subset of cells against the originals, and confirms the extraction schema was applied correctly.

**Browser workflow.** Claude Cowork opens pages from a defined list of trusted sources to gather information. The human specifies which domains are in scope, confirms that no external-facing actions were taken, and checks the source list in the output.

Each of these workflows involves the agent doing real work that saves real time. Each requires the human to design scope before the work starts and to verify the output before it is used. The agent's value comes from doing the execution. The human's irreducible contribution is judgment: defining the boundary, reading the plan, and verifying the result.

**The human-only zone.** Not every task belongs to an agent. An agent should not send legal advice, delete production data, submit a grant application, or access protected health information without explicit governed approval from someone accountable for those decisions. This book is about supervised delegation, and supervision includes the decision not to delegate.

---

## The Plan Is Not the Work

One misconception deserves to be named early. When an agent presents a plan — a sequence of steps, a proposed tool sequence, a structured outline of what it intends to do — that plan can look like evidence that the agent understands the task. It is not.

The planning research literature makes this clear: planning in LLM-based agents is a useful output to inspect and can catch errors before they happen, but it is not a guarantee of execution quality (Liang et al., 2024). An agent can produce a plausible plan and still read the wrong file, misapply a formula, skip a step under an unusual condition, or confidently report completion when it failed partway through. The plan is a proposal, not a proof.

This applies to the reader's supervision practice: do not approve a plan because it sounds reasonable. Read the plan against the actual scope. Check whether the steps match the task. Ask what would happen if one of the middle steps returned an unexpected result. The plan is useful as a checkpoint, not as a substitute for verification after action.

Lucy Suchman's foundational work on situated action supports exactly this caution: plans are schematic approximations of action, not fully determined scripts (cited in Tang et al., 2023). The situated details of real files, real error messages, and real edge cases will not have been in the plan. Verification after action is irreplaceable.

---

## Common Misconceptions

**"Agentic means autonomous."** Autonomy is a spectrum and a design variable, not a binary. An agentic system can take real actions in the world and still operate within tight boundaries, with human approval at every consequential step.

**"If the agent has a plan, it knows what it is doing."** A plan is a structured proposal. It can be wrong about context, order, tools, edge cases, or dependencies. The plan is a checkpoint to read and assess, not proof of competence.

**"More tools always means better performance."** More tools expand the action surface and the failure surface equally. Each additional tool is an additional way for the agent to act in ways you did not intend (Li et al., 2024).

**"Human review is a final polish step."** Review is part of the control system. It happens before action (at the plan), during action (at approval gates), and after action (at verification). Leaving it only to the end is the design that lets wrong answers into the world.

**"Agents are mainly for programmers."** Claude Code is built for technical workflows, but Claude Cowork brings agentic capabilities to document, file, spreadsheet, and browser workflows that do not require programming.

---

## Exercises: Try This

**Exercise 1: Audit a recent delegation.**
Think of a task you have recently asked an AI assistant to complete. Answer three questions: What did you tell it about scope? Did you review a plan before action? Did you verify the output against the sources? Where, specifically, could an error have entered undetected?

**Exercise 2: Name your human-only boundary.**
For a domain of work you own — a project, a document set, a data set, a workflow — write a one-sentence scope statement for what an agent could be given access to, and a one-sentence statement for what must remain human-only. Keep both sentences specific.

---

## What Would Change My Mind

This book argues that supervised delegation is the right model for agentic AI in professional work. That argument would need revision if:

- AI systems demonstrated reliable independent verification — meaning they could catch their own factual, logical, and contextual errors without human checking at a rate that exceeded human error rates. Current evidence does not support this.
- Liability for agentic AI errors shifted fully to the system vendor. Current legal and professional frameworks hold humans accountable for delegated work.
- The tasks in question were so low-stakes and fully reversible that verification costs exceeded the cost of any potential error. For those narrow cases, lighter supervision is defensible.

For the workflows in this book — professional documents, code, data extraction, file management — the case for human supervision remains strong.

---

## Still Puzzling

A few questions this book does not definitively answer:

- How much of the agent's internal reasoning should users be able to inspect, and does more transparency actually improve supervision, or does it just create more to process?
- Where is the boundary between a tightly constrained agentic workflow and a sophisticated automation script? At what point does an agent become a pipeline?
- As verification tools improve — linters, test suites, source-comparison tools — will human verification remain as central, or will some verification steps migrate back to the machine?

---

## Bridge to Chapter 1

This chapter established that agentic AI is different from chat because it acts in the world. The next question is more precise: not just that agents act, but what makes a system an agent rather than a chatbot or an assistant, and how that distinction changes what you need to do as a user.

Chapter 1 draws the taxonomy.

---

## Sources Used

- Anthropic, "Claude Code overview," Claude Code Docs. https://code.claude.com/docs
- Anthropic, "Get started with Claude Cowork," Claude Help Center. https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork
- Anthropic, "Use Claude Cowork safely," Claude Help Center. https://support.claude.com/en/articles/13364135-use-cowork-safely
- Anthropic, "Let Claude use your computer in Cowork," Claude Help Center, April 24, 2026. https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork
- Bainbridge, Lisanne. "Ironies of Automation." *Automatica*, 1983. https://doi.org/10.1016/0005-1098(83)90046-8
- Li, Xinzhe et al. "A Review of Prominent Paradigms for LLM-Based Agents: Tool Use, Planning, and Feedback Learning." arXiv, 2024. https://arxiv.org/abs/2406.05804
- Liang, Wenliang et al. "Understanding the Planning of LLM Agents: A Survey." arXiv, 2024. https://arxiv.org/abs/2402.02716
- Microsoft Research. "Guidelines for Human-AI Interaction." CHI 2019. https://www.microsoft.com/en-us/research/project/guidelines-for-human-ai-interaction/publications/
- Parasuraman, R., Sheridan, T. B., and Wickens, C. D. "A Model for Types and Levels of Human Interaction with Automation." 2000. https://pubmed.ncbi.nlm.nih.gov/11760769/
- Tang, Xiangru et al. "A Survey on Large Language Model based Autonomous Agents." arXiv, 2023. https://arxiv.org/abs/2308.11432

---

*Tags: #claude #agentic #ai #supervision #scope #verification #delegation #Medhavy*
