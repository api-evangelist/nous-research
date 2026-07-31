---
name: Generate a chat completion with a Nous model
description: Discover an available model and generate an OpenAI-compatible chat completion through the Nous Research inference API, authenticating with a Portal API key or via x402 payment.
api: openapi/nous-research-inference-api-openapi.yml
operations: [listModels, createChatCompletion]
method: generated
generated: '2026-07-20'
---

# Generate a chat completion with a Nous model

Use the Nous Research inference API (Nous Portal) to run an OpenAI-compatible chat
completion. Base URL: `https://inference-api.nousresearch.com/v1`.

## Steps

1. **Pick a model** — call `listModels` (`GET /v1/models`, public, no auth). Choose an
   `id` such as `nousresearch/hermes-4-405b`. The catalog includes per-model
   `pricing`, `context_length`, and `supported_parameters`.
2. **Authenticate** — supply your Nous Portal API key as
   `Authorization: Bearer <key>` (issue keys at https://portal.nousresearch.com).
   Alternatively, use the x402 flow: an un-authenticated request returns HTTP 402
   with an `accepts` envelope describing the exact Solana USDC micropayment.
3. **Create the completion** — call `createChatCompletion`
   (`POST /v1/chat/completions`) with `{ "model": "<id>", "messages": [...] }`.
   Set `"stream": true` to receive a Server-Sent Events stream.
4. **Handle errors** — 401 = missing/invalid key; 402 = payment required (x402
   envelope); 429 = rate limited; 400 = malformed request. See
   `errors/nous-research-problem-types.yml`.

## Notes
- The API is OpenAI-compatible: existing OpenAI SDKs work by overriding `base_url`.
- Chat completions are not idempotent; do not blindly retry a 200-producing call.
