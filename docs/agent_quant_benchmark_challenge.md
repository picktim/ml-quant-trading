# Agent Quant Benchmark Challenge

Can your coding agent reproduce a 213-factor, cost-aware quant research
pipeline without turning the result into an unsupported trading claim?

This challenge turns `ml-quant-trading` into a concrete reproducibility target
for coding agents, quant agents, and agent harnesses. The goal is not to prove
alpha. The goal is to test whether an agent can read a real research codebase,
run a fixed workflow, preserve evidence, and report caveats honestly.

## Why this challenge exists

Quant repositories often get cloned more than they get starred. That is
understandable: users may be evaluating privately, avoiding public signals, or
testing ideas on proprietary infrastructure.

This challenge creates a safer public path:

- agents can run zero-account synthetic and public-data workflows;
- users can submit redacted environment and benchmark notes;
- failures, unstable outputs, and cost-sensitive results are accepted;
- reports stay useful for reproducibility and citation without exposing private
  alpha, positions, accounts, or vendor data.

Announcement and coordination thread:
[`Discussion #66`](https://github.com/initial-d/ml-quant-trading/discussions/66).

## Tracks

| Track | Entry point | Report template | What it tests |
| --- | --- | --- | --- |
| Zero-account smoke test | `mlquant demo` | Reproduction report | Can the agent install, run, and preserve generated reports? |
| Protocol v1 CPU benchmark | `scripts/benchmark_tensor_factors.py` | Benchmark result | Can the agent follow a fixed performance protocol? |
| DeepSeek Harness run | `docs/deepseek_harness_recipe.md` | DSH benchmark report | Can the harness run, validate, and draft an issue-ready report? |
| Public-data validation | `docs/public_data_validation.md` | Public-data validation | Can the agent keep data source, costs, turnover, and caveats attached? |
| Private or institutional evaluation | `docs/private_evaluation_checklist.md` | Private evaluation note | Can users share useful redacted evidence without leaking strategy details? |

## Recommended first run

For the lowest-friction public run:

```bash
python -m pip install --upgrade mlquantx
mlquant demo
```

The demo uses deterministic synthetic data. It is a smoke test for the research
pipeline, not evidence of live or out-of-sample profitability.

For an agent benchmark, ask the agent to run the fixed protocol v1 CPU command:

```bash
python scripts/benchmark_tensor_factors.py \
  --device cpu --n-dates 750 --n-stocks 1000 --window 20 \
  --repeat 10 --warmup 3 --threads 1 --interop-threads 1 --seed 42 \
  --json-out artifacts/benchmark-v1.json
```

## Suggested agent prompt

```text
Read AGENTS.md, README.md, docs/reality_check.md, docs/benchmarking.md,
docs/agent_reproducibility.md, and docs/agent_quant_benchmark_challenge.md.
Run one challenge track exactly as documented. Preserve the commit SHA, command,
environment, generated Markdown/JSON artifacts, warnings, retries, and caveats.
Do not describe runtime, synthetic data, or public-data backtests as trading
alpha. Draft an issue-ready report using the appropriate template.
```

## Report links

- [Challenge discussion](https://github.com/initial-d/ml-quant-trading/discussions/66)
- [Reproduction report](https://github.com/initial-d/ml-quant-trading/issues/new?template=reproduction_report.yml)
- [Benchmark result](https://github.com/initial-d/ml-quant-trading/issues/new?template=benchmark_result.yml)
- [DeepSeek Harness benchmark report](https://github.com/initial-d/ml-quant-trading/issues/new?template=deepseek_harness_benchmark.yml)
- [Public-data validation](https://github.com/initial-d/ml-quant-trading/issues/new?template=public_data_validation.yml)
- [Private evaluation note](https://github.com/initial-d/ml-quant-trading/issues/new?template=private_evaluation_note.yml)

## What a good report includes

- repository commit SHA or release tag;
- exact command and agent prompt;
- environment: OS, Python, PyTorch, CPU/GPU, CUDA availability, thread settings;
- generated report paths and JSON artifacts;
- raw tables or aggregate metrics;
- warnings, failures, retries, and local changes;
- data source category and public/private boundary;
- transaction-cost assumptions for any backtest-like result;
- a short interpretation that stays inside the evidence.

Negative results are welcome. A report that exposes a setup problem, unstable
data path, leakage concern, cost sensitivity, or documentation gap is useful.

## What not to post

Do not post:

- API keys, broker credentials, cookies, tokens, or account identifiers;
- raw proprietary market data or vendor-licensed files;
- live positions, holdings, fills, order logs, or execution venues;
- private alpha definitions, factor weights, or production trading rules;
- internal hostnames, client names, private notebooks, or firm-identifying paths.

## Positioning

This challenge is deliberately narrower than a full quant platform comparison.
It asks one auditable question:

> Can an agent reproduce a documented quant research workflow, keep the evidence
> bundle intact, and avoid overstating the result?

That makes the repository useful as a benchmark target for agent research,
reproducible quantitative-finance workflows, and implementation-focused papers.
