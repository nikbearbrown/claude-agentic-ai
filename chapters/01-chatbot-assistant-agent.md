# Chatbot, Assistant, Agent

**Capability built:** Distinguish conversation, assistance, and agency.

---

## The Same Task, Three Times

Here is one task, handled three different ways.

A developer has a bug: a function that should return an empty list is returning `None`. She wants Claude's help.

**Version 1.** She opens Claude.ai and asks: "Why would a Python function return `None` instead of an empty list?" Claude explains the common causes — missing return statement, early return paths, implicit `None` at branch end — and shows a corrected example. She reads the explanation, applies the fix herself in her editor, runs her tests.

**Version 2.** She pastes the function into the conversation and uploads her test file. She asks Claude to rewrite the function so it returns an empty list in the relevant case. Claude produces a revised function. She copies it into her editor, runs her tests.

**Version 3.** She opens Claude Code, points it to her repository, describes the bug. Claude Code reads the relevant file, identifies the function, proposes an edit, asks for approval, makes the change, runs the tests, and reports the result along with the diff.

The surface task is identical. The scope of action is not. In Version 1, Claude produces text that the human acts on. In Version 2, Claude produces a draft that the human places. In Version 3, Claude reads files, writes files, and executes commands. Only in Version 3 has anything happened in the codebase before the human reviews a diff.

That difference — not in output quality, but in action scope — is the distinction this chapter builds.

---

## What This Chapter Lets You Do

After this chapter, you will be able to:

- Classify AI interactions by what the system can observe, decide, and do
- Explain why the boundary between assistant and agent matters for supervision
- Apply the three diagnostic questions — see, decide, do — to real workflows
- Identify when a task requires agent-level permission design and verification

---

## A Spectrum, Not a Taxonomy

The three categories — chatbot, assistant, agent — are useful labels, but they describe positions on a spectrum rather than sealed boxes. The question to ask is not "which category is this?" but rather "how far along the spectrum of action is this system?" The further along, the more demanding the supervision.

The spectrum runs along a single axis: **external state change**. At one end, the system produces text that the user may or may not act on. At the other end, the system takes autonomous multi-step actions — reads files, runs tools, contacts external services, changes data — that persist after the conversation closes.

Between those poles are intermediate positions. A system that creates a file when you ask it to is doing more than producing text but less than running a multi-step plan. A system that searches the web and summarizes results is acting in the world, but in a limited and usually reversible way. A system that reorganizes a file system or submits a form is taking consequential external action.

The useful practitioner taxonomy is built from three diagnostic questions (Tang et al., 2023; Li et al., 2024):

1. **What can it see?** — the observation surface
2. **What can it decide?** — the planning and selection scope
3. **What can it do?** — the action surface

These three questions will return throughout this book, in every chapter. They are the frame for deciding what supervision is required.

---

## Chatbots: Text In, Text Out

A chatbot, in the operational sense used here, is a system whose primary output is text, and that text does not change anything outside the conversation by default. The system may be sophisticated — it may reason well, explain clearly, compare options, translate languages, summarize documents, draft prose. None of that makes it agentic.

The user's job with a chatbot is interpretive: read the output, assess its accuracy, decide what to do with it. The human holds the pen. The AI generates a draft or an explanation; the human is the one who emails it, commits it, posts it, or files it.

Verification for a chatbot focuses on claims. Is this accurate? Does it match what I know? Does it omit something important? Is the source reliable? The error modes are content errors — hallucination, misrepresentation, oversimplification — not action errors.

**The observation surface** of a chatbot is typically the conversation context: what you have typed, uploaded, or attached in the current session. It does not, by default, read your file system, run your code, or see your connected applications.

**The decision scope** is to produce the next response. It does not choose between action paths that affect external systems.

**The action surface** is narrow: text output, and possibly file downloads in some interfaces.

---

## Assistants: Task Support With Closer Proximity

An assistant, as used in this chapter, occupies the middle of the spectrum. It helps a user produce an artifact, often working with uploaded files, prior drafts, or task context. It may create files, produce formatted outputs, or integrate across multiple inputs. But the user remains close to each step and typically performs external actions manually.

The observation surface is broader — uploaded documents, pasted content, structured inputs — but still defined by what the user has explicitly provided. The assistant does not reach out on its own to gather more context.

The decision scope includes structuring, drafting, extracting, transforming, and summarizing. The assistant selects how to organize the work, which facts to highlight, how to format the output. It does not autonomously decide to gather more information or extend the task scope.

The action surface includes file creation in some interfaces. Claude can produce documents, tables, code files, and formatted outputs. This complicates a simple taxonomy: file creation is a form of external state change, so where does an assistant end and an agent begin? The honest answer is that the boundary blurs here. A system that creates a file you have not explicitly directed it to create is doing something more than pure assistance (Anthropic, "Create and edit files with Claude"). The safer teaching frame is to track the three questions, not the labels.

Verification for an assistant focuses on content and structure: does the draft accurately represent the sources? Are the facts correct? Does the structure match the intended use? Is anything missing that should be there?

---

