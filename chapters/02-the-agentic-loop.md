# The Agentic Loop

**Capability built:** Trace observe, plan, act, check, and report in a Claude workflow.

---

## What Happens When No One Is Watching

A project manager asks an agent to compile a competitive analysis from five industry reports in a shared folder. The agent starts immediately. It reads the first two files, produces a draft structure, fills in sections from memory rather than from the remaining three files it has not yet read, generates fluent summaries, and reports completion.

The output looks complete. The formatting is professional. Several of the competitor names are correct. But two sections describe companies that were not in the source documents. One figure is fabricated. One competitor has been given the wrong product line.

The manager forwards the document to her director.

What went wrong here is not primarily an AI accuracy problem. It is a loop problem. The agent skipped the observation step for three of five files. It filled in missing context from training data rather than from the designated sources. It did not check whether its output matched the sources. It reported completion as if the work were done.

An agent with a well-designed loop would have read all five files before drafting, flagged the files it could not open, cited the specific passage for each claim, noted where a section had insufficient source coverage, and held the report for human review before calling it done.

The loop is not a feature of the AI system. It is a discipline of the workflow. This chapter teaches you how to see it, how to trace it, and how to interrupt it when it is going wrong.

---

## What This Chapter Lets You Do

After this chapter, you will be able to:

- Describe the five stages of the agentic loop: observe, plan, act, check, report
- Identify where errors enter the loop and how they compound across stages
- Map the loop onto Claude Code and Claude Cowork workflows
- Place human intervention points at each stage
- Distinguish self-checking from external verification

---

## The Loop: Five Stages

The agentic loop is a cycle. The agent goes around it once for a simple task, and multiple times for a complex one. Each iteration uses the observations and results from the previous one to refine the next. The stages are:

**Observe.** The agent takes stock of what is available: the task instructions, the files in scope, the output of a previous tool call, the error message from a failed step, the partial result of a completed one. Observation is the foundation. An agent that observes badly — reads the wrong file, works from stale context, misses a key constraint in the instructions — will plan badly regardless of how capable the planning step is.

**Plan.** The agent forms a sequence of steps: which tools to use, in what order, with what inputs. Planning may be simple (a single edit to a single file) or complex (a multi-stage research and synthesis task with dependencies between steps). The plan is the artifact the human should see before action begins. It is a proposal, not a commitment.

**Act.** The agent executes a step: reads a file, writes a file, runs a command, calls a tool, opens a browser page. Each action changes something — or attempts to. The action surface is where the real-world consequences of the agent's work appear.

**Check.** The agent examines what happened: did the tool return expected output? Did the test pass? Does the draft match the sources it drew from? Does the row count in the extracted table match the document? Checking can include the agent's own self-review, but — critically — self-checking is not independent verification. The agent may find some errors this way. It will not find all of them, because it cannot compare its output against ground truth it does not have access to.

**Report.** The agent describes what it did, what changed, what succeeded, and what is uncertain. A good report is evidence, not decoration. It includes the specific files touched, the tests run and their results, the sources cited, and any steps that were ambiguous or incomplete. A report that says "completed successfully" without evidence is a red flag, not a green light.

This cycle — observe, plan, act, check, report — is the practical mental model for supervising any agentic Claude workflow. It applies to Claude Code bug repairs, Cowork document assembly, spreadsheet extraction, and browser research.

---

## Research Foundations: ReAct and Reflexion

Two lines of research shaped how practitioners think about the agentic loop.

The ReAct framework, from Yao et al. (ICLR 2023), introduced the idea of interleaving reasoning and action. Rather than planning once and executing, the agent alternates: it reasons, acts, observes the result, reasons again about what just happened, and acts again. This is more like a skilled human doing research — adjusting the approach based on what each step reveals — than a pipeline executing in sequence. ReAct showed that connecting reasoning to real-world feedback improved performance substantially over either pure reasoning or pure reaction.

The Reflexion framework, from Shinn et al. (NeurIPS 2023), extended this to the self-checking stage. An agent that receives feedback from a failed attempt can turn that feedback into language and use it as additional context for the next attempt. This is useful: an agent that failed a test and can articulate why it failed is in a better position than one that simply retries blindly. Reflexion also illustrates the limit of self-checking: the agent's self-critique is only as good as its understanding of the failure. An agent that misdiagnosed the cause of a failed test will write a revised plan that targets the wrong fix.

Both frameworks are now embedded in how Claude Code and Cowork operate, even if users never see the label (Anthropic, "How Claude Code works") [verify — current as of writing]. The practical consequence for users is this: the loop exists whether you design it or not. The question is whether you have built in human intervention points, or whether the loop is running without them.

