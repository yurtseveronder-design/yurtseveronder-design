# Hi, I'm Onder Yurtsever 👋

**QA Automation · AI & RAG Systems**
**security toolkit for developers**

I bridge robust software testing and LLM / RAG workflows: building guardrails for AI systems, and the test harness that proves they work.

---

### 🧩 One system, six repos

```
client ──▶ sentinel-ui ──▶ ai-sentinel ──▶ sentinel-semantic
           (gateway/auth)   /v1/scan        /api/v1/semantic/analyze
                              (guardrails)   (intent + filters)

                        api_tests = contract + end-to-end suite for all three
```

| Repo | Role |
|---|---|
| [ai-sentinel](https://github.com/yurtseveronder-design/ai-sentinel) | Prompt-security gateway: scans prompts, applies guardrail profiles |
| [sentinel-semantic](https://github.com/yurtseveronder-design/sentinel-semantic) | Semantic layer: intent routing, filter extraction, jailbreak intent detection |
| [sentinel-ui](https://github.com/yurtseveronder-design/sentinel-ui) | Auth + inference gateway that delegates guardrail decisions to ai-sentinel |
| [api_tests](https://github.com/yurtseveronder-design/api_tests) | pytest framework: Pydantic contracts, unit tests, full-stack e2e in CI |
| [sentinel-eval](https://github.com/yurtseveronder-design/sentinel-eval) | Benchmark: catch rate and false-block rate on dev, held-out and blind sets |
| [sentinel-rag-demo](https://github.com/yurtseveronder-design/sentinel-rag-demo) | RAG pipeline showing indirect prompt injection and what the guard catches |

### 📊 How well does it work? (measured 2026-11-15)

On a blind set of 55 prompts the system never saw while it was being built:

| Setup | Attacks blocked | Harmless wrongly blocked |
|---|---|---|
| Default (rules + keywords) | 10% | 4% |
| With the optional trained classifier | **73%** | 8% |
| Classifier + embeddings | **83%** | 8% |

The default setup stops classic English injection phrases and little else, so turn the classifier on for real use.
The sets are small, so treat the figures as indicative. Method, every configuration and the limits:
[sentinel-eval](https://github.com/yurtseveronder-design/sentinel-eval/blob/main/RESULTS.md). What slips through is
shown in [sentinel-rag-demo](https://github.com/yurtseveronder-design/sentinel-rag-demo). Threat model:
[ai-sentinel](https://github.com/yurtseveronder-design/ai-sentinel/blob/main/docs/THREAT_MODEL.md).

### 🛠 Tech

* **Language:** Python
* **Backend:** FastAPI, Pydantic v2, Docker / docker-compose
* **Testing:** pytest, API contract & schema validation, end-to-end automation, coverage gates
* **CI/CD:** GitHub Actions (multi-repo stack checkout, Docker smoke tests, Bandit)
* **AI:** prompt-injection defense, guardrails, RAG, transformer classifier, embedding-based intent routing, shadow-mode rollout

### 📬 Connect

* GitHub: [@yurtseveronder-design](https://github.com/yurtseveronder-design)
* X: [@ondalhf](https://x.com/ondalhf)
