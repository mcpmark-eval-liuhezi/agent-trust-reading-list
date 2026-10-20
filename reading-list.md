# Agent-Trust Reading List

Theme: **agentic search — how much do people trust the answers they get back from conversational search agents?**

Papers were found via two arXiv sweeps: (1) tool use by LLM-driven agents, and (2) trust in conversational search. Five papers made the cut and are listed below in reading order.

---

## 1. arXiv:2604.00835 — Agentic Tool Use in Large Language Models: A Survey

**Authors:** Jinchao Hu, Meizhi Zhong, Kehai Chen, Xuefeng Bai, Min Zhang

**Takeaway:** This survey organizes LLM tool use into three paradigms — prompting as plug-and-play, supervised tool learning, and reward-driven tool policy learning — distinguished by what optimization signal drives the behavior (in-context control, supervised data, or reward feedback). For agentic search specifically, it explains how retrieval APIs and code interpreters became the standard fix for static knowledge and hallucination, while also showing that tool access alone degrades over long horizons as agents trigger excessive, low-quality tool calls. It is useful background for the session because it describes the machinery that *produces* an agentic search answer, which is only half of the trust story.

## 2. arXiv:2403.09987 — Trusting the Search: Unraveling Human Trust in Health Information from Google and ChatGPT

**Authors:** Xin Sun, Rongjun Ma, Xiaochang Zhao, Zhuying Li, Janne Lindqvist, Abdallah El Ali, Jos A. Bosch

**Takeaway:** In a within-subjects lab study (N=21) on health information seeking, participants trusted ChatGPT significantly more than Google (F(1,20)=6.73, p=.017), with trust in the retrieved information averaging 4.05 vs. 3.77 and trust in the agent 3.58 vs. 3.31. Notably, trust in the information correlated with trust in the agent only for Google — for ChatGPT the two came apart — and search-task type had no significant effect, with prior knowledge, presentation style, and the interactive manner of searching driving trust instead. The uncomfortable reading is that the conversational experience itself, rather than the evidence behind an answer, is doing a lot of the trust work.

## 3. arXiv:2608.21177 — From Search Agents to Dissemination Interfaces: Understanding Human Trust in Health Information from Conversational Search

**Authors:** Xin Sun, Rongjun Ma, Xiaochang Zhao, Janne Lindqvist, Jan de Wit, Zhuying Li, Abdallah El Ali, Jos A. Bosch

**Takeaway:** This paper extends the Google-vs-ChatGPT comparison into two studies: a replication confirming higher trust in ChatGPT-sourced health information, and a second study (N=20) delivering *identical* LLM content through text, speech, and embodied interfaces. Trust differed significantly across interfaces (text vs. embodied β=.189, p=.035; speech vs. embodied β=.180, p=.002), and usability fully mediated the interface→trust relationship, meaning the channel shaped trust even though the underlying information never changed. The core contribution for our session is the decomposition of trust into three separable objects — the answer, the search agent, and the dissemination interface — which gives us a vocabulary for arguing about what exactly a user is trusting.

## 4. arXiv:2504.06435 — Human Trust in AI Search: A Large-Scale Experiment

**Authors:** Haiwen Li, Sinan Aral

**Takeaway:** Using a preregistered, randomized experiment on a U.S.-representative sample (after auditing ~12,000 queries yielding ~80,000 real search results across seven countries), this paper causally shows that interface design moves trust independent of accuracy. Participants trusted generative search less than traditional search on average — yet reference links and citations significantly *increased* trust even when those links were hallucinated, invalid, or broken, a "veneer of rigor" effect that hit Democrats and lower-education, lower-experience users hardest. Uncertainty highlighting cut trust and willingness to share, positive social feedback raised it, and higher trust predicted more clicking with less time spent evaluating results, making this the clearest evidence in the set that trust in agentic search is a design variable rather than a fact-checking outcome.

## 5. arXiv:2605.28498 — The Decision to Verify: How Warmth and User Characteristics Shape Reliance on Conversational Agents for Information Search

**Authors:** Mert Yazan, Frederik Bungaran Ishak Situmeang, Suzan Verberne

**Takeaway:** In a mixed-subjects QA experiment (n=199) with a GPT-4.1 chatbot whose answer correctness was randomized and whose every participant interaction was logged via browser extension, reliance persisted even though users had web search available alongside the chatbot. The decision to verify was driven almost entirely by user characteristics (prior trust in chatbots, digital literacy) rather than answer properties — question variance was effectively zero while participant variance was large — and a warm conversational style increased agreement with the chatbot specifically when it was wrong. Counterintuitively, consulting *additional AI* sources predicted higher answer accuracy while traditional web search did not, suggesting the fix for overreliance is not more tool access but changing who decides to use it.

---

## Search provenance

- Sweep 1 (tool use by LLM agents): arXiv:2604.00835 selected as the survey anchor; other hits (AutoTool 2511.14650, entropy-based tool-use optimization 2602.02050, AgentMath 2512.20745, and others) were domain-specific rather than search/trust focused.
- Sweep 2 (trust in conversational search): arXiv:2403.09987, 2608.21177, 2504.06435, and 2605.28498 selected; adjacent hits on trust measurement (2010.04885), conversational recommender trust (2203.12981), and advertising risk (2506.06447) were off-topic for this session.
