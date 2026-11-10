# 03 — Rubric and example answers

- **Model:** Gemini-2.5-pro (weeks 1–9), GPT-5 (weeks 10–14)
- **Temperature:** 0.6
- **Output:** a rubric, plus a list of example answers, each with an expected accuracy (0–1), the answer text, and optional teacher feedback

The rubric and example answers are what the grader receives when the "rubric" and/or "examples" variant is selected (see prompt 04).

## System message

```
You are tasked with autocompleting a question's rubric and grading answers.
You received a list of SOURCES that are the factual basis your output should depend on,
  an EXISTING QUESTION that may or may not already some of the output you should generate,
  and a list of LEARNING OBJECTIVES AND INSTRUCTIONS that you should use as a guide on what the user expects.

The rubric should explain the individual criteria and rules that makes an answer correct, partially correct or incorrect,
  preferably as a bullet point list without concrete examples (examples should be included in the example answers array).
For lower bloom's taxonomy levels: Keep the rubric as short as possible or leave completely empty if the answer
  can be graded appropriately with the example answers alone.
For higher bloom's taxonomy levels: Focus more on the rubric, maybe it doesn't even make sense to include
  example answers if the question is very open ended.
If you do include example answers, make sure you think about what kinds of edge cases a group of students
  could collectively come up with and only include the most important examples that test the limits of the rubric.
Keep the example answer realistic to what a real student would write,
  (usually short and to the point or even single word if applicable by the bloom's taxonomy level).
Usually around 2-4 good examples should be enough unless specified otherwise.
You may or may not include a short feedback for each individual example answer that will be used as a template
  should the grader encounter a similar answer by a real student.
This feedback should be concise, constructive and relevant,
  and should not include filler words like "correct", "partially correct" or "excellent". ("yes", and "no" are allowed)
Some example answers may not require feedback at all (e.g. completely correct answers).
The language of the rubric, answer and feedback must be "${language}".
If the question or entire topic is about translating from one language to another,
  the example answers may deviate from "${language}".
```

## User message

```
SOURCES: """${sources}"""
LEARNING OBJECTIVES AND INSTRUCTIONS: """${topicObjectives}"""
EXISTING QUESTION: {
  "bloom": "${bloom}",
  "question": "${question}",
  "rubric": "${existingRubric, if any}",
  "answers": [ ${existingExampleAnswers, if any} ]
}
```

## Output schema

| Field | Description |
|---|---|
| `rubric` | A rubric explaining the bounds of what makes an answer correct or incorrect |
| `answers[].accuracy` | The expected accuracy of the answer, 0–1 |
| `answers[].content` | The actual answer (GFM markdown with LaTeX math) |
| `answers[].feedback` | The feedback a teacher would give to this student answer (GFM markdown with LaTeX math) |
