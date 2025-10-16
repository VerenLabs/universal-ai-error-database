# Universal AI Error Database v1

A public dataset cataloguing verified AI system errors across multiple large language models and architectures.
Each entry includes prompt context, a detailed technical root cause, and an engineering level resolution that can be implemented in production systems.

## Why this dataset

* Standardises how AI failures are described, traced and fixed
* Enables reproducible model evaluation across vendors and versions
* Supports benchmarking, red teaming and reliability driven development
* Encourages transparent documentation of limitations and mitigations

## Contents

Data files live under `data/` and are delivered in 25 entry packets for easier review.

* `data/Universal_AI_Error_Database_v1_part001.csv`  25 entries
* `data/Universal_AI_Error_Database_v1_part002.csv`  25 entries
* `data/Universal_AI_Error_Database_v1_part003.csv`  25 entries
* `data/Universal_AI_Error_Database_v1_part004.csv`  25 entries

Schema and validation resources live under `schema/`

* `schema/Universal_AI_Error_Schema_v3.json`

## Schema overview

The CSV files follow the v3 schema. All fields are UTF 8, comma separated.
See the JSON schema for strict validation. Summary below.

| Field | Type | Notes |
|------|------|------|
| ID | string | zero padded incremental identifier, for example 001 |
| Date Logged | string | ISO date, for example 2025 10 16 |
| Category | string | high level class, for example Reasoning, Factual, Policy, Tool Use, Formatting, Context, Bias, Tone, Computation, Attribution |
| Subcategory | string | specific failure type, for example Arithmetic Error, Hallucinated Citation |
| User Prompt Summary | string | short input synopsis that triggered the failure |
| Model Output Summary | string | what the model produced, kept concise |
| Expanded Description | string | two to four sentences that explain the sequence of events and why the output is wrong or incomplete |
| Root Cause (Technical) | string | mechanism of failure, for example retrieval omission, sampling drift, token segmentation, policy misapplication |
| AI Model Type | string | for example GPT 4, Claude 3, Gemini 1.5, LLaMA 3, Mistral Large |
| Architecture Scope | string | for example Transformer LLM, Multimodal Transformer, Retrieval Augmented, Symbolic |
| Model Layer Impact | string | layer or module where failure occurred, for example Retrieval layer, Reasoning layer, Policy filter, Formatter |
| Confidence Score | number | 0.55 to 0.95 representing certainty before failure |
| Confidence Context | string | model self confidence, evaluator rating, cross model uncertainty |
| Severity | string | Low, Medium, High, Critical |
| Source Reference | string | public report or benchmark reference, for example ARC Evals 2024 |
| Resolution / Fix (Expanded) | string | two to three sentence engineering remediation plan |
| Verification Status | string | True or False, whether the issue was validated |
| Replicability | string | High, Medium, Low |
| Detection Method | string | User feedback, Auto QA, Red team probe, Benchmark evaluation, Manual review |
| Validation Status | string | Pending, Validated, Mitigated, Deprecated |
| Re occurrence Likelihood | number | probability between 0 and 1 of recurrence after mitigation |
| Dataset Link | string | optional reference to the related test set or log |

## Quick start

1. Download a CSV under `data/`
2. Validate against the JSON schema, example in Python:

```python
import pandas as pd, json, jsonschema
from jsonschema import validate

df = pd.read_csv("data/Universal_AI_Error_Database_v1_part001.csv")
schema = json.load(open("schema/Universal_AI_Error_Schema_v3.json"))
# field by field validation example, adjust as needed
for col in schema["properties"].keys():
    assert col in df.columns, f"Missing column: {col}"
```

## Usage examples

* Reliability analysis, aggregate by Category and Subcategory to identify top failure modes
* Guardrail design, filter by Policy and Safety to build refusal and guidance templates
* Tool routing rules, use Root Cause and Resolution fields to implement deterministic routes
* Benchmark creation, convert User Prompt Summary and Model Output Summary into unit tests

## Versioning

This repository follows semantic versioning for the dataset.
Initial release is v1.0.0 with four CSV packets totalling 100 entries.

## How to cite

> Universal AI Error Database v1, 2025. Public dataset of verified AI system errors across model families.
> URL, your repository URL once published.

## Licence

MIT for code, CC BY 4.0 recommended for data.
If you prefer a single licence, MIT is acceptable for this dataset release.

## Contributing

Issues and pull requests are welcome. For new entries, please include
a minimal reproduction, a public source reference and a proposed fix.
