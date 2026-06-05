# Chapter 12 — Capstone: The Supervised Agentic Project

## TL;DR

- The capstone is not about the final artifact. It is about every decision you made before and after the agent acted.
- The supervised agentic project has a defined structure: project brief, data boundary, action surface map, agent plan, approval gates, failure pre-mortem, verification evidence, final artifact, audit note, and transfer reflection.
- The human expertise is visible in the artifacts, not in the output. Anyone can get an agent to produce something plausible. The capability being practiced here is knowing whether it is trustworthy.
- Use this template for real work. The audit note is not paperwork — it is how you improve the next delegation.

---

## Opening Scene

It is three hours before a grant proposal deadline. A program officer at a small research nonprofit has been using Claude for months. She knows the tool. She asks Cowork to pull together a summary of three recent funding announcements from a folder of PDFs and draft a one-page comparative brief.

Cowork produces something that looks authoritative. It has a table. It has bullets. The language is confident. She attaches it to the proposal and submits.

Two days later, a colleague reads the brief. One of the funding announcements in the table does not match the actual source. The eligibility criteria are wrong — copied from an earlier version of the announcement that happened to be in the folder alongside the current one. The brief was polished, specific, and incorrect.

Nothing in the output announced the problem. The artifact looked like finished work. The error was in the gap between what the agent had access to and what the program officer assumed it would use.

This is the book's central lesson in its most concentrated form. The agent did exactly what it was capable of doing. The supervision — scoping the folder, verifying which version of each document was current, checking the table against the originals — was the part that did not happen.

This chapter provides a structure for making sure it does.

---

## What This Chapter Lets You Do

By the end of this chapter you will be able to:

- Select a bounded real or realistic project appropriate for supervised agentic work.
- Define a data boundary, action surface map, and set of approval gates before the agent acts.
- Require and review an agent plan before execution.
- Supervise agentic execution with defined stop conditions and verification evidence.
- Write an audit note that makes your reasoning and accountability visible.
- Transfer what you learned to the next agentic task.

This chapter integrates every concept in the book: agent taxonomy (Chapter 1), the agentic loop (Chapter 2), tool permissions (Chapter 3), Claude Code and Cowork as agent surfaces (Chapters 4 and 5), MCP and extended capabilities (Chapter 6), planning before acting (Chapter 7), verification as a control system (Chapter 8), failure modes (Chapter 9), approval gates (Chapter 10), and team governance (Chapter 11). The capstone is where these become a single practice rather than separate concepts.

---

## Why the Final Artifact Is Not the Measure

GenAI assessment research has identified a consistent failure mode: evaluating agentic or AI-assisted work by the quality of the output alone (arXiv, 2025, "Navigating the New Landscape"). A polished deliverable can hide:

- Unverified claims that happen to sound plausible.
- Data inputs that were out of scope, outdated, or confidential.
- Reasoning steps the agent skipped or compressed.
- Actions the agent took that the human did not approve.
- Omissions the agent made silently.

The same research supports process-oriented assessment: the workflow matters as much as the deliverable. What the learner decided, approved, verified, changed, and rejected is the evidence of competent supervision.

Microsoft Research's study on generative AI and critical thinking (CHI 2025) documents a complementary risk: self-reported reductions in cognitive effort and confidence effects when users over-rely on AI output. The check does not happen because the output seems authoritative. This is precisely the dynamic the capstone structure is designed to counteract.

The capstone treats the workflow artifacts as evidence of supervision. The final artifact matters — but only if the process behind it was sound.

---

## Core Concept: The Supervised Agentic Project Structure

A supervised agentic project produces ten artifacts. Together they answer: what was the task, what was the agent allowed to do, what happened, and how do I know the output is trustworthy?

### The Ten Artifacts

**1. Project brief.**
What is the goal? What is the deliverable? Who is the audience? What would success look like, and what would failure look like? A brief that cannot answer these questions is not ready to delegate to an agent.

**2. Data boundary.**
What inputs is the agent allowed to use? Name specific files, folders, or sources. Name what is explicitly excluded: credentials, PII, confidential data, outdated versions of documents. The program officer in the opening scene needed this artifact. She did not have it.

**3. Action surface map.**
Which Claude surface will you use — Claude AI, Claude Cowork, Claude Code? Which tools and connectors are enabled? What can the agent read, write, execute, or send? What is it explicitly blocked from? The action surface map is Chapter 3 applied to a specific project.

**4. Agent plan.**
Before the agent acts, require a stated plan: what steps it will take, what tools it will use, in what order, and what it will produce. Review the plan for missing steps, bad order, or overreach before approving any action. This is Chapter 7 applied.