---

## The Loop in Claude Code: A Bug Repair

Here is a concrete trace of the loop in a Claude Code workflow (Anthropic, "Claude Code overview").

**Observe.** The user describes a bug: a function that intermittently returns wrong values when the input list is empty. Claude Code reads the relevant source file, locates the function, reads related test files.

**Plan.** Claude Code proposes a plan: inspect the function's branch logic, identify the path that handles empty input, draft a one-line fix, run the associated test suite.

**Human gate.** The user reads the plan. Is the function it has identified actually the source of the bug? Are the tests it plans to run the right ones? Does the scope include any files that should not be touched? The user approves, redirects, or corrects before action begins.

**Act.** Claude Code edits the function. One line changes. The edit is logged.

**Check.** Claude Code runs the test suite. Three tests pass. One test that was previously flaky now reliably passes. No new failures.

**Report.** Claude Code presents a diff — the exact change made, the line numbers, the before and after — along with the test output. It notes that the intermittent failure appears resolved based on the test run, but that production behavior should be verified with a broader test case.

**Human verification.** The user reads the diff. The change is what was proposed. The test output matches. The user decides whether to accept the change, add another test case, or investigate further before committing.

The loop ran once for a simple bug. For a more complex issue, it would run multiple times — each cycle using the result of the last to refine the approach.

---

## The Loop in Claude Cowork: A Document Assembly

Here is the same five-stage trace applied to a knowledge-work workflow (Anthropic, "Get started with Claude Cowork").

**Observe.** The user asks Cowork to assemble a section-by-section summary from eight source documents in a designated folder. Cowork reads the folder listing, opens each document, and notes which files it can access and which are empty or formatted in a way it cannot read.

**Plan.** Cowork proposes a structure: an introduction pulled from the first two documents, three analytical sections corresponding to themes in the middle group, and a conclusions section from the final report. It lists which source documents map to which sections.

**Human gate.** The user reviews the proposed structure. Are the sections the right ones? Does the source mapping make sense? Is the theme identification correct? The user may correct misattributions or redirect the structure before action begins.

**Act.** Cowork drafts each section, drawing specific passages from the identified sources. It creates an output document in the user's designated folder.

**Check.** Cowork reviews the draft against its source list: are the citations present? Are the page or paragraph references included? Does the section on topic X draw from the document identified as the source for topic X?

**Report.** Cowork presents the draft with a source list — which document contributed to which section — and flags two sections where the source documents had conflicting numbers, noting that a human should review which figure is authoritative.

**Human verification.** The user opens two or three source documents and spot-checks specific figures against the draft. The user reads the flagged conflict sections and makes a judgment call. The user checks whether any sensitive information from a confidential document was included in a section that will be distributed publicly.

This is supervised delegation working as intended. The agent does the execution. The human does the judgment. Both are necessary.

---

## Where Errors Enter the Loop

The loop reveals failure architecture. Errors do not appear randomly — they enter at specific stages, and they compound as the loop continues.

**Errors at observe.** The agent reads the wrong file. It works from an earlier version of a document. It cannot open one of the five required source files and proceeds without flagging the gap. It misreads an instruction and thinks the task scope includes files it should not touch. These errors propagate into the plan before anything has been done, and they may never be caught if the report is read at the summary level rather than the detail level.

**Errors at plan.** The agent proposes steps in the wrong order, creating a dependency failure later. It selects a tool that is not suited to the data format. It breaks a complex task into too few steps and misses a case. It plans to modify a file that should be read-only. These errors are catchable at the human gate — which is why the plan review matters.

**Errors at act.** The tool returns an error that the agent does not notice or report. The file write partially succeeds, leaving a corrupted file. The command runs with insufficient permissions and silently fails. The browser request times out and the agent substitutes a guess. These errors may or may not surface in the check stage.

**Errors at check.** The agent self-checks against its own output rather than against the source. It finds no inconsistencies because it is the same system that generated both the output and the comparison. It marks a step as complete when it succeeded conditionally. It does not check the cases the user most needs checked.

**Errors at report.** The agent presents a confident summary that omits the two steps that failed or returned unexpected results. It reports test passage without noting that one test was skipped. It says "completed" without listing the files it touched or the sources it used. The user reads the summary and assumes verification has been done.

The planning survey literature organizes these failures under task decomposition, plan selection, tool use, self-reflection, and memory — and treats each as a research problem (Liang et al., 2024; Li et al., 2024). For the user, the practical takeaway is simpler: read the plan before action, read the report for evidence, and do not assume the check stage was adequate.

