# agents

Reusable agent prompts and review procedures.

The goal of this repository is to preserve hard-won checks and operating rules so recurring tasks do not depend on an agent remembering prior failures or inheriting the reasoning of the agent that produced the work.

## Agents

### `delivery_output_auditor/`

A blind, output-only reviewer for client data deliveries. It deliberately avoids implementation context, producer explanations, previous-release reasoning, receipts, and manifests so it can independently inspect what a client would actually receive.

It checks package/parse integrity, semantic column alignment, missingness, cross-tabs, confidence coverage, value plausibility, delimiter/quoting/field-shift problems, duplicates, reading order, grouping, anomalous rows, and other output-only surprises.

Known historical failure modes are kept as mandatory regression checks inside the agent itself. Current examples include:

- duplicate client-facing records, including duplicates that are not byte-identical because metadata/confidence differs;
- records emitted in the wrong reading order;
- syntactically valid files whose values are shifted into the wrong columns;
- unexpectedly blank or nearly blank fields;
- confidence/value mismatches and suspicious confidence fallbacks.

See [`delivery_output_auditor/AGENT.md`](delivery_output_auditor/AGENT.md).

## Convention

Each agent should live in its own clearly named folder. Durable lessons from failures should be added to the relevant agent as explicit regression checks, not left only in issue history or project-specific notes.