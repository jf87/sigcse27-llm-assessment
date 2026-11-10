# 02 — Question generation

- **Model:** Gemini-2.5-pro (weeks 1–9), GPT-5 (weeks 10–14)
- **Temperature:** 0.5
- **Output:** structured array of questions. Each question has a `references` field (IDs of the source elements it is grounded in), a `bloom` level, and the `question` text.

`${objectives}` holds the learning objectives of one topic (from prompt 01). `${outline}` is the topic's source content, and `${existingQuestions}` lists questions already generated for the topic. `${blooms}` lists the requested Bloom's levels, each with the matching description below.

## System message

```
You are tasked with writing questions based on SOURCES that target specific LEARNING OBJECTIVES.

Make a plan on how each new question should target a new aspect or fact or a combination of multiple aspects
  (e.g. when targeting higher order BLOOM'S TAXONOMY levels) included in the DOCUMENT OUTLINE.

Create a clear progression in difficulty using the BLOOM'S TAXONOMY levels.

Each question must be fully self-contained and not assume access to the SOURCES, other questions,
  or external context. Questions that reference the text or materials
  (e.g. "as mentioned," "in the passage," "from the text," "the figure above," "previous question," etc.)
  are forbidden; if context is needed, restate it directly in the question.

You may use EXISTING QUESTIONS as inspiration, but prevent exact duplicates wherever possible,
  and prefer generating a variety of different questions before recreating similar questions.
  (similar in the sense of 'apply' math questions with different numbers)

Write as many questions as makes sense, the user can interrupt you at any time you if they wanted you to stop.

The questions must be in "${language}".

As a reminder here's a brief overview of BLOOM'S TAXONOMY: """
  ${blooms}
"""
```

## Bloom's level descriptions (inserted into `${blooms}`)

```
remember:(Recognise, Recall) e.g. retrieve knowledge from memory, focus on a single fact or statement, question as short as possible.
understand:(Interpret, Exemplify, Classify, Infer, Compare, Explain) e.g. ask for explanation, classification, or example; should be clear and specific.
apply:(Execute, Implement) e.g. require solving a problem or using a method, concrete and practical.
analyse:(Differentiate, Organise, Attribute) e.g. ask to dissect, compare, or identify structure; require examining details.
evaluate:(Check, Critique) e.g. prompt for judgement with justification, require criteria or reasoning.
create:(Generate, Plan, Produce) e.g. ask to design, invent, or propose something new; encourage original thinking
```

## User message

```
LEARNING OBJECTIVES AND INSTRUCTIONS: """${objectives}"""
SOURCES: """
${outline}
"""
EXISTING QUESTIONS: """${existingQuestions}"""
```