| Loop stage | Failure | Human intervention |
|---|---|---|
| Observe | Missing or stale context | Add or correct context before plan |
| Plan | Wrong order, wrong scope, wrong tool | Review and revise plan before approval |
| Act | Tool overreach, silent failure, permission error | Deny permission; require explicit error reporting |
| Check | Weak or absent evidence; self-comparison | Require source citations, test results, row counts |
| Report | Overconfident completion, missing uncertainty | Ask for uncertainty flagging and action log |

---

## Self-Checking Is Not Verification

This distinction deserves its own section because it is the most commonly misunderstood.

When an agent checks its own output — reviewing a draft, running internal consistency tests, reflecting on whether the plan was followed — that is self-checking. It is useful. It can catch some errors.

It is not independent verification. An agent checking its own output is working from the same context that produced the output: the same interpretation of the sources, the same understanding of the task, the same implicit assumptions. Reflexion (Shinn et al., 2023) showed that self-critique improves performance on some benchmarks, but it also showed the limits: an agent that misunderstood the task will often produce self-critique that misdiagnoses the problem.

Independent verification means checking the output against something external to the agent's reasoning: the actual source documents, the test results produced by an independent test suite, the row count in the original data, the expert judgment of a human who knows the domain.

The Microsoft Research Guidelines for Human-AI Interaction (CHI 2019) frame this as a design principle: systems should support user verification, not substitute for it. A report that includes citations, diffs, test outputs, and uncertainty flags supports user verification. A report that says "all done" does not.

---

## The Human Gate in the Loop

The loop has natural intervention points. The human's job is to be present at them, not to watch passively while the agent runs to completion.

**Before the plan is approved.** This is the highest-leverage point. The human reads the proposed steps, checks the scope, confirms the tool selection, and decides whether the agent should proceed. A bad plan stopped here costs nothing. A bad plan executed and discovered at the report stage costs the time and effort of the entire run — plus whatever state the agent has already changed.

**During multi-step execution.** For complex tasks with multiple planning-action cycles, the human should have the opportunity to interrupt between cycles. If the agent's intermediate result looks wrong — the wrong theme was identified, the wrong file was prioritized — the human should be able to correct context before the next cycle begins.

**At the report.** The human reads not the summary but the evidence: the diff, the source list, the test output, the flagged uncertainties. The report is not the end of the process. It is the information the human needs to make a judgment about whether the work is complete.

Parasuraman, Sheridan, and Wickens (2000) describe this as the intervention architecture of automation: the human can intervene at plan selection, execution approval, monitoring, and result evaluation. Each point has different leverage and different cost. The plan stage is cheap to intervene in and high-leverage. The report stage is expensive to undo if the wrong actions have already been taken.

NIST's AI Risk Management Framework (2023) treats this at the organizational level: map the risks, measure the impacts, manage with controls, document the process. The loop framework translates that into operational practice: map the stages, measure the checkpoints, manage through human gates, document through the report.

---

## An Interrupted Loop

Not every loop should run to completion. Here is what it looks like to interrupt one.

The user asks Claude Code to refactor a module to improve performance. Claude Code observes the module, reads its tests, and proposes a plan that includes deleting six functions it has identified as unused.

The user reads the plan. Three of the six functions are used in a configuration file that Claude Code did not read — they were outside the scope it was given. Deleting them would break a production workflow.

The user does not approve the plan. The user corrects the context: tells Claude Code about the configuration file, asks it to re-observe with that file included, and requests a revised plan.

Claude Code re-observes, revises the plan. The six deletions are reduced to two. The user approves. The refactor proceeds safely.

The interruption cost ten minutes. The uninterrupted version would have broken production. The loop is designed to be stopped.

---

## Common Misconceptions

**"The plan is the work."** The plan is a proposal. It does not execute itself, and it does not guarantee that the execution will match the proposal. Plans can be correct and execution can still go wrong if a tool fails, a file is unavailable, or an edge case appears.

**"If an agent checks itself, the output is verified."** Self-checking can catch some errors. It cannot substitute for external verification against ground truth — the actual source documents, the test suite, the original data. An agent checking its own output is still a single party's view.

**"Tool output is always interpreted correctly."** Agents can misread tool output — interpreting a partial result as a complete one, misidentifying an error code as a success signal, misunderstanding a data format. This is why the report stage must include the actual tool output, not just the agent's interpretation.