**5. Approval gates.**
Where will the human decide before the agent continues? At minimum: before any external-facing action, before any irreversible change, before any output leaves the defined scope. Approval gates are pre-specified, not improvised in the moment.

**6. Failure pre-mortem.**
Before execution, list the three to five most likely ways this delegation could fail. Consider: stale data, fabricated details, scope creep, irreversible actions, misunderstood instructions, silent omissions. Pre-mortems are covered in Chapter 9. Writing one before execution is the habit that makes failure prevention possible.

**7. Verification evidence.**
What evidence will you collect to know the output is trustworthy? For a literature summary: source checks against originals. For code: tests that pass before merge. For a data table: row counts and formula audits against the source. For a report: spot-check of specific claims against cited documents. Verification evidence is defined before the agent acts, not after the output arrives. This is Chapter 8 applied.

**8. Final artifact.**
The deliverable — the report, the code, the summary, the analysis. This is what the agent produced and what the human approved for use after verification.

**9. Audit note.**
A short written record of what happened. Headings: what you delegated, what you did not delegate, what tools and permissions were used, what went wrong or changed, what evidence you checked, what you accepted or revised, and what you would do differently next time. The audit note is not optional. It is the document that turns agentic work into organizational knowledge rather than invisible automation.

**10. Transfer reflection.**
What did this project teach you about supervised delegation? What would you set up differently? What failure mode appeared that you did not anticipate? What verification method worked well? The transfer reflection, following Perkins and Salomon (1992), explicitly connects what you learned in this project to how you will approach the next one.

---

## Worked Walkthrough: Research Brief

Let the project be a research brief: summarize three recent peer-reviewed papers on AI governance published in the last two years, comparing their recommendations for organizational oversight.

**Project brief.** Goal: a three-page comparative brief on AI governance recommendations. Deliverable: a structured document with source citations. Audience: a team making policy decisions. Success: accurate, cited, clearly comparative. Failure: uncited claims, outdated papers, fabricated details, missing differences.

**Data boundary.** Inputs: three specific PDFs downloaded from verified journal sources, stored in a controlled folder. Excluded: preprints that have not undergone peer review, papers outside the specified date range, any web search by the agent. The folder contains exactly three files. Nothing else.

**Action surface map.** Surface: Claude Cowork. Connector: the specific research folder only. Tools: document reading, text generation. No web search connector. No email connector. No file-write access outside the draft folder. [verify — current as of writing]

**Agent plan.** Request a plan before execution. Expected plan: read each paper in sequence, extract key governance recommendations, compare across papers, draft the brief with citations. Review the plan: does it include source verification steps? Does it treat the three files as the only inputs? If the plan mentions searching for additional sources, reject and revise.

**Approval gates.** Gate 1: plan reviewed and approved before any reading begins. Gate 2: draft reviewed against the source PDFs before finalization. Gate 3: citations verified against originals before the brief leaves the folder.

**Failure pre-mortem.**
- Most likely failure: the agent synthesizes claims not directly supported by the specific papers.
- Second: the agent quotes accurately but the brief omits a paper's central disagreement with the others.
- Third: the citations are formatted plausibly but do not match actual page locations in the originals.
- Fourth: the agent offers additional "relevant context" from its training data rather than sticking to the three sources.

**Verification evidence.** Check each citation against the original PDF. Check that each paper's primary recommendation is represented without distortion. Check that differences between papers are stated as differences, not smoothed over. Record what you checked and what you found.

**Final artifact.** A three-page brief with accurate citations, comparative structure, and a human-verified claim set.

**Audit note (abbreviated).**

*What I delegated:* Initial extraction and comparative structuring from three source PDFs.

*What I did not delegate:* Final claim verification, judgment about which disagreements mattered, the framing of the brief for its audience.

*Tools/permissions used:* Cowork with read access to the research folder. No web access.

*What went wrong:* The draft treated one paper's conclusion as if it were shared by all three. Found during Gate 2 review. Revised before approval.

*What evidence I checked:* All three citations against source PDFs. The one divergent paper's conclusion verified against the full conclusion section.

*What I accepted, rejected, or revised:* Accepted the comparative structure. Revised the characterization of Paper 2's position. Rejected one framing sentence that was ambiguous about whose view it represented.

*What I would do differently:* In the plan request, explicitly ask the agent to flag where papers disagree rather than only summarizing where they agree.

**Transfer reflection.** The failure pre-mortem predicted synthesis errors. It was right. The verification step I had planned (checking each citation) caught the problem. Next time I will add to the plan request: "explicitly identify where these papers take different positions." The audit note goes into a team shared folder so the next person running a similar brief has a model to follow.

