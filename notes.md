# Session Notes — Agentic Search & Trust in Conversational Search Agents

Longer write-ups for the five papers on the reading list, prepared for our reading-group session. Each section covers what the paper actually did, what it found, and how it connects to the session theme. The short versions live in [`reading-list.md`](../blob/main/reading-list.md).

---

## arXiv:2604.00835 — Agentic Tool Use in Large Language Models: A Survey

**Authors:** Jinchao Hu, Meizhi Zhong, Kehai Chen, Xuefeng Bai, Min Zhang

**What it does.** A survey of LLM tool use that organizes the literature into three paradigms, distinguished by the optimization signal behind the tool-use behavior: (I) *prompting as plug-and-play*, where a frozen model is steered through prompts and in-context interaction (ReAct, Reflexion, Self-Refine, HuggingGPT, program-aided reasoning like PAL/ViperGPT); (II) *supervised tool learning*, where tool-use patterns are internalized via labeled or synthetic supervision (Toolformer's self-annotation trick, ToolLLM/ToolBench's 16,000+ real-world RESTful APIs, Gorilla's retrieval-aware training, APIGen and ToolACE's verification pipelines); and (III) *reward-driven tool policy learning*, which optimizes long-horizon interaction with reinforcement signals. Evaluation is treated as a cross-cutting dimension, evolving from function-call correctness toward end-to-end interactive success, safety, and robustness.

**What stands out.** Toolformer's core criterion is elegant: keep a tool call only if inserting its result measurably improves next-token prediction — i.e., a call is "useful" because it reduces prediction loss, not because it's syntactically valid. The survey also documents how the field moved from bootstrapping demonstrations to caring about data quality control (executable verification in APIGen, hierarchical validation in ToolACE), and it flags long-horizon failure modes: agents in extended trajectories trigger excessive, low-quality tool calls that inflate latency and degrade final answers.

**Why it matters for our session.** This is the "supply side" of agentic search. Every trust finding elsewhere in this list lands on top of the machinery described here — retrieval APIs grafted onto an LLM to patch static knowledge and hallucination, with the residual risk that over long horizons the agent over-calls tools or calls them badly. The trust papers show users can't see any of this; the visible artifact is a confident conversational answer. Reading the survey first makes the later papers' trust gaps concrete: what users are asked to trust is a composite of a model, a tool policy, and whatever the tools returned.

**Discussion questions.**
1. Does the three-paradigm taxonomy (prompt / supervised / reward) change how we should think about *calibrating* trust — is a reward-trained tool policy more or less predictable to a user than a prompted one?
2. If long-horizon tool-calling degrades answer quality, how should that risk be surfaced to a user who has no way to inspect the trajectory?
3. Which evaluation levels in the survey's landscape (function-call correctness vs. end-to-end interactive success) come closest to measuring what a user actually bases trust on?

---

## arXiv:2403.09987 — Trusting the Search: Unraveling Human Trust in Health Information from Google and ChatGPT

**Authors:** Xin Sun, Rongjun Ma, Xiaochang Zhao, Zhuying Li, Janne Lindqvist, Abdallah El Ali, Jos A. Bosch

**What it does.** A mixed-methods, within-subjects lab study (N=21) in which each participant completed three health search tasks using Google and three using ChatGPT, counterbalanced, followed by a ~25-minute semi-structured interview per participant (516 minutes of transcripts total). Trust was measured three ways: trust in the retrieved information (validated 11-item "Trust of Online Health Information" scale, α=.95), trust in the search agent itself (15-item "Model of Online Trust" scale), and prospective intention to use the agent.

**What stands out.** Participants trusted ChatGPT more than Google on both measures — trust in information 4.05 vs. 3.77 (F(1,20)=6.73, p=.017, η²=.057), trust in the agent 3.58 vs. 3.31 (t(21)=-2.53, p=.02, d=0.55). Two details are more interesting than the headline. First, search-task type had *no* significant effect (F(2,40)=0.63, p=.538): informational, treatment/advice, and symptom/diagnosis questions all produced similar trust, which is mildly alarming for a domain where stakes vary enormously. Second, trust in the information and trust in the agent correlated significantly only for Google — for ChatGPT, the two came apart, so users were judging the answer separately from their feelings about the tool. The thematic analysis points to prior knowledge, presentation style, and interactive manner as the trust drivers, and the paper frames ChatGPT as a "stepping stone for further search" rather than a terminal answer.

