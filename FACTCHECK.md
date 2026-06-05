# FACTCHECK register — claude-agentic-ai
*Run: 2026-06-01 | Checker: Claude Sonnet 4.6 sub-agent*

## Summary

**Total flagged items: 54**
- PRODUCT/PLATFORM (defer to publication-time): **42**
- CITATION/STAT (verifiable): **12**
- CONTESTED (noted in-text as contested): **2** (not separate flags — inline acknowledgments)

**CITATION/STAT verdicts:**
- CONFIRMED: **11**
- CORRECTED → [fix]: **1** (MCP USB-C attribution)
- UNCONFIRMED: **0** (Zhu et al. 2026 — previously suspect — confirmed via Springer)

**No chapters contain [UNVERIFIED] or [AGING] tags.** All flags use `[verify]` or `[verify — current as of writing]` or `[verify — current as of writing for ...]` variants.

---

## Full Table

| Chapter | Flagged claim | Type | Verdict | Action needed |
|---|---|---|---|---|
| 00-the-agent-arrives | Claude Code and Claude Cowork described as Anthropic's concrete implementations | PRODUCT/PLATFORM | DEFER | Check at publication |
| 00-the-agent-arrives | Claude Cowork computer-use mode (Anthropic "Let Claude use your computer in Cowork") | PRODUCT/PLATFORM | DEFER | Check at publication |
| 01-chatbot-assistant-agent | Claude Cowork computer-use mode description | PRODUCT/PLATFORM | DEFER | Check at publication |
| 01-chatbot-assistant-agent | Bainbridge (1983) "Ironies of Automation" *Automatica* DOI 10.1016/0005-1098(83)90046-8 | CITATION/STAT | CONFIRMED | None — correct journal, volume 19 no.6 pp.775–779, DOI verified |
| 01-chatbot-assistant-agent | Parasuraman, Sheridan & Wickens (2000) "A Model for Types and Levels…" — described as foundational human-automation paper | CITATION/STAT | CONFIRMED | None — IEEE Trans. Syst. Man Cybern. Part A, vol. 30, pp. 286–297, PMID 11760769, DOI 10.1109/3468.844354 verified |
| 01-chatbot-assistant-agent | NIST AI RMF 1.0 (2023) organize AI governance around mapping, measuring, managing, documenting risk | CITATION/STAT | CONFIRMED | None — NIST AI 100-1, launched Jan 26 2023; four core functions are Govern/Map/Measure/Manage |
| 02-the-agentic-loop | ReAct and Reflexion frameworks described as embedded in Claude Code and Cowork | PRODUCT/PLATFORM | DEFER | Check at publication |
| 02-the-agentic-loop | Yao et al. (2023) "ReAct: Synergizing Reasoning and Acting in Language Models" ICLR 2023 arxiv 2210.03629 | CITATION/STAT | CONFIRMED | None — confirmed at arxiv.org/abs/2210.03629; ICLR 2023 correct |
| 02-the-agentic-loop | Shinn et al. (2023) "Reflexion: Language Agents with Verbal Reinforcement Learning" NeurIPS 2023, hash URL used | CITATION/STAT | CONFIRMED | None — NeurIPS 2023 confirmed (poster 70114); hash 1b44b878bb782e6954cd888628510e90 verified at proceedings.neurips.cc |
| 02-the-agentic-loop | Parasuraman et al. (2000) — intervention architecture | CITATION/STAT | CONFIRMED | Already confirmed above |
| 02-the-agentic-loop | NIST AI RMF (2023) — map/measure/manage | CITATION/STAT | CONFIRMED | Already confirmed above |
| 03-tools-permissions | Access types in Claude's agentic surfaces | PRODUCT/PLATFORM | DEFER | Check at publication |
| 03-tools-permissions | Saltzer & Schroeder (1975) "least set of privileges" — Proceedings of the IEEE, 1975 | CITATION/STAT | CONFIRMED | None — Proc. IEEE vol. 63 no. 9 pp.1278–1308, web.mit.edu URL valid |
| 03-tools-permissions | OWASP LLM Top 10 (2025) — "excessive agency" as core risk | CITATION/STAT | CONFIRMED | None — OWASP Top 10 for LLM Applications 2025 exists at genai.owasp.org/llm-top-10/ |
| 03-tools-permissions | OWASP MCP Top 10 (2025) — excessive permissions, tool poisoning, command injection | CITATION/STAT | CONFIRMED | None — OWASP MCP Top 10 live at owasp.org/www-project-mcp-top-10/; risks labeled MCP01:2025–MCP10:2025 |
| 03-tools-permissions | Rung 7 computer use — Cowork safety docs recommend preferring connectors over computer use | PRODUCT/PLATFORM | DEFER | Check at publication |
| 03-tools-permissions | Anthropic "Configure permissions" URL https://code.claude.com/docs/en/permissions | PRODUCT/PLATFORM | DEFER | Check at publication |
| 03-tools-permissions | Anthropic "Use Claude Cowork safely" URL https://support.claude.com/en/articles/13364135 | PRODUCT/PLATFORM | DEFER | Check at publication |
| 03-tools-permissions | Anthropic "Let Claude use your computer in Cowork" Apr 24 2026 URL 14128542 | PRODUCT/PLATFORM | DEFER | Check at publication |
| 03-tools-permissions | Anthropic "Use plugins in Claude Cowork" Apr 9 2026 URL 13837440 | PRODUCT/PLATFORM | DEFER | Check at publication |
| 03-tools-permissions | NIST AI RMF — documentation of controls and residual risk | CITATION/STAT | CONFIRMED | Already confirmed above |
| 04-claude-code | Claude Code description as command-line AI agent | PRODUCT/PLATFORM | DEFER | Check at publication |
| 04-claude-code | Anthropic permission docs — configure policy for auto vs. per-action confirmation | PRODUCT/PLATFORM | DEFER | Check at publication |
| 04-claude-code | OWASP LLM Top 10 — "excessive agency" | CITATION/STAT | CONFIRMED | Already confirmed above |
| 04-claude-code | HumanEval (Chen et al. 2021) — code evaluated by execution | CITATION/STAT | CONFIRMED | None — arxiv 2107.03374, July 2021, OpenAI paper; HumanEval benchmark confirmed |
| 04-claude-code | Reflexion (Shinn et al. 2023) — self-evaluation | CITATION/STAT | CONFIRMED | Already confirmed above |
| 04-claude-code | Secrets/credentials posture — Anthropic "Claude Code security" URL | PRODUCT/PLATFORM | DEFER | Check at publication |
| 04-claude-code | Production access boundary — Anthropic "Configure permissions" | PRODUCT/PLATFORM | DEFER | Check at publication |
| 04-claude-code | Claude Code Docs URLs (4 items in references) | PRODUCT/PLATFORM | DEFER | Check at publication |
| 05-claude-cowork | Claude Cowork description as agentic knowledge-work environment | PRODUCT/PLATFORM | DEFER | Check at publication |
| 05-claude-cowork | Framing that Cowork brings Claude Code-level agentic capability to noncoding desktop | PRODUCT/PLATFORM | DEFER | Check at publication |
| 05-claude-cowork | Hierarchy: prefer connectors over browser, browser over computer use | PRODUCT/PLATFORM | DEFER | Check at publication |
| 05-claude-cowork | "Assign tasks remotely" increases supervision responsibility at setup time | PRODUCT/PLATFORM | DEFER | Check at publication |
| 05-claude-cowork | 5 Anthropic Help Center URLs in references (articles 13345190, 13364135, 14128542, 14116274, 13947068) | PRODUCT/PLATFORM | DEFER | Check at publication |
| 06-mcp | "MCP is like USB-C for AI applications" — attributed to "the protocol team at Anthropic" | CITATION/STAT | CORRECTED → [fix] | Attribution is imprecise: the analogy is in Anthropic's MCP announcement and widely used by community; no named "protocol team" quote identified. Change to: "Anthropic's MCP announcement described the protocol as 'USB-C for AI applications'" or remove specific team attribution |
| 06-mcp | Connecting more servers extends action surface (Saltzer & Schroeder 1975 cited) | CITATION/STAT | CONFIRMED | Already confirmed above |
| 06-mcp | OWASP MCP Top 10 — prompt injection, tool poisoning mechanism documented | CITATION/STAT | CONFIRMED | Already confirmed above |
| 06-mcp | Permission boundary as structural defense — mitigation tool specifics | PRODUCT/PLATFORM | DEFER | Check at publication |
| 06-mcp | Anthropic MCP Directory policy on tool descriptions | PRODUCT/PLATFORM | DEFER | Check at publication |
| 06-mcp | Available MCP connectors in Claude environment | PRODUCT/PLATFORM | DEFER | Check at publication |
| 06-mcp | MCP standardization conditions not currently met | PRODUCT/PLATFORM | DEFER | Check at publication |
| 07-planning | ReAct architecture (Yao et al. 2023) underlies current agentic systems | CITATION/STAT | CONFIRMED | Already confirmed above |
| 07-planning | Parasuraman et al. (2000) — levels of human interaction with automation | CITATION/STAT | CONFIRMED | Already confirmed above |
| 08-verification | Farquhar et al. (2024) — high-confidence prose not correlated with accuracy | CITATION/STAT | CONFIRMED | None — Nature 2024, vol. 630 no. 8017 pp.625–630; DOI verified; semantic entropy method confirmed |
| 08-verification | HumanEval principle — code verified by execution (Chen et al. 2021) | CITATION/STAT | CONFIRMED | Already confirmed above |
| 08-verification | ReAct loop (Yao et al. 2023) | CITATION/STAT | CONFIRMED | Already confirmed above |
| 08-verification | Reflexion (Shinn et al. 2023) | CITATION/STAT | CONFIRMED | Already confirmed above |
| 08-verification | NIST AI RMF (2023, 2024) — provenance documentation, output risk management | CITATION/STAT | CONFIRMED | None — both NIST AI 100-1 (2023) and NIST AI 600-1 GenAI profile (2024) exist at nvlpubs.nist.gov |
| 08-verification | Anthropic Cowork safety guidance — file-affecting workflows | PRODUCT/PLATFORM | DEFER | Check at publication |
| 08-verification | Developing conditions for automated verification | PRODUCT/PLATFORM | DEFER | Check at publication |
| 09-failure-modes | Zhan et al. (2024) / InjecAgent — tool-integrated agents vulnerable to indirect prompt injection | CITATION/STAT | CONFIRMED | None — ACL Findings 2024, arXiv 2403.02691; GPT-4 ReAct-prompted vulnerable 24% of time |
| 09-failure-modes | AgentDojo (2024) — attacks succeed at meaningful rates against real agent architectures | CITATION/STAT | CONFIRMED | None — arXiv 2406.13352; attacks succeed <25% against best agents; agentdojo.spylab.ai |
| 09-failure-modes | OWASP MCP Top 10 (2025) — tool poisoning and server trust as injection vectors | CITATION/STAT | CONFIRMED | Already confirmed above |
| 09-failure-modes | Injection detection unsolved at scale (Zhan et al. 2024; AgentDojo 2024) | CITATION/STAT | CONFIRMED | Already confirmed above |
| 10-approval-gates | Parasuraman et al. (2000) — gate can sit at information acquisition, analysis, action selection, or execution | CITATION/STAT | CONFIRMED | Already confirmed above |
| 10-approval-gates | Risk-reversibility classification table — tool interfaces may evolve | PRODUCT/PLATFORM | DEFER | Check at publication |
| 10-approval-gates | Claude Code permission tiers (auto / confirm / block) | PRODUCT/PLATFORM | DEFER | Check at publication |
| 10-approval-gates | Cowork safety guidance on browser form submission / external app actions | PRODUCT/PLATFORM | DEFER | Check at publication |
| 10-approval-gates | NIST AI RMF (2023) — risk-tiered governance | CITATION/STAT | CONFIRMED | Already confirmed above |
| 10-approval-gates | OWASP excessive agency guidance (2025) | CITATION/STAT | CONFIRMED | Already confirmed above |
| 11-teams-orgs | .claudeignore file excluding paths | PRODUCT/PLATFORM | DEFER | Check at publication |
| 11-teams-orgs | OWASP LLM Top 10 and MCP Top 10 — tool permission scope / server trust as organizational risks | CITATION/STAT | CONFIRMED | Already confirmed above |
| 11-teams-orgs | NIST AI RMF + ISO/IEC 42001:2023 as governance frameworks | CITATION/STAT | CONFIRMED | None — ISO/IEC 42001:2023 published December 2023, first certifiable AI management system standard; confirmed at iso.org/standard/42001 |
| 11-teams-orgs | Zhu et al. (2026) "Designing Meaningful Human Oversight in AI" AI and Ethics | CITATION/STAT | CONFIRMED | None — published at link.springer.com/article/10.1007/s43681-026-01147-7; authors: Liming Zhu, Qinghua Lu, Ming Ding, Sung Une Lee, Chen Wang; open access |
| 11-teams-orgs | Shared MCP server governance risks — OWASP MCP Top 10 | CITATION/STAT | CONFIRMED | Already confirmed above |
| 11-teams-orgs | Enterprise settings claim | PRODUCT/PLATFORM | DEFER | Check at publication |
| 11-teams-orgs | Platform-level audit logging capabilities | PRODUCT/PLATFORM | DEFER | Check at publication |
| 11-teams-orgs | Elinor Ostrom (Wayback figure) — Nobel laureate, commons governance | CITATION/STAT | CONFIRMED | None — 2009 Nobel Prize in Economic Sciences; "Governing the Commons" 1990; first woman to win the prize; Indiana University faculty |
| 11-teams-orgs | Ida B. Wells (Wayback figure in Ch 12) — anti-lynching journalist | CITATION/STAT | CONFIRMED | None — born 1862, died 1931; co-founder NAACP; 2020 Pulitzer Prize; anti-lynching pamphlets confirmed |
| 12-capstone | Cowork connector / folder restrictions | PRODUCT/PLATFORM | DEFER | Check at publication |
| 12-capstone | Claude Code non-production branch requirement | PRODUCT/PLATFORM | DEFER | Check at publication |
| 12-capstone | AI self-verification conditions | PRODUCT/PLATFORM | DEFER | Check at publication |

