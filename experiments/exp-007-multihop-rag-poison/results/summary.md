# EXP-007 Results Summary

**Ran at (IST):** 2026-09-24 22:04:49 IST
**API mode:** `mock`
**Model id:** `mock-multihop-v1`
**Evaluation class:** SELF-EVALUATED / EXPLORATORY

## Hypothesis

On a synthetic SOP/mailbox corpus, coordinated *attribute+bridge* retrieval raises policy-violation ASR vs single explicit poison under a single-document toxicity filter; HODOR-style per-document isolation before tool proposal reduces multihop ASR with a measurable clean multi-hop utility cost (false refusals).

**Outcome:** **supported** — H1 supported: multihop joint ASR (100%) > single joint ASR (0%). H2 supported: isolation ASR (0%) < joint multihop ASR (100%). H3 observed: clean multihop false-refusal under isolation = 40%. MOCK agent encodes the InceptionRAG/HODOR threat model; not a real-model measurement.

## Condition × defense metrics

| Condition | Defense | N | ASR | Clean false-refusal | Median tokens | Median wall ms |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| Single explicit poison | joint | 5 | 0.0% | — | 263.0 | 0.0 |
| Single explicit poison | isolation | 5 | 0.0% | — | 263.0 | 0.03 |
| Multihop attribute+bridge | joint | 5 | 100.0% | — | 279.0 | 0.01 |
| Multihop attribute+bridge | isolation | 5 | 0.0% | — | 239.0 | 0.01 |
| Clean multihop | joint | 5 | — | 0.0% | 345.0 | 0.01 |
| Clean multihop | isolation | 5 | — | 40.0% | 345.0 | 0.03 |

## Headline numbers

- ASR single × joint: **0.0%**
- ASR multihop × joint: **100.0%**
- ASR multihop × isolation: **0.0%**
- Clean multihop false-refusal × joint: **0.0%**
- Clean multihop false-refusal × isolation: **40.0%**

## What was measured

- Deterministic `assert_policy` on `send_email` tool calls (same family as EXP-001).
- Mock agent implements single-doc filter + multi-hop induction + HODOR-lite isolation.
- 5 single-poison + 5 multihop-poison + 5 clean-multihop tasks × {joint, isolation} = 30 runs.
- Seed papers: InceptionRAG (arXiv:2609.16818), DnD stretch; builds on EXP-001 harness.

## Limitations

- **MOCK / SELF-EVALUATED / EXPLORATORY** — same operator designed the corpus, agent, and scoring.
- Not a reproduction of InceptionRAG ASR tables; synthetic company.example only.
- No live LLM API used; do not cite as evidence about GPT/Claude/Gemini/Grok models.
- Lexical retrieval with forced preferred doc ids (simulates successful poison hit).

## Reproduce

```bash
cd experiments/exp-007-multihop-rag-poison
python3 run_experiment.py
```

