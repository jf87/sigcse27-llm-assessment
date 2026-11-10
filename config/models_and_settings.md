# Models and settings

All LLM calls went through the Vercel AI SDK (`ai` v5) and the Vercel AI Gateway, with structured (JSON-schema) outputs.

## Models per pipeline step

| Step | Model | Temperature |
|---|---|---|
| OCR of slide PDFs | Mistral OCR 2 (`mistral-ocr-2505`, called as `mistral-ocr-latest`) | — |
| Topic extraction (prompt 01) | `google/gemini-2.5-pro` (weeks 1–9), `openai/gpt-5` (weeks 10–14) | 0.5 |
| Question generation (prompt 02) | `google/gemini-2.5-pro` (weeks 1–9), `openai/gpt-5` (weeks 10–14) | 0.5 |
| Rubric and examples (prompt 03) | `google/gemini-2.5-pro` (weeks 1–9), `openai/gpt-5` (weeks 10–14) | 0.6 |
| Grading (prompt 04) | random, see below | 0 |

## Grading assignment

For each student answer, one configuration was drawn uniformly at random from

    {model} × {with rubric, without rubric} × {with examples, without examples}

The model pool contained `google/gemini-2.5-pro`, `google/gemini-2.5-flash`, `openai/gpt-5`, and `alibaba/qwen-3-32b`. Qwen-3-32B was removed from the pool in mid-December 2025.

## Provider options

| Provider | Options |
|---|---|
| OpenAI (GPT-5) | `reasoningEffort: "medium"`, `strictJsonSchema: true`, `store: false` |
| Google (Gemini) | `structuredOutputs: true`, `thinkingConfig: { thinkingBudget: -1 (dynamic), includeThoughts: true }` |
| Qwen-3-32B (served by Cerebras) | thinking disabled via the `/no-think` suffix in the system prompt |
| Gateway | providers restricted to Cerebras, Google Vertex, OpenAI; `maxRetries: 2` |

## Human review

Generated questions were held in a `pending` state until the instructor approved or rejected them. Only approved questions were released to students.
