# Hi, I'm Onder Yurtsever 👋

**QA Automation · AI & RAG Systems**

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

### 📊 How well does it work? (measured 2026-11-14)

On a blind set of 55 prompts the system never saw while it was being built, the default setup blocks about **10%** of
attacks and wrongly blocks 4% of harmless prompts. With the embedding semantic layer it reaches **47%** at a
similar false-block rate (73% with more false blocks). It reliably stops classic English injection phrases and little
else; the gap is documented, not hidden. Method and every number: [sentinel-eval](https://github.com/yurtseveronder-design/sentinel-eval/blob/main/RESULTS.md).
Demo of what it stops (and what slips through): [sentinel-rag-demo](https://github.com/yurtseveronder-design/sentinel-rag-demo).

### 🛠 Tech

* **Language:** Python
* **Backend:** FastAPI, Pydantic v2, Docker / docker-compose
* **Testing:** pytest, API contract & schema validation, end-to-end automation, coverage gates
* **CI/CD:** GitHub Actions (multi-repo stack checkout, Docker smoke tests, Bandit)
* **AI:** prompt-injection defense, guardrails, RAG, embedding-based intent routing

### 📬 Connect

* GitHub: [@yurtseveronder-design](https://github.com/yurtseveronder-design)
* X: [@ondalhf](https://x.com/ondalhf)