**Why it matters for our session.** This is the baseline finding for the session theme: in a high-stakes domain, the conversational agent already out-trusts the incumbent search engine, and the trust appears to be attached to the interaction rather than to the evidence. The paper deliberately treats ChatGPT as a *search agent*, not just a chatbot, which is exactly the framing our session needs.

**Discussion questions.**
1. The Google trust-in-agent ↔ trust-in-information correlation existed; the ChatGPT one didn't. What does it mean to trust an answer you don't trust the source of?
2. N=21, 76% female, 71% aged 18–24, mostly social-science students. How far do we let these findings travel?
3. If task type doesn't move trust, what would? Which trust-relevant dimensions does this design simply not capture?

---

## arXiv:2608.21177 — From Search Agents to Dissemination Interfaces: Understanding Human Trust in Health Information from Conversational Search

**Authors:** Xin Sun, Rongjun Ma, Xiaochang Zhao, Janne Lindqvist, Jan de Wit, Zhuying Li, Abdallah El Ali, Jos A. Bosch

**What it does.** Two mixed-methods studies, both in the health domain. Study 1 (N=21) replicates and extends the Google-vs-ChatGPT comparison across three task types. Study 2 (N=20) holds the underlying LLM constant and varies only the *dissemination interface* — text-based, speech-based, and embodied — so any trust difference is attributable to the channel rather than the content. The paper is published in *Behaviour & Information Technology*.

**What stands out.** Study 1 confirmed the ChatGPT trust advantage (4.05 vs. 3.77 for information trust; 3.58 vs. 3.31 for agent trust). Study 2 found significant trust differences across interfaces even with identical content: text vs. embodied (β=.189, p=.035) and speech vs. embodied (β=.180, p=.002), and a mediation analysis showed usability *fully* mediated the interface→trust relationship (indirect β=.154, p<.001; direct effect non-significant). The qualitative themes explain the mechanism: participants found reading less effortful than listening, could scroll back and re-check text but not replay speech, and found the embodied interface's non-verbal cues added cognitive load rather than clarity. Familiarity did real work too — text interfaces benefited from resemblance to WhatsApp and to reading professional literature.

**Why it matters for our session.** This paper contributes the conceptual decomposition that structures the whole session: trust in the answer, trust in the search agent, and trust in the dissemination interface are three different objects, and Study 2 shows the interface alone moves trust even when information is held fixed. It also carries a practical warning — "human-like" features, the very ones vendors ship to make agents feel trustworthy, can reduce the trustworthiness of the encounter by raising processing cost and triggering authenticity concerns.

**Discussion questions.**
1. If usability fully mediates interface→trust, is "trust in agentic search" partly just an interface-design metric in disguise?
2. Voice and embodied agents scored lower on trust here. Does that mean they're safer, or just worse at manufacturing trust? What's the right normative target?
3. Where does trust in a *tool-using agent* sit in this three-way decomposition — is the agent the "search agent," the "interface," or something the taxonomy doesn't yet have a slot for?

---

## arXiv:2504.06435 — Human Trust in AI Search: A Large-Scale Experiment

**Authors:** Haiwen Li, Sinan Aral

**What it does.** The strongest causal evidence in the set. The authors first ran ~12,000 search queries (11,372 executed via serpAPI) across seven countries, generating ~80,000 (79,604) real GenAI and traditional search results, to quantify current global exposure to generative search. They then ran a preregistered, randomized experiment on a large sample representative of the U.S. adult population, holding the AI models and their outputs constant while randomizing only the *design* of the generative search interface. Robustness is taken seriously: attrition was low (2.62%) and balanced across arms, 47 of 51 covariates balanced, randomization inference confirmed significance for all but one result, and three placebo tests came back clean.

