# Chapter 4 — Claude Code as Agentic Engineering

## TL;DR

- Claude Code is not a smarter autocomplete. It is an agent that can read a codebase, plan across files, run commands, and change a working system.
- The user's role shifts from code requester to engineering supervisor: define the task, bound the permissions, review the plan, inspect the diff, run the tests, decide.
- Code has natural verification paths — tests, builds, linters, diffs — that make agentic engineering unusually tractable. Use them.
- The danger is not that the agent writes bad text. The danger is that it makes changes to a system you depend on.

---

## Opening Scene

A developer pastes a stack trace into a chat window, asks for a fix, copies the suggested code, and drops it into the affected file. The code compiles. The error disappears in the log. Two days later, an edge case that the fix silently broke reaches a user.

This is not an agent failure. It is a workflow failure. The human skipped the step where the fix is run against the actual codebase, tested against the failing case and several adjacent ones, and diffed against the original to understand exactly what changed. Chat produced a plausible artifact. Plausible is not tested.

Claude Code changes this workflow by moving the agent inside the repository. It can read the actual files, run the actual tests, see the actual failure, and show you an actual diff. That is a genuine capability gain. It also means the agent is operating on a system that matters, with tools that can change it. The supervision requirements go up, not down.

---

## What This Chapter Lets You Do

By the end of this chapter you can:

- Explain the difference between snippet generation and agentic repository work.
- Define a bounded task with acceptance criteria that an agent can act on.
- Review a plan before authorizing execution.
- Understand what permissions an engineering agent requires and which to restrict.
- Use tests and diffs as the primary verification method.
- Decide when to accept, when to ask for revision, and when to stop.

---

## What Claude Code Is

Claude Code is a command-line AI agent that operates inside a development environment [verify — current as of writing]. Unlike a chat interface that generates code for you to paste elsewhere, Claude Code can:

- Read files across a repository
- Edit multiple files in a single task
- Run shell commands — tests, builds, linters, scripts
- Report what it changed and why

This puts it squarely inside the agentic loop described in Chapter 2: it observes the repository state, forms a plan, acts through tool calls (file reads, file writes, command execution), checks its own work, and reports. The ReAct architecture's core insight applies here — reasoning and acting interleave (Yao et al., 2023). Each observation updates the plan; each action produces new observations. An agent investigating a bug may read one file, infer it needs to read another, run a reproduction command, update its hypothesis, and edit only after several inspection rounds.

The Anthropic documentation describes this explicitly: Claude Code works by reading context from the codebase, using tools to inspect and modify it, and running commands as needed to verify its work (Anthropic, "How Claude Code works"). This is not text generation with extra steps. It is agentic action.

---

## The Engineering Action Surface

Returning to Chapter 3's framework, a coding agent's action surface includes:

| Agent action | Risk level | Required gate |
|---|---|---|
| Read files | Privacy and secrets exposure | Scope repository or folder; exclude secrets |
| Edit files | Behavioral change in a working system | Diff review before merge |
| Run tests | Low–moderate | Command approval if new to environment |
| Install packages | Supply-chain risk | Human approval |
| Access credentials | High | Avoid; use governed secrets management |
| Deploy to production | Very high | Human-only or organizational gate |
| Delete files or databases | Very high | Human-only; prefer copies and staging |

The stable principle from Saltzer and Schroeder (1975) applies to coding agents exactly as it applies elsewhere: grant the minimum set of capabilities the task requires. A bug fix does not require deployment credentials. A documentation update does not require database write access. A refactor does not require production environment access.

Anthropic's permission documentation covers how Claude Code requests and handles permission for file operations and shell commands, and how users can configure policy to control what is approved automatically versus what requires per-action confirmation [verify — current as of writing] (Anthropic, "Configure permissions"). The OWASP LLM Top 10 includes excessive agency as a core risk category (OWASP, 2025): an agent that can do more than the task requires is an agent whose errors can propagate further.

---

## The Issue-to-PR Workflow

The most instructive way to understand agentic engineering supervision is to follow a bounded task from problem statement to decision point. Here is a worked walkthrough of an issue-to-merge workflow.