---

## Choosing Your Track

The capstone supports multiple workflows. Choose based on your project and access:

**Chat-only simulation.** Use Claude AI to work through the capstone structure in conversation. Ask Claude to play the role of an agent with limited tool access. Produce all ten artifacts as text documents. This track practices the thinking without requiring Cowork or Code access.

**Cowork workflow.** Choose a file-heavy project: report assembly, document comparison, data extraction, folder summarization. Use Cowork with a tightly defined source folder. Produce the action surface map and approval gates as explicit Cowork configuration. [verify — current as of writing]

**Claude Code workflow.** Choose a project that involves a codebase: a failing test, a feature request, a documentation gap. Use Claude Code on a non-production branch. Require tests before any merge. Produce the plan as an explicit Claude Code task description. Produce verification evidence as test results and diff review. [verify — current as of writing]

**MCP capability review.** Choose a project that evaluates whether to add a new MCP server to your workflow or team. The deliverable is not a file — it is a governance recommendation: approve, restrict, or reject, with reasoning. Produce the action surface map as a tool-by-tool permission analysis.

Every track produces the same ten artifacts. The specific tools change; the supervision structure does not.

---

## The Capstone Packet Template

| Artifact | Purpose | Done? |
|---|---|---|
| Project brief | Define goal and deliverable | |
| Data boundary | Name allowed and forbidden inputs | |
| Action surface map | Name tools and permissions | |
| Agent plan | Make delegation inspectable | |
| Approval gates | Define where human decides | |
| Failure pre-mortem | Anticipate likely failures | |
| Verification evidence | Document the check | |
| Final artifact | Show useful output | |
| Audit note | Record what happened | |
| Transfer reflection | Prepare the next delegation | |

Print this. Fill it in. Cross off items only when the artifact exists, not when you intend to produce it.

---

## Common Misconceptions

**"The capstone is the final artifact."** The final artifact is one of ten outputs. A polished deliverable produced through an undocumented, unverified process is not the goal. The workflow is the goal. The artifact is evidence of the workflow.

**"A more autonomous project is a better project."** A project that requires less human intervention is not more advanced. It is either lower risk, better designed, or not yet verified. Demonstrate capability through the quality of your supervision, not by removing it.

**"Using every tool proves mastery."** Using the minimum tool set needed for the task is better practice than demonstrating range. The action surface map should reflect the project, not a feature inventory.

**"The audit note is paperwork."** The audit note is the document that makes your reasoning visible, makes your accountability checkable, and makes your practice improvable. A person who cannot produce an audit note cannot demonstrate that they supervised the work. For team practice (Chapter 11), the audit note is also how the team learns across projects.

**"If the output is good, the workflow was good."** The opening scene disproves this. The output looked good. The workflow had a critical gap. Outcome quality is not process quality. This distinction is the book's central argument.

**"Reflection means describing what happened, not what changed."** Transfer reflection, following Perkins and Salomon (1992) on learning transfer, requires explicit connection to future practice. "The agent made a synthesis error" is description. "Next time I will include 'flag disagreements' in the plan request" is transfer.

---

## Try This

**Exercise 1: Complete a capstone packet on a real project.**
Select a project from your current work that is low-to-moderate risk, does not involve confidential data that cannot be scoped, and has a defined deliverable. Complete all ten artifacts. Do not submit the final artifact until the audit note is written. Share the packet — not just the artifact — with someone who can evaluate your supervision decisions.

**Exercise 2: Pre-mortem first.**
Before your next agent-assisted task, write the failure pre-mortem before you start. Identify the three most likely ways the delegation will fail. Run the task. Come back and check whether your pre-mortem was accurate. What did you predict correctly? What did you miss?

**Exercise 3: Evaluate an audit note.**
Find or construct a plausible-looking agent-assisted output in your domain — a summary, a code change, a data table. Now write the audit note for it, including what data was allowed, what verification was done, what was rejected or revised, and what you would do differently. What questions does writing the audit note force you to answer? What would you have to go back and check?

---

## What Would Change My Mind

The chapter argues that the ten-artifact supervised agentic project is the right structure for demonstrating capable agentic delegation, and that final artifact quality alone is insufficient evidence.

This argument would weaken if:

- Evidence accumulated that supervised, documented workflows performed substantially worse on task outcomes than unsupervised ones. No such evidence currently exists, and the research on GenAI over-reliance (Microsoft Research, CHI 2025) points in the opposite direction.
- AI systems developed reliable, transparent self-verification mechanisms that made external human verification redundant for defined task types. This would require genuinely interpretable intermediate outputs, not just confident final text. [verify — current as of writing]
- The ten-artifact structure consistently proved too burdensome for the actual value added. In practice, the artifacts can be lightweight; the audit note for a routine task can be three sentences. The question is not whether to produce them but how much detail the risk level requires.