## Agents: Tool-Mediated Action in an Environment

An agent — as the term is used in this book — is a system that uses tools to act in an environment, observes what happens, and adjusts course accordingly. The action changes things that persist after the conversation ends.

The research field's canonical description identifies the components: context or observation, planning, tools or actions, memory or state, feedback, and reporting (Tang et al., 2023; Li et al., 2024; Liang et al., 2024). In practice, what matters to the user is simpler: the agent can do things you did not manually do, and those things leave marks in the world.

**Claude Code** is an agentic engineering surface (Anthropic, "Claude Code overview"). It can inspect a repository, read source files, modify code, run tests, and report results. The user describes an issue; the agent observes the relevant files, proposes a fix, requests approval, makes the change, and verifies through test output. Changes persist in the file system.

**Claude Cowork** is an agentic knowledge-work surface (Anthropic, "Get started with Claude Cowork"). It can read documents, assemble reports, transform spreadsheets, search the web, and operate applications. When working in computer-use mode, it can see and interact with the desktop (Anthropic, "Let Claude use your computer in Cowork") [verify — current as of writing]. Each of these capabilities extends the action surface and, with it, the supervision requirement.

The observation surface for an agent is potentially broad: the file system, connected applications, browser sessions, APIs, MCP-connected services. This is exactly why scope definition matters — before the agent acts, you must be deliberate about what it is permitted to see.

The decision scope includes multi-step planning, tool selection, priority ordering, and adaptive revision when steps fail. The agent does not just produce a response; it chooses a path through the work.

The action surface is the part that demands the most attention from a supervision standpoint. Agents can read files, write files, execute code, send requests to external services, and in some configurations use applications as a human would. Each action type has different reversibility, different blast radius, and different verification requirements.

---

## The Supervision Table

Different positions on the spectrum require different supervision designs. This table maps the questions to the positions.

| Question | Chatbot | Assistant | Agent |
|---|---|---|---|
| Produces text output? | Yes | Yes | Yes |
| Uses task context? | Sometimes | Often | Often |
| Uses tools? | Rarely | Sometimes | Usually |
| Changes files or applications? | No or limited | Sometimes | Yes |
| Needs permission design? | Light | Moderate | Strong |
| Needs action log? | Usually no | Sometimes | Yes |

The table is a design tool, not a grading rubric. A system that needs strong permission design and an action log requires different preparation from the user — scope statements, approval checkpoints, verification steps — than a system where the only supervision task is reading an answer carefully.

Parasuraman, Sheridan, and Wickens (2000) make the underlying principle explicit: levels of human interaction with automation differ by what the system selects, recommends, executes, and confirms. As the system takes on more of those functions autonomously, the human's role shifts from executing to supervising — but the supervisory demands increase in kind. This is not a paradox. It is the architecture of delegation.

---

## The See/Decide/Do Framework in Practice

Return to the three questions. They are diagnostic, not definitional. Use them before every agentic task.

**What can it see?** List what the system has access to: which folder, which connected service, which files, which applications. If you cannot answer this, define it before you start. An agent that can see more than you intended can include information you did not mean to share and act on context you did not authorize.

**What can it decide?** Describe what the system can choose autonomously: which tools to use in what order, how to structure the output, whether to retry a failed step. The wider the decision scope, the more important the plan review. If the system can decide to extend the task scope on its own initiative, you need an explicit boundary in the prompt.

**What can it do?** Enumerate the actions and their reversibility. File reads are reversible in the sense that they leave no mark. File writes are not — they change state that persists. Browser submissions, API calls, and external-facing actions may be irreversible and consequential. For each action type, decide whether you require approval before it happens, or whether you trust the agent's judgment within defined bounds.

The NIST AI Risk Management Framework (NIST, 2023) organizes AI governance around mapping, measuring, managing, and documenting risk. The see/decide/do framework is a practitioner's version of that mapping step, applied to individual tasks before they start.

---

## The Ambiguous Middle

A word about the cases that do not fit neatly.

A chat session where Claude creates a formatted document at your request is closer to assistant than agent — you directed the creation explicitly. A tightly constrained Claude Code run that can only edit one file and only runs pre-specified tests is far less agentic in practice than its tool access might suggest. An MCP-connected assistant that can read a database is acting with more reach than most users expect from a "chat" interface.

The labels will blur because products blur. What matters is not the label but the answer to the three questions. When you have answered them honestly, you know what supervision design the task requires.

Bainbridge's warning — that automation can increase monitoring and intervention demands (Bainbridge, 1983) — applies most sharply at the ambiguous middle. A system that looks like a chat assistant but has file-write access is carrying more supervision responsibility than it appears to. The gap between apparent scope and actual scope is where errors enter without anyone noticing.

---

## Why Stronger Agency Means Stronger Requirements, Not Better Performance

A misconception worth naming explicitly: more capability does not mean better results. It means more action surface, which means more ways for errors to propagate before they are caught.

A chatbot that misidentifies a bug produces a wrong answer. The user reads it, disagrees, discards it. Cost: a few minutes.