**Step 1: Define the issue and acceptance criteria.** The human writes what is broken, what the correct behavior should be, and how to confirm it. Vague scope ("fix the login bug") is not enough. Concrete scope includes: what input produces the wrong output, what the expected output is, and what test or demonstration confirms the fix is correct.

**Step 2: Bound the permissions.** Before the agent starts, the human decides: which repository, which folders, which commands, and what is off-limits. Secrets should not be in scope. Production systems should not be in scope. If the project includes a secrets file, exclude it explicitly.

**Step 3: Review the plan.** Before any file is edited or command is run, Claude Code produces a plan: which files it will inspect, what it expects to find, how it proposes to fix the problem, and what it will do to verify the fix. This plan is the human gate. Read it. Ask whether it covers the scope correctly. Ask whether it proposes to touch anything outside the stated issue. A plan that reaches further than the issue is a prompt for a conversation, not authorization.

**Step 4: Authorize bounded edits and commands.** When the plan is acceptable, the agent proceeds. For high-risk commands — installing packages, running migration scripts, modifying configuration — require explicit approval per action rather than batch authorization.

**Step 5: Run verification.** When the agent reports completion, verify with the means appropriate to the task: run the tests, run the build, run the linter. HumanEval-style evaluation (Chen et al., 2021) makes a foundational point the chapter needs to generalize: code should be evaluated by execution, not by whether it looks right. A fix that passes the failing test but breaks an adjacent behavior is not a fix. Run the full test suite, not only the targeted case.

**Step 6: Inspect the diff.** Read what changed. The diff is the complete record of the agent's action on your system. If lines changed that were not discussed in the plan, ask why. If the diff is larger than the problem scope warrants, that is a warning sign. Accept based on what the diff says, not based on what the agent's explanation says.

**Step 7: Merge or reject.** The human makes the merge decision. This is not a formality. Reflexion-style self-evaluation (Shinn et al., 2023) shows agents can reason about their own work and revise — but self-reflection is not a substitute for external test evidence. Agents may be confidently wrong. The tests and diff are the evidence; the agent's explanation is a hypothesis about why its changes are correct.

---

## Secrets, Credentials, and Deployment

Two categories of access require special treatment.

**Secrets and credentials.** Coding agents read files. If secrets, API keys, database passwords, or private keys are in the repository or in files the agent can read, they are inside the action surface. The safe posture is to exclude secrets directories and credential files explicitly from the scope, use a .gitignore-style exclusion or folder separation, and never ask the agent to work with authentication credentials as part of a task (Anthropic, "Claude Code security") [verify — current as of writing].

**Deployment and production access.** An agent that can run commands can, in principle, run deployment commands. Unless your workflow explicitly requires it and has organizational approval, deployment should not be part of an agentic coding task. The appropriate boundary is: staging and test environments are acceptable; production environments require a separate, human-authorized gate (Anthropic, "Configure permissions") [verify — current as of writing].

---

## The Human Gate in Engineering

The research on AI-assisted developer productivity (Peng et al., 2023) shows that AI coding assistance can improve throughput on well-defined tasks — but the gains are task-dependent, and the verification burden does not disappear. A faster path to a wrong answer is not progress.

In the agentic engineering model, the human's role is:

- Write the issue clearly enough that the acceptance criteria are testable.
- Set the permission boundary before the agent starts.
- Read the plan before authorizing action.
- Verify with tests and diff, not with the agent's description of success.
- Make the final accept or reject call.

This is engineering supervision, not engineering delegation. The agent handles the investigation and editing; the human owns the outcome.

---

## Common Misconceptions

**"Claude Code is just chat that writes code."** Chat generates text for you to apply elsewhere. Claude Code operates inside the repository and can edit and run things without a paste step. The action surface is different and the supervision requirements are different.

**"A green test means no review is needed."** Tests check what they test. A fix can pass a targeted test while introducing a regression elsewhere. Review the full test suite, not the focused test, before merging.

**"A good plan means a good change."** Plans are proposals. The plan tells you what the agent intends; the diff tells you what it did; the test results tell you whether it worked. All three matter.

**"The agent should decide the scope."** Scope is a human decision. If the agent's plan reaches beyond the stated issue, the human narrows it. The agent does not define its own permission boundary.

**"Permissions slow down real work."** Permissions slow down the first occurrence of a class of action. They prevent irreversible mistakes that are much slower to correct than the few seconds of approval overhead.

**"Generated code is less risky if it compiles."** Compilation is a syntax check. Correctness, security, and behavioral preservation require tests and review. Code that compiles and fails is still a failure.

---

## Try This

**Exercise 1: Write an issue as acceptance criteria.**
Take a bug or small task from your current work (or invent a plausible one). Write it as an agent-ready task packet: what is broken, what the correct behavior is, which files are in scope, which are not, and what test or demonstration would prove the fix is correct. Compare your draft with what you would normally write in a ticket. What is different?

**Exercise 2: Diff review.**
Look at a recent code change — one you made, one a colleague made, or one from an open-source project. Read the diff without reading the commit message first. Identify: What changed? Does the scope match what you would expect from the description? Is there anything in the diff that was not in the stated purpose of the change? Practice this exercise so that diff review feels like reading, not inspection of alien text.

---

## What Would Change My Mind

This chapter's conservative stance — bounded tasks, mandatory tests, human merge decision — would relax if test coverage in a codebase were complete and if the agent's ability to detect and report edge cases were reliable. Neither condition is routine. If agentic coding systems develop reliable self-auditing that catches behavioral regressions even outside the targeted test case, the case for full automated merge strengthens. Until then, tests prove what they test; the human sees the rest.

---

## Still Puzzling

Where is the right boundary between autonomous fix and human-merged fix? For well-tested, high-coverage codebases with very low-stakes components, automated merge on passing tests may be defensible. For any code that touches user data, money, authentication, or production state, the case for human review is strong. The field has not converged on a principled tiering, and the answer likely varies by organization and domain. The conservative default — human merge decision — is not a claim that autonomy is never appropriate; it is a claim that the current state of the tools and verification methods does not reliably support it in general.

---

## Bridge to Chapter 5

Code has a property that makes supervision tractable: it has an oracle. A test either passes or fails. A build either compiles or errors. This makes verification relatively clear compared to knowledge work, where the output is a document, a summary, or a reorganized folder. Chapter 5 applies the same agentic loop to that harder verification problem — and shows that the principles transfer even when the oracle is human judgment rather than a test suite.

---

## Sources Used

- Anthropic. "Claude Code overview." *Claude Code Docs*. https://code.claude.com/docs [verify — current as of writing]
- Anthropic. "How Claude Code works." *Claude Code Docs*. https://code.claude.com/docs/en/how-claude-code-works [verify — current as of writing]
- Anthropic. "Configure permissions." *Claude Code Docs*. https://code.claude.com/docs/en/permissions [verify — current as of writing]
- Anthropic. "Claude Code security." *Claude Code Docs*. https://docs.claude.com/en/docs/claude-code/security [verify — current as of writing]
- Chen, M. et al. "Evaluating Large Language Models Trained on Code." *arXiv*, 2021. https://arxiv.org/abs/2107.03374
- Peng, S. et al. "The Impact of AI on Developer Productivity: Evidence from GitHub Copilot." *arXiv*, 2023. https://arxiv.org/abs/2302.06590
- Yao, S. et al. "ReAct: Synergizing Reasoning and Acting in Language Models." *ICLR*, 2023. https://arxiv.org/abs/2210.03629
- Shinn, N. et al. "Reflexion: Language Agents with Verbal Reinforcement Learning." *NeurIPS*, 2023. https://papers.nips.cc/paper_files/paper/2023/hash/1b44b878bb782e6954cd888628510e90-Abstract-Conference.html
- OWASP. "Top 10 for LLM Applications 2025." https://owasp.org/www-project-top-10-for-large-language-model-applications/
- Saltzer, J. H. and Schroeder, M. D. "The Protection of Information in Computer Systems." *Proceedings of the IEEE*, 1975. https://web.mit.edu/Saltzer/www/publications/protection/