---

## Still Puzzling

**Where is the right line between necessary structure and bureaucratic overhead?** The capstone template scales from a brief audit note for routine delegation to a full governance document for high-stakes organizational work. The chapter does not fully resolve where on that continuum a given project should land. Practice and judgment fill that gap.

**How do you handle a project that goes badly enough to stop?** The chapter teaches stop conditions (Chapter 10) but the capstone walkthrough assumes the project completes. A capstone that included a deliberate stop — where the learner recognized a failure mode and chose not to use the output — would be a stronger demonstration of supervision than one that completed smoothly.

**What counts as adequate verification for novel task types?** The chapter names verification methods for common domains (code tests, source checks, row counts). For genuinely novel tasks without established verification conventions, designing the evidence standard is itself a competence that needs development.

**How does the audit note standard evolve across time?** An early-career practitioner and an experienced one will produce very different audit notes for the same task. The chapter treats audit notes as uniform artifacts, but their quality depends on judgment that develops with practice.

---

## Closing

You started this book with the observation that a polished artifact announces nothing about whether the work behind it was sound. An agent can produce fluent text, passing code, formatted tables, and plausible-sounding citations. None of that is evidence that the output is correct, appropriately scoped, ethically handled, or worth acting on.

The book's argument has been consistent: agentic AI is delegated action under constraints, and the capable human is the one who defines the constraint before the agent acts, reviews the plan before the agent moves, supervises execution through defined gates, verifies with evidence rather than impression, and takes responsibility for the final decision.

These are not limitations on what agents can do. They are the practices that make agent-assisted work trustworthy — in your own hands, in your team's practice, and in the domains where the work has real consequences.

The audit note is the last artifact in the capstone packet. It is also the first document for the next project. What you learned from this delegation goes into the next one's failure pre-mortem. What your team learned goes into the next policy review. The supervised agentic project is not a one-time assignment. It is a practice you are beginning.

Begin it with the same question the Introduction asked: not whether the output is impressive, but what would have to be true for it to be trusted.

---

## AI Wayback Machine

![Ida B. Wells](../images/ida-b-wells-82h.png)

*Puppet Art by [Nik Bear Brown](https://www.nikbearbrown.com/).*

**Run this:**

```
Who was Ida B. Wells, and how does her approach to evidence, documentation, and accountability connect to how we should supervise AI agents today? Keep it to three paragraphs. End with the single most surprising thing about her career or methods.
```

Search **"Ida B. Wells"** on Wikipedia, then try the same prompt with Claude.

**Now make the prompt better:**

- Ask it to apply Wells's investigative method — gather primary evidence, verify claims independently, document sources — to a specific AI-assisted research task you might run.
- Ask it: if Wells were reviewing an AI-generated report, what would her first three questions be?

What changes? What gets sharper? Where does the analogy usefully resist you?

---

## Sources Used

Brown, Collins, and Duguid. "Situated Cognition and the Culture of Learning." *Educational Researcher*, 1989. https://www.jstor.org/stable/1176008

Collins, Brown, and Newman. "Cognitive Apprenticeship: Teaching the Crafts of Reading, Writing, and Mathematics." 1989. https://apps.dtic.mil/sti/pdfs/ADA178530.pdf

Perkins and Salomon. "Transfer of Learning." 1992. https://jaymctighe.com/wp-content/uploads/2011/04/Transfer-of-Learning-Perkins-and-Salomon.pdf

"Navigating the New Landscape: A Conceptual Model for Project-Based Assessment in the Age of GenAI." arXiv, 2025. https://arxiv.org/abs/2508.11709

NIST. "Artificial Intelligence Risk Management Framework (AI RMF 1.0)." 2023. https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10

Anthropic. "Claude Code overview." Claude Code Docs. https://code.claude.com/docs

Anthropic. "Configure permissions." Claude Code Docs. https://code.claude.com/docs/en/permissions

Anthropic. "Get started with Claude Cowork." Claude Help Center. https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork

Anthropic. "Use Claude Cowork safely." Claude Help Center. https://support.claude.com/en/articles/13364135-use-cowork-safely

Microsoft Research. "The Impact of Generative AI on Critical Thinking." CHI 2025. https://www.microsoft.com/en-us/research/publication/the-impact-of-generative-ai-on-critical-thinking-self-reported-reductions-in-cognitive-effort-and-confidence-effects-from-a-survey-of-knowledge-workers/
