# Claude Agentic AI
## Full TOC Draft - Tik TOC Architecture

**Working title:** Claude Agentic AI: A Practitioner's Guide to Supervised Agents  
**Author:** Humanitarians AI Incorporated  
**Publisher:** Humanitarians AI Incorporated  
**Document:** Full TOC Draft  
**Version:** 1.0  
**Status:** Architecture draft - ready for outline expansion and chapter drafting  

---

## Document Structure

1. Book Concept and Thesis
2. Learner Profile
3. Book Type and Deployment Specification
4. Field Positioning
5. Three-Act Learning Arc
6. Prerequisite Map
7. Chapter-by-Chapter TOC
8. Chapter Anatomy Template
9. Case Study Strategy
10. Hard Topics, Contested Claims, Aging Risk
11. Adoption Risk Register
12. Open Questions

---

# Part 1 - Book Concept and Thesis

## Book Concept Summary

This book teaches professionals, students, educators, and technical-adjacent builders how to understand and supervise agentic AI systems through the Claude ecosystem. It uses Claude AI, Claude Code, Claude Cowork, MCP, tool access, plans, approvals, and verification loops as the practical ground for learning what an agent is and how agentic work should be conducted. It succeeds when the reader can design a bounded agentic task, specify its tools and permissions, supervise execution, and evaluate whether the result is trustworthy.

## One-Sentence Logline

An AI agent is not magic autonomy; it is delegated action under constraints, and the capable human knows how to draw the boundary before the agent acts.

## Central Thesis

This book argues that agentic AI should be taught as supervised delegation, not autonomous replacement. Claude's agentic surfaces make the lesson concrete: Code can change a codebase, Cowork can act across files and workflows, and MCP can extend what a system can touch. Each new capability increases both usefulness and responsibility. The reader's job is to define the task, limit the tool surface, require approval, verify outputs, and retain accountability.

## Thesis Test

- Act One defines agentic AI by action, tools, memory/context, and approval boundaries.
- Act Two teaches task design, tool permissions, MCP, and verification loops.
- Act Three applies the discipline to work, research, coding, education, and organizational adoption.

**Thesis test:** Pass.

---

# Part 2 - Learner Profile

## Primary Reader

A technically curious professional or graduate student who has heard that "agents are the future" but needs a sober operational model. They may use Claude chat and may have seen demos of Claude Code or Cowork, but they do not yet know how to scope agentic work safely.

## Prior Knowledge Assumed

- Basic experience with Claude or another AI assistant
- Familiarity with documents, projects, and workflows
- Basic understanding that AI outputs can be wrong

## Prior Knowledge Not Assumed

- Agent architectures
- MCP servers
- Software engineering
- Enterprise AI governance
- Formal evaluation methods

## Prior Misconceptions

1. "Agentic means autonomous" - autonomy is bounded by tools, permissions, instructions, and approval gates.
2. "More tools make the agent better" - more tools expand the failure surface.
3. "The agent's plan proves it understands" - plans are proposals, not evidence.
4. "Human review is a final polish step" - review is part of the control system.

## Motivation Type

**Primary:** Professional and intellectual.  
**Secondary:** Technical upskilling.  
**Not primary:** Building custom frontier-agent infrastructure from scratch.

---

# Part 3 - Book Type and Deployment Specification

## Book Type

**Primary type:** Practitioner handbook.  
**Secondary type:** AI literacy text for advanced courses or professional development.  
**Not:** A research monograph or a framework-by-framework survey of agent architectures.

## Primary Adoption Context

Professional development workshops, AI strategy courses, graduate seminars, and team onboarding for people who need to work with agentic tools responsibly.

## Secondary Adoption Context

Courses in AI for work, computational skepticism, software design, education technology, and human-AI collaboration.

## What This Book Is Not Designed For

- Readers building custom agent frameworks from scratch
- Readers seeking vendor-neutral product reviews only
- Readers trying to automate regulated workflows without governance
- Readers who want to remove human approval from high-stakes work

---

# Part 4 - Field Positioning

## Comparable Texts and Gaps

**General AI agent books** explain agent concepts but often float above the everyday workflow where people actually use tools. This book grounds the concepts in Claude surfaces and practical supervision.

**Claude Code manuals** focus on coding. This book uses Claude Code as one example of agentic action, not the whole field.

**MCP and tool-use guides** explain integration mechanics. This book asks the prior question: should this agent have that tool at all?

## Positioning Statement

Unlike agent books that celebrate autonomy, this book teaches agentic AI as bounded, supervised delegation for readers who need to put agents to work without losing control of the work.

---

# Part 5 - Three-Act Learning Arc

## Act One - What Makes a System Agentic

The reader learns the difference between chat, workflow automation, code agents, and tool-using agents. The act ends when the reader can identify what the system can observe, decide, and do.

## Act Two - Designing the Boundary

The reader learns to define tasks, tools, permissions, context windows, approval checkpoints, fallback paths, and evidence of completion.

## Act Three - Supervising Real Work

The reader applies the boundary discipline across knowledge work, coding, research, education, and organizational settings.

## Arc Statement

This book takes the reader from agent hype to agent supervision by first naming what agents can do, then designing the boundaries around that action, then practicing supervised delegation in real workflows.

---

# Part 6 - Prerequisite Map

| Prerequisite | Safe to Assume? | Where Introduced |
|---|---|---|
| Basic Claude chat use | Probably | Introduction |
| Difference between output and action | No | Chapter 1 |
| Tool permissions | No | Chapter 3 |
| Claude Code | No | Chapter 4 |
| Claude Cowork | No | Chapter 5 |
| MCP | No | Chapter 6 |
| Evaluation loop | No | Chapter 8 |

**Front-loading decision:** The book opens with concrete agent behavior before naming architecture, avoiding a theory-first failure mode.

---

# Part 7 - Chapter-by-Chapter TOC

## Introduction - The Agent Arrives in Ordinary Work

**Capability built:** Recognize why agentic AI changes the user's responsibility.

The introduction frames agentic AI as a shift from generating content to taking bounded action. It names the central rule: no action without scope, approval, and verification.

## Chapter 1 - Chatbot, Assistant, Agent

**Capability built:** Distinguish conversation, assistance, and agency.

The reader learns a practical taxonomy: answerers produce text, assistants help with tasks, agents use tools to move the state of a system.

## Chapter 2 - The Agentic Loop

**Capability built:** Trace observe, plan, act, check, and report in a Claude workflow.

The chapter introduces the loop through examples from Claude Code and Cowork, then shows where errors enter: bad context, bad plan, bad tool use, bad verification.

## Chapter 3 - Tools, Permissions, and the Action Surface

**Capability built:** Decide which tools an agent should be allowed to use.

Core topics: local files, connectors, terminal access, browser access, APIs, least privilege, reversibility, and permission boundaries.

## Chapter 4 - Claude Code as Agentic Engineering

**Capability built:** Supervise codebase-changing work through tests, diffs, and approval gates.

The chapter covers repository context, issue-to-PR workflows, running tests, reviewing diffs, and refusing changes without a verification path.

## Chapter 5 - Claude Cowork as Agentic Knowledge Work

**Capability built:** Supervise multi-step file and document workflows without coding.

Examples include report generation, spreadsheet extraction, folder cleanup, meeting-note synthesis, and cross-document summaries.

## Chapter 6 - MCP and External Capabilities

**Capability built:** Understand MCP as a controlled way to extend what an agent can access.

The chapter explains MCP at a practitioner level: what a server exposes, why capability discovery matters, and how tool access changes risk.

## Chapter 7 - Planning Before Acting

**Capability built:** Require an agent to state a task plan before execution.

The reader learns plan review, missing-step detection, dependency order, stop conditions, and when to ask the agent to revise the plan.

## Chapter 8 - Verification Is the Control System

**Capability built:** Build verification into the task before the agent starts.

Examples: tests for code, source checks for research, row counts for data extraction, before/after snapshots for file changes, and peer review for prose.

## Chapter 9 - Failure Modes of Agentic Work

**Capability built:** Predict common agent failures before they appear.

Failures include tool overreach, stale context, plausible summaries, silent omissions, irreversible actions, prompt injection, and fabricated completion.

## Chapter 10 - Designing Human Approval Gates

**Capability built:** Decide where the human must approve, redirect, or stop.

The chapter distinguishes low-risk reversible work from high-risk irreversible or external-facing work.

## Chapter 11 - Agentic AI in Teams and Organizations

**Capability built:** Translate individual supervision into team practice.

The reader learns role boundaries, audit trails, shared prompts, policy, documentation, and escalation paths.

## Chapter 12 - Capstone: The Supervised Agentic Project

**Capability built:** Design and run a bounded agentic workflow from problem to verified output.

The reader specifies a real project, chooses tools, defines permissions, reviews the plan, supervises action, verifies output, and writes a short audit note.

---

# Part 8 - Chapter Anatomy Template

Each chapter should include:

1. Concrete agentic failure or scenario
2. Capability statement
3. Agentic concept introduced through the scenario
4. Claude-specific worked example
5. Boundary/permission decision
6. Verification method
7. Exercise: design the same boundary for the reader's own work

---

# Part 9 - Case Study Strategy

| Case Type | Chapters | Purpose |
|---|---|---|
| Codebase issue to PR | 2, 4, 8 | Demonstrates action with tests |
| File-heavy report generation | 2, 5, 8 | Demonstrates Cowork |
| MCP tool expansion | 6, 9 | Demonstrates action surface risk |
| Prompt-injection or bad source | 9 | Demonstrates adversarial risk |
| Team workflow | 11, 12 | Demonstrates governance |

---

# Part 10 - Hard Topics and Aging Risk

## Hard Chapters

- **Chapter 6:** MCP must be explained without burying the reader in protocol mechanics.
- **Chapter 9:** Security risks must be serious but not alarmist.
- **Chapter 11:** Team governance must remain practical rather than policy theater.

## Aging Risk

High-aging-risk content: product names, model tiers, interface details, MCP ecosystem examples.  
Stable content: least privilege, approval gates, reversibility, verification, audit trails, and human accountability.

---

# Part 11 - Adoption Risk Register

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Agent products change quickly | High | Medium | Keep chapters principle-first |
| Reader expects deep technical architecture | Medium | Medium | State practitioner scope clearly |
| Reader underestimates risk | High | High | Put permissions and verification early |
| Reader overestimates risk and avoids agents | Medium | Medium | Use bounded low-risk examples |
| MCP chapter becomes too technical | Medium | Medium | Keep it capability-focused |

---

# Part 12 - Open Questions

1. Should the capstone use Claude Code, Claude Cowork, or both?
2. Should MCP get one chapter or an appendix plus examples?
3. Should enterprise governance be included, or left to a future organizational handbook?
4. Should security examples include prompt injection explicitly?
