# Evaluation Setup

This file is outside the editable surface. It defines how results are judged. Agents cannot modify the evaluator or the scoring logic — the evaluation is the trust boundary.

Consider defining more than one evaluation criterion. Optimizing for a single number makes it easy to overfit and silently break other things. A secondary metric or sanity check helps keep the process honest.

eval_cores: 1
eval_memory_gb: 1.0
prereq_command: npm install

## Setup

Install dependencies:

```bash
npm install
```

No build step is required for this JavaScript library. The `prereq_command` is set to `npm install` to ensure dependencies are available.

After setup, verify correctness with:
```bash
npm test
```

All tests must pass for any changes to be considered valid.

## Run command

```bash
node benchmark.js
```

## Output format

The benchmark must print `METRIC=<number>` to stdout.

Example output:
```
METRIC=48784.63
```

## Metric parsing

The CLI looks for `METRIC=<number>` in the output. The metric represents operations per second (ops/sec).

## Ground truth

The benchmark measures throughput of content negotiation operations. Each iteration creates a Negotiator instance and performs 8 negotiation operations (mediaType, mediaTypes, language, languages, charset, charsets, encoding, encodings) with realistic HTTP headers and available options.

The benchmark runs 100,000 iterations across 3 different request patterns (representing common scenarios: HTML browser, JSON API client, and image requests) and reports the total operations per second.

Baseline performance: ~48,000-50,000 ops/sec on a single core (varies by hardware).

Higher values are better. The metric_direction in PROGRAM.md is set to "higher_is_better".