**What stands out.** The central result is uncomfortable: participants trusted GenAI search less than traditional search on average, *but* reference links and citations significantly increased trust in GenAI even when those links were hallucinated, invalid, or broken — a "veneer of rigor" effect. The vulnerability is unevenly distributed: Democrats and those with less education and less GenAI experience were induced to trust more by references than Republicans or more educated/experienced users; Republicans, the more educated, and the more GenAI-experienced trusted GenAI more overall. Uncertainty highlighting (exposing the system's confidence) *reduced* both trust and willingness to share, whether confidence was high or low. Positive social feedback raised trust, negative lowered it. Trust also predicted behavior: higher-trust participants clicked more on GenAI results and spent *less* time evaluating them. Topic mattered too — highest trust for climate-change information, lowest for gun control across every condition.

**Why it matters for our session.** This is the paper that reframes the question. Trust in agentic search is not primarily a fact-checking outcome; it is a design variable that can be tuned up or down independently of whether the information deserves it. The most striking implication is that the industry's default trust affordance — citations — manufactures trust precisely when it is least warranted, while the affordance that would honestly communicate uncertainty suppresses trust even when confidence is legitimate.

**Discussion questions.**
1. Citations increase trust even when hallucinated. Should we conclude that citation-style interfaces are net-harmful, or is the right response citation *verification* rather than citation removal?
2. Uncertainty highlighting reduced trust regardless of confidence level — including for answers that were right. How do you design calibrated trust when the honest signal gets punished?
3. Trust varied by party, education, and GenAI experience. What does it mean to "design for" populations that are differentially vulnerable to manufactured trust?
4. The lab can't be the field here — the authors note only search engines can run these experiments in the wild, and they won't publish them. Is preregistered lab work enough for policy?

---

## arXiv:2605.28498 — The Decision to Verify: How Warmth and User Characteristics Shape Reliance on Conversational Agents for Information Search

**Authors:** Mert Yazan, Frederik Bungaran Ishak Situmeang, Suzan Verberne

**What it does.** A mixed-subjects QA experiment (n=199) with a GPT-4.1 chatbot (web-search tool enabled, temperature 0.7 for initial answers, 0 thereafter, instructed to give short answers with source links). Answer correctness was randomized so each participant saw the chatbot be right about half the time. Participants were randomly assigned a *warm* or *neutral* chatbot and could freely use other sources, simulating today's hybrid chatbot-plus-web-search paradigm. Crucially, the authors instrumented behavior properly: a custom browser extension logged every URL visited, letting them distinguish AI-related sources (other chatbots, AI summaries) from ordinary web pages, and to count both verification frequency and verification type — rather than relying on the self-reported binary "did you check" used in prior work.

**What stands out.** Reliance persisted despite fact-checking tools being one click away, and the decision to verify was almost entirely a *person* variable, not a question variable: participant variance was extremely high while question variance was effectively zero. The warm style worked indirectly — it increased agreement with the chatbot specifically when the chatbot was *wrong*. The most counterintuitive finding is about verification *type*: consulting additional AI sources predicted higher answer accuracy (between-participant effect, p<.001), while traditional web search did not. In the open-ended responses, participants split cleanly into always-fact-checkers (n=33), never-checkers (n=51), and conditional checkers (n=115), and the most common stated reason for picking an answer was *agreement between multiple sources* — which is worrying when the "multiple sources" are one LLM queried twice. High-trust participants also used the chatbot itself as their verification tool, seeking alignment with the original answer rather than independent confirmation.

**Discussion questions.**
1. "Multiple sources agreed" was the top justification for trusting an answer — but the sources were often one AI asked repeatedly. Is source-consistency a valid trust heuristic in agentic search, or is it a bug masquerading as diligence?
2. Warmth increased agreement only when the chatbot was wrong. Should conversational warmth be treated as a risk factor for misinformation in search UIs?
3. Additional AI helped accuracy; traditional web search didn't. What does that imply about where verification effort should be pointed?
4. If verification is a stable trait rather than a situational response, are interventions aimed at the moment of the answer mis-aimed — and what would a trait-level intervention even look like?

---

## Cross-cutting observations

- **The trust target is unclear, and that's the problem.** Across all five papers, "trust" attaches to different objects — the answer, the agent, the interface, the tool policy — and users (and often the studies) don't distinguish them. The Sun et al. decomposition (answer / agent / interface) is a good starting vocabulary for the session.
- **Trust is manufactured by design, not earned by accuracy.** Li & Aral show citations raise trust even when hallucinated; Yazan et al. show warmth raises agreement specifically when the agent is wrong. Two independent mechanisms, same direction.
- **Tool access doesn't fix trust.** The survey documents the tool-calling machinery; Yazan et al. shows that putting web search one click away doesn't curb reliance. Availability of verification ≠ use of verification.
- **Who is vulnerable is not uniform.** Trust effects vary by education, prior GenAI experience, political identity, prior trust in chatbots, and default checking habits — meaning "average trust" numbers understate the problem.
- **A open methodological gap:** nobody in this set measures trust in the *tool-using pipeline* itself (did the agent call the right tool, read the right result, degrade over a long trajectory?). Every study treats the composite answer as the only observable. A study that paired the survey's tool-trajectory view with a user-facing trust measure would be a genuine contribution.
