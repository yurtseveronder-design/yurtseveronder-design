# Hi, I'm Onder Yurtsever 👋

**QA Automation · AI & RAG Systems**

I bridge robust software testing and LLM / RAG workflows: building guardrails for AI systems, and the test harness that proves they work.

---

### 🧩 One system, four repos

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

### 🛠 Tech

* **Language:** Python
* **Backend:** FastAPI, Pydantic v2, Docker / docker-compose
* **Testing:** pytest, API contract & schema validation, end-to-end automation, coverage gates
* **CI/CD:** GitHub Actions (multi-repo stack checkout, Docker smoke tests, Bandit)
* **AI:** prompt-injection defense, guardrails, RAG, embedding-based intent routing

### 📬 Connect

* GitHub: [@yurtseveronder-design](https://github.com/yurtseveronder-design)
* X: [@ondalhf](https://x.com/ondalhf)