**"A failed tool call means the agent failed completely."** Failures in the loop are recoverable, especially if they are reported. An agent that cannot open a file should say so. A step that fails should not cause the agent to fabricate the result as if the step succeeded. Failure handled correctly is better than silent failure handled incorrectly.

**"The human only matters at the final report."** The plan-approval gate is where errors are cheapest to catch. Intervention during multi-step execution is where mid-course correction is possible. Waiting until the final report to engage means accepting whatever the loop produced.

---

## Exercises: Try This

**Exercise 1: Trace a loop you have already run.**
Think of a recent AI-assisted task that involved more than answering a question — something where an agent used files, created output, or ran steps. Map it onto the five-stage loop: observe, plan, act, check, report. At which stages did you see what the agent was doing? At which stages were you working from summary rather than evidence?

**Exercise 2: Design the human gates.**
Choose a task you would like to delegate to Claude Code or Cowork. Write down the five stages of the loop for that specific task. At each stage, write a one-sentence description of what you would need to see or do to maintain supervision. Identify which stage you consider highest-risk for your task.

**Exercise 3: Spot the failure.**
Read the following report summary and identify which loop stage most likely failed: "Task complete. The competitive analysis has been assembled from available sources. The document is ready for review." What is missing from this report? What would you ask the agent to provide before you accepted it?

---

## What Would Change My Mind

This chapter argues that the observe-plan-act-check-report cycle is the right mental model for supervising agentic work. That framing would need revision if:

- Better transparency mechanisms emerged — not just reasoning traces but genuinely inspectable action logs — that allowed users to verify loop execution without relying on the report. If the loop became fully auditable in real time, the report would be less critical.
- Self-checking improved substantially — specifically, if agents demonstrated reliable detection of their own context gaps and planning errors at rates that exceeded current human review. That would shift the balance between self-check and external verification.
- Agent architectures changed in ways that broke the sequential cycle — for instance, massively parallel sub-agents working independently — in which case the linear five-stage model might need to become a graph rather than a loop.

Until then, the five-stage cycle is the right frame for practitioners.

---

## Still Puzzling

- How much of the loop should be visible to the user? Some users benefit from seeing every tool call; others are overwhelmed by it. Is there a reliable way to calibrate the right level of transparency for different users and tasks?
- Reflexion-style self-correction is useful but fallible. Are there types of tasks or error patterns where agent self-correction reliably works, versus types where it reliably fails, and can practitioners use that distinction in practice?
- As multi-agent systems become more common — where one agent orchestrates others — how does the loop model need to extend? The chapter describes single-agent loops; orchestration may require a different supervision architecture.

---

## Bridge to Chapter 3

The agentic loop tells you what happens between task start and report. The next question is what the agent is allowed to reach when it acts. Chapter 3 opens the action surface: which tools, which permissions, and which limits are the right ones for the work you are delegating.

---

## Sources Used

- Anthropic, "Claude Code overview," Claude Code Docs. https://code.claude.com/docs
- Anthropic, "Get started with Claude Cowork," Claude Help Center. https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork
- Anthropic, "How Claude Code works," Claude Code Docs. https://code.claude.com/docs/en/how-claude-code-works
- Li, Xinzhe et al. "A Review of Prominent Paradigms for LLM-Based Agents: Tool Use, Planning, and Feedback Learning." arXiv, 2024. https://arxiv.org/abs/2406.05804
- Liang, Wenliang et al. "Understanding the Planning of LLM Agents: A Survey." arXiv, 2024. https://arxiv.org/abs/2402.02716
- Microsoft Research. "Guidelines for Human-AI Interaction." CHI 2019. https://www.microsoft.com/en-us/research/project/guidelines-for-human-ai-interaction/publications/
- NIST. "Artificial Intelligence Risk Management Framework (AI RMF 1.0)." 2023. https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10
- Parasuraman, R., Sheridan, T. B., and Wickens, C. D. "A Model for Types and Levels of Human Interaction with Automation." 2000. https://pubmed.ncbi.nlm.nih.gov/11760769/
- Shinn, Noah et al. "Reflexion: Language Agents with Verbal Reinforcement Learning." NeurIPS 2023. https://papers.nips.cc/paper_files/paper/2023/hash/1b44b878bb782e6954cd888628510e90-Abstract-Conference.html
- Yao, Shunyu et al. "ReAct: Synergizing Reasoning and Acting in Language Models." ICLR 2023. https://arxiv.org/abs/2210.03629

---

*Tags: #claude #agentic #ai #loop #observe #plan #act #check #report #supervision #ReAct #Reflexion #Medhavy*