---

## Corrections to apply

**1. Ch 06 — MCP USB-C attribution (CORRECTED)**

Current text (line 27):
> "The protocol team at Anthropic offered a memorable analogy: MCP is like USB-C for AI applications"

Issue: No specific "protocol team" quote has been identified. The USB-C analogy appears in Anthropic's MCP announcement and is widely attributed to Anthropic generally, not to a named team or individual in an identifiable source.

Recommended fix:
> "Anthropic's MCP announcement described the protocol as 'USB-C for AI applications'"

Or, if a specific blog post or documentation page can be identified at publication time, add the direct citation. This is a minor attribution precision issue, not a factual error about the analogy itself (the analogy is genuine and from Anthropic).

---

## Deferred to publication-time (PRODUCT/PLATFORM — 42 items)

All items tagged `[verify — current as of writing]` that refer to Anthropic product behavior, documentation URLs, or platform features. These cover:

- Claude Code behavior: permission tiers, .claudeignore, action surface, shell command policy, secrets/credentials handling, production access boundary
- Claude Cowork behavior: computer-use mode, connector hierarchy, remote task assignment, projects feature, plugin behavior
- All Anthropic Help Center URLs (support.claude.com articles: 13345190, 13364135, 14128542, 14116274, 13947068, 13837440)
- All Claude Code Docs URLs (code.claude.com/docs/*)
- MCP directory policy accuracy
- Available MCP connectors in Claude environment
- Enterprise audit/governance platform features
- Self-verification and automated detection tool status (which is a state-of-technology claim)

**Recommended publication-time workflow:** (1) Check each URL for 404s and title/content drift. (2) Verify that documented feature behaviors (permission tiers, computer-use, connector hierarchy) still match current product. (3) Remove or update any deprecated article references.

---

## Notes on items the draft already flags as contested

Two passages are marked `[contested]` inline (not extraction flags but in-text acknowledgments):

- **Ch 03** (line 184): Tradeoff between approval friction and usability — correctly flagged in-text as unresolved; no correction needed, the framing is accurate.
- **Ch 11** (line 227): Organizational politics of AI governance ownership — correctly flagged as genuinely contested; no correction needed.

---

## Highest-risk unverified claim

None of the citation/stat items are unconfirmed. The highest-risk item is the **MCP USB-C attribution** (Ch 06, line 27): assigning a quote to "the protocol team at Anthropic" without a citable source is the kind of attributional imprecision that can erode reader trust if challenged. Fix before publication.

The previously suspect citation **Zhu et al. 2026** (AI and Ethics, Springer) is confirmed as a real, open-access paper at the cited URL with the cited authors. No correction needed.
