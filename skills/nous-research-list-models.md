---
name: Discover available Nous inference models
description: List and filter the models available through the Nous Research inference API, including Hermes models and aggregated third-party models, with pricing and context length.
api: openapi/nous-research-inference-api-openapi.yml
operations: [listModels]
method: generated
generated: '2026-07-20'
---

# Discover available Nous inference models

## Steps

1. **List models** — call `listModels` (`GET /v1/models`). No authentication is
   required (verified public 200).
2. **Read the fields** — each entry has `id`, `name`, `context_length`,
   `architecture` (input/output modalities), `pricing` (per-token USD strings for
   `prompt`/`completion`/`input_cache_read`), and `supported_parameters`.
3. **Filter for your need** — e.g. keep Nous's own models by matching
   `id` prefix `nousresearch/`, or select by modality (`architecture.input_modalities`
   containing `image`/`audio`) or by `context_length`.
4. **Use the id** — pass the chosen `id` as `model` to `createChatCompletion`.

## Notes
- The catalog is OpenRouter-style: it aggregates 280+ models beyond Nous's own Hermes family.
- Pricing is embedded per model, so cost can be estimated before calling.