An agent that misidentifies a bug, edits files, reruns tests, gets an ambiguous result, patches around the failing test, and reports completion has done more. Whether it has done better depends on whether the human read the plan, reviewed the diff, and verified the test result before calling it done.

More agency requires the user to be more ready, not less. The Microsoft Research Guidelines for Human-AI Interaction (CHI 2019) frame this as a design responsibility: systems should support appropriate levels of user control, uncertainty disclosure, and recoverability. For agents, those properties must be designed in before use, not discovered after.

---

## Common Misconceptions

**"Any AI that chats is a chatbot."** A system with a conversational interface can have substantial action capabilities underneath it. The interface does not determine the action surface.

**"Any AI with tools is fully autonomous."** Tools expand what a system can do; they do not determine how much human oversight is required. A well-designed agent with broad tools can be more tightly supervised than a poorly designed one with fewer.

**"Agents are defined by intelligence rather than action."** A system can reason well and still be a chatbot if it cannot change external state. A system can reason poorly and still be an agent if it can edit your files. The distinction is in the action, not the IQ.

**"If it asks before acting, it is not an agent."** Asking for approval is a design feature, not a disqualifier. An agent that asks before each action is a supervised agent — exactly the kind this book teaches. The asking is a good sign, not evidence that the system is merely an assistant.

**"Agency is a product label, not a capability spectrum."** Vendors will label their products inconsistently. The three-question framework gives you a product-neutral way to assess what you are actually working with.

---

## Exercises: Try This

**Exercise 1: The three-question audit.**
Choose one AI tool you currently use. Answer the three questions: What can it see? What can it decide? What can it do? Compare your answers to what you assumed before you started this exercise. Note any gap between assumed scope and actual scope.

**Exercise 2: Classify a workflow.**
Describe a real task you do regularly that might benefit from AI assistance. Place it on the chatbot-assistant-agent spectrum using the supervision table. Write one sentence about what permission design the task would require before you delegated it.

**Exercise 3: Find the human-only zone.**
For the same workflow, name one decision or action that should not be delegated regardless of the agent's capability. Explain why: is it a matter of accountability, irreversibility, sensitivity, or expertise?

---

## What Would Change My Mind

This chapter argues that the chatbot/assistant/agent spectrum is the right frame for thinking about supervision requirements. That argument would need revision if:

- A new interaction paradigm emerged that did not map to observation, planning, and action — a system that produced outputs in a way that bypassed the environmental action model entirely.
- Verification technology advanced to the point that external state changes could be reliably detected and reversed without human review, eliminating the asymmetry between text output and tool-mediated action.
- Empirical research showed that users who did not distinguish assistant from agent made better supervision decisions than those who did, suggesting the taxonomy is cognitively counterproductive.

None of these conditions hold currently. The spectrum framing remains the best entry point for practitioners.

---

## Still Puzzling

- The line between a sophisticated assistant and a constrained agent may move as interfaces evolve. How should the three-question framework be updated as tool access becomes more routine even in "chat" interfaces?
- How much of the action surface does a user need to understand to supervise well? Is complete enumeration of tool capabilities necessary, or is a summary-level understanding sufficient?
- If agents become better at reporting uncertainty — flagging the steps they are less sure about — does that reduce the supervision burden at the plan-review stage?

---

## Bridge to Chapter 2

Now that you can classify a system by its observation, decision, and action scope, the next question is: what does the system actually do between when you hand it the task and when it reports completion? Chapter 2 opens the loop.

---

## Sources Used

- Anthropic, "Claude Code overview," Claude Code Docs. https://code.claude.com/docs
- Anthropic, "Create and edit files with Claude," Claude Help Center. https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude
- Anthropic, "Get started with Claude Cowork," Claude Help Center. https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork
- Anthropic, "Let Claude use your computer in Cowork," Claude Help Center. https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork
- Bainbridge, Lisanne. "Ironies of Automation." *Automatica*, 1983. https://doi.org/10.1016/0005-1098(83)90046-8
- Li, Xinzhe et al. "A Review of Prominent Paradigms for LLM-Based Agents: Tool Use, Planning, and Feedback Learning." arXiv, 2024. https://arxiv.org/abs/2406.05804
- Liang, Wenliang et al. "Understanding the Planning of LLM Agents: A Survey." arXiv, 2024. https://arxiv.org/abs/2402.02716
- Microsoft Research. "Guidelines for Human-AI Interaction." CHI 2019. https://www.microsoft.com/en-us/research/project/guidelines-for-human-ai-interaction/publications/
- NIST. "Artificial Intelligence Risk Management Framework (AI RMF 1.0)." 2023. https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10
- Parasuraman, R., Sheridan, T. B., and Wickens, C. D. "A Model for Types and Levels of Human Interaction with Automation." 2000. https://pubmed.ncbi.nlm.nih.gov/11760769/
- Tang, Xiangru et al. "A Survey on Large Language Model based Autonomous Agents." arXiv, 2023. https://arxiv.org/abs/2308.11432

---

*Tags: #claude #agentic #ai #chatbot #assistant #agent #taxonomy #supervision #Medhavy*
