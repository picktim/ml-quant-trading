# Private evaluation checklist

Many users evaluate quantitative research code without publicly starring,
commenting, or disclosing their strategy work. That is understandable. This
checklist is for private or institutional evaluations that want a reproducible
record without exposing proprietary data, signals, accounts, or trading ideas.

## Safe scope

Share only information that can be made public:

- commit SHA or release tag;
- package version and installation path;
- command shape with private paths removed;
- operating system, Python, PyTorch, CPU/GPU, and CUDA availability;
- data source category, such as synthetic, public API, public CSV, or private
  point-in-time vendor data;
- universe size, date range, frequency, and number of failed tickers;
- aggregate runtime, memory, factor count, IC, turnover, cost, and backtest
  metrics;
- redacted error messages that do not reveal private hostnames, keys, account
  ids, order logs, or holdings.

Do not share:

- API keys, broker credentials, cookies, tokens, or account identifiers;
- raw proprietary market data or vendor-licensed files;
- live positions, holdings, fills, order logs, or execution venues;
- private alpha definitions, factor weights, or production trading rules;
- internal file paths, machine names, customer names, or research notebooks
  that identify a firm or client.

## Minimal private run record

Keep this internally so a result can be reproduced later:

```yaml
project:
  repository: https://github.com/initial-d/ml-quant-trading
  commit:
  package_version:
environment:
  os:
  python:
  pytorch:
  cpu:
  gpu:
  cuda_available:
data:
  source_category: synthetic | public-api | public-file | private-vendor
  market:
  universe_size:
  start:
  end:
  frequency:
  failed_symbols:
run:
  command:
  config:
  factor_count:
  model:
  cost_bps:
  slippage_bps:
outputs:
  runtime:
  peak_memory:
  rank_ic:
  turnover:
  sharpe:
  max_drawdown:
  final_equity:
notes:
  warnings:
  local_changes:
  reproducibility_gaps:
```

## Public redacted report

If the repository helped your research, a redacted public report is useful even
when the data and strategy remain private. The most useful public reports say:

- what entry point was tested, such as `mlquant demo`,
  `scripts/public_data_validation.py`, or the tensor benchmark;
- whether the run succeeded, failed, or required local changes;
- what environment and data category were used;
- what aggregate metrics changed compared with the documented baseline;
- what caveats prevent direct comparison.

Use the
[private evaluation note](https://github.com/initial-d/ml-quant-trading/issues/new?template=private_evaluation_note.yml)
template when you can disclose only a limited summary. Use the
[reproduction report](https://github.com/initial-d/ml-quant-trading/issues/new?template=reproduction_report.yml)
or
[benchmark result](https://github.com/initial-d/ml-quant-trading/issues/new?template=benchmark_result.yml)
template when you can share full commands and generated reports.

## Citation path

For academic work, cite the paper when the method, implementation, benchmark
protocol, factor pipeline, bias correction, portfolio construction, or
validation workflow influenced the experiment:

```bibtex
@article{du2025mlquant,
  title  = {Machine Learning Enhanced Multi-Factor Quantitative Trading:
            A Cross-Sectional Portfolio Optimization Approach with Bias Correction},
  author = {Du, Yimin},
  journal= {arXiv preprint arXiv:2507.07107},
  year   = {2025},
  url    = {https://arxiv.org/abs/2507.07107}
}
```

For engineering notes or internal evaluations, cite the repository commit or
release tag so the software snapshot remains clear.

## Maintainer note

Redacted reports are welcome, including negative results. A report that says
"this failed under a realistic cost assumption" or "this public-data path is
too unstable for our environment" is more useful than an unqualified success
claim.
