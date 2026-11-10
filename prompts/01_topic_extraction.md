# 01 — Topic and learning-objective extraction

- **Model:** Gemini-2.5-pro (weeks 1–9), GPT-5 (weeks 10–14)
- **Temperature:** 0.5
- **Output:** structured array of topics

`${language}` is the course language (German). `${outline}` is the OCR'd slide content, with an ID for each element. `${existingTopics}` lists previously created topics, and `${instructions}` holds optional instructor instructions.

## System message

```
You are tasked with creating a structured lesson plan from the provided SOURCES.
Follow these rules unless overridden by USER INSTRUCTION:
- Group related content into topics and subtopics.
- Assign every outline element id to at least one topic. Do not overlap ids between topics.
- Skip only elements that contain no educational material (e.g. references, copyright notices).
- Merge very small subtopics if needed, but avoid creating topics that cover too much at once.
- Update EXISTING TOPICS if applicable by reusing their id.
- Prefer bullet point lists for learning objectives.
- Generate at least one topic, but as many as makes sense.
- Write all titles and objectives in "${language}".
```

## User message

```
EXISTING TOPICS: """${existingTopics}"""
SOURCES: """
${outline}
"""
USER INSTRUCTION: """${instructions}"""
```

## Output schema (per topic)

| Field | Description |
|---|---|
| `id` | The ID of the topic, use any unique identifier to ensure uniqueness |
| `parent_id` | The ID of the parent topic, or null if this is a top-level topic |
| `references` | IDs of the source outline elements covered by this topic |
| `title` | The title of this topic |
| `objectives` | A study plan including objectives that explain the ideal approach of teaching this subtopic in GFM markdown with LaTeX math |
