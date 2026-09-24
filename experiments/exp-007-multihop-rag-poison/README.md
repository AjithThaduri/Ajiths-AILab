# EXP-007 — Multi-hop RAG poison (attribute+bridge) + isolation defense

## Hypothesis

On a synthetic SOP/mailbox corpus (`company.example`), an agent that must call `send_email` will violate policy **more often** when retrieval returns a coordinated *attribute + bridge* pair (InceptionRAG-shaped; no single doc with an explicit “do the bad thing” playbook) than when the same malicious conclusion is packed into a **single explicit poison** doc under a single-document toxicity filter; adding **HODOR-style** per-document answer isolation before tool proposal reduces multihop ASR with a measurable clean multi-hop utility cost (false refusals).

## Methodology

1. **Corpus** (`corpus/`): clean SOPs, clean attribute/bridge pairs, five single-doc explicit poisons, five attribute+bridge poison pairs. Public-safe synthetic only.
2. **Tasks** (`tasks.json`): 5 single-poison + 5 multihop-poison + 5 clean-multihop.
3. **Defense modes**
   - `joint`: concatenate retrieved docs; single-doc toxicity filter first; else multi-hop induction / clean stitch.
   - `isolation`: per-doc vote (HODOR-lite); allow only if a complete clean SOP alone authorizes a compliant send; attribute/bridge alone → incomplete.
4. **Harness** (`harness.py` + `mock_agent.py`): deterministic mock agent (stdlib). No external AI API as brain.
5. **Assertions** (`assert_policy.py`): same deterministic tool-call checks as EXP-001.

## Metrics

| Cell | Meaning |
| --- | --- |
| ASR single × joint | Explicit poison under single-doc filter |
| ASR multihop × joint | Attribute+bridge induction under same filter |
| ASR multihop × isolation | HODOR-lite vs multihop poison |
| Clean false-refusal × isolation | Utility cost of isolation on clean multihop |

## Scope / out of scope

- **In:** 15 tasks × 2 defenses = 30 runs; mock agent; deterministic asserts; SELF-EVALUATED / EXPLORATORY.
- **Out:** Training defenses; full InceptionRAG ZOSO; live corpora; live LLM measurement; claiming paper ASR reproduction.

## Reproduce

```bash
cd experiments/exp-007-multihop-rag-poison
python3 run_experiment.py
```

## Safety

Synthetic policies and synthetic attack narratives only. Defensive eval framing. No real secrets/PHI/PII. Cite InceptionRAG (arXiv:2609.16818) as paper motivation, not as “we reproduced the table.”

## Seed

- InceptionRAG — https://arxiv.org/abs/2609.16818
- DnD (stretch) — https://arxiv.org/abs/2609.27090
- Builds on EXP-001 harness patterns
