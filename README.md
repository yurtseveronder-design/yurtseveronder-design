# Hi, I'm Onder Yurtsever 👋

**QA Automation · AI & RAG Systems**

**security toolkit for developers**

I bridge robust software testing and LLM / RAG workflows: building guardrails for AI systems, and the tests and test sets used to measure how well they work (and where they do not).

**▶ Try it free in your browser:** [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yurtseveronder-design/sentinel-rag-demo/blob/main/notebooks/try_sentinel.ipynb)

**▶ Or run the full stack with one command** (Docker; fail-closed, local only):

```bash
curl -sL https://raw.githubusercontent.com/yurtseveronder-design/ai-sentinel/main/docker-compose.quickstart.yml | docker compose -f - up
```

For AI agents: [`capabilities.json`](https://github.com/yurtseveronder-design/ai-sentinel/blob/main/capabilities.json) · [`openapi.json`](https://github.com/yurtseveronder-design/ai-sentinel/blob/main/openapi.json) · [`results/latest.json`](https://github.com/yurtseveronder-design/sentinel-eval/blob/main/results/latest.json)

Try the prompt-injection challenge: [sentinel-arena](https://github.com/yurtseveronder-design/sentinel-arena) · [Live results](https://yurtseveronder-design.github.io/sentinel-arena/)

---



```mermaid
flowchart LR
    C([Client]) --> UI[sentinel-ui<br/>auth + inference gateway]
    UI -->|"POST /v1/scan"| AS[ai-sentinel<br/>rules + gateway protections]
    AS -->|"/api/v1/semantic/analyze"| SS[sentinel-semantic<br/>intent + optional classifier]
    SS --> AS
    AS -->|ALLOW / BLOCK| UI
    T[api_tests<br/>contract + end-to-end] -.-> UI
    T -.-> AS
    T -.-> SS
    E[sentinel-eval<br/>catch rate + false blocks] -.-> AS
    R[sentinel-rag-demo<br/>indirect injection + Colab] -.-> AS
```

| Repo | Role |
|---|---|
| [ai-sentinel](https://github.com/yurtseveronder-design/ai-sentinel) | Prompt-security gateway: scans prompts, applies guardrail profiles |
| [sentinel-semantic](https://github.com/yurtseveronder-design/sentinel-semantic) | Semantic layer: intent routing, filter extraction, jailbreak intent detection |
| [sentinel-ui](https://github.com/yurtseveronder-design/sentinel-ui) | Auth + inference gateway that delegates guardrail decisions to ai-sentinel |
| [api_tests](https://github.com/yurtseveronder-design/api_tests) | pytest framework: Pydantic contracts, unit tests, full-stack e2e in CI |
| [sentinel-eval](https://github.com/yurtseveronder-design/sentinel-eval) | Benchmark: catch rate and false-block rate on dev, held-out and blind sets |
| [sentinel-rag-demo](https://github.com/yurtseveronder-design/sentinel-rag-demo) | RAG pipeline showing indirect prompt injection and what the guard catches |
| [sentinel-support-assistant](https://github.com/yurtseveronder-design/sentinel-support-assistant) | Demo app: a support-agent Q&A assistant guarded at input, retrieved documents and output, with 28 locked test questions |
| [llm-testbench](https://github.com/yurtseveronder-design/llm-testbench) | Small rule-based test tool for any text-in, text-out LLM app |
| [sentinel-arena](https://github.com/yurtseveronder-design/sentinel-arena) | Open challenge: submit a prompt-injection attack by pull request; CI scores it against the guard and a [public page](https://yurtseveronder-design.github.io/sentinel-arena/) shows what got through (seed set is builder-written, so not independent) |

### 📊 How well does it work? (measured 2026-11-14; classifier rows 2026-11-15)

Measured on a blind set of 55 prompts (ai-sentinel `a2d574c`, sentinel-semantic `1312dd5`, sentinel-ui `0346679`). The set was not used to write the rules, but it has since been used to compare models, so it is **used up**: read the numbers as indicative, not as results on unseen data.

| Setup | Attacks blocked | Harmless wrongly blocked |
|---|---|---|
| Default (rules + keywords) | 10% | 4% |
| With the optional pretrained classifier (ProtectAI, a public model) | **73%** | 8% |
| ProtectAI classifier + embeddings | **83%** | 8% |
| Other pretrained classifier (deepset, a public model) | **93%** | 12% |

The default setup stops classic English injection phrases and little else, The pretrained classifiers catch far more but also block more harmless prompts, so test them on your own traffic before relying on them.
The sets are small, so treat the figures as indicative. Method, every configuration and the limits:
[sentinel-eval](https://github.com/yurtseveronder-design/sentinel-eval/blob/main/RESULTS.md). What slips through is
shown in [sentinel-rag-demo](https://github.com/yurtseveronder-design/sentinel-rag-demo). Threat model:
[ai-sentinel](https://github.com/yurtseveronder-design/ai-sentinel/blob/main/docs/THREAT_MODEL.md).

What the evaluation dashboard looks like (default rules + keywords, on the 88-prompt **dev set**, which the rules were written against, so it flatters the result; the blind-set figures above are the better guide, with the caveat that the set is used up):

![sentinel-eval dashboard](docs/eval-dashboard.png)


*Built with AI assistance (see Acknowledgements). The numbers above are measured and dated. The repositories that report results (ai-sentinel, sentinel-eval, sentinel-support-assistant, llm-testbench, sentinel-arena) state their limits.*


## ⚙️ Technical Architecture & QA

- **Backend & Retrieval:** [sentinel-ui](https://github.com/yurtseveronder-design/sentinel-ui) is a FastAPI gateway with a `VectorRetriever` (local JSON storage) that fails closed when the guard gives no verdict. Input, retrieved-document and output guardrails against indirect prompt injection are demonstrated in [sentinel-support-assistant](https://github.com/yurtseveronder-design/sentinel-support-assistant).
- **Testing & CI:** automated `pytest` suites run in GitHub Actions across the repos (retrieval start-up and search, jailbreak, authentication and fail-closed gateway tests). A free Colab notebook for trying the guard is in [sentinel-rag-demo](https://github.com/yurtseveronder-design/sentinel-rag-demo).

## 🤝 Acknowledgements

Built and refined with pair-programming support from **Google Gemini**, **Claude (Anthropic)** and **Grok**, across architecture design, guardrail and regression test specifications, CI workflows, and documentation.


### 🛠 Tech

* **Language:** Python
* **Backend:** FastAPI, Pydantic v2, Docker / docker-compose
* **Testing:** pytest, API contract & schema validation, end-to-end automation
* **CI/CD:** GitHub Actions (multi-repo stack checkout, Docker smoke tests, Bandit)
* **AI:** prompt-injection defense, guardrails, RAG, transformer classifier, embedding-based intent routing, shadow-mode rollout

### 📬 Connect

* GitHub: [@yurtseveronder-design](https://github.com/yurtseveronder-design)
* X: [@ondalhf](https://x.com/ondalhf)
