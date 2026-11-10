# Closing the Feedback Loop — Supplementary Material

Supplementary material for:

> Jonathan Fürst, Gerome Laurin Meyer, Yi Zhang, and Philip Breuer. 2027.
> *Closing the Feedback Loop: Lessons from a 14-Week Deployment of LLM-Driven Assessment.*
> In Proceedings of the 58th ACM Technical Symposium on Computer Science Education V.1 (SIGCSE TS 2027).

The material documents the system deployed in a 14-week undergraduate database course (autumn semester 2025/26).

## Contents

| Path | What it contains |
|---|---|
| `prompts/01_topic_extraction.md` | Prompt that turns the OCR'd course slides into topics and learning objectives |
| `prompts/02_question_generation.md` | Prompt that generates questions for given Bloom's taxonomy levels |
| `prompts/03_rubric_and_examples.md` | Prompt that generates the rubric and example graded answers for each question |
| `prompts/04_grading.md` | Grading prompt used for all student answers (`grading-2`) |
| `config/models_and_settings.md` | Models, sampling parameters, provider options, and grading assignment |
| `survey/survey_instrument.md` | End-of-semester student survey (German original with English translation) |

Prompts are reproduced verbatim from the deployed application. Template variables are shown as `${...}`.

## Pipeline overview

1. **OCR.** Mistral OCR converts the course slide PDFs into Markdown ("sources").
2. **Topic extraction** (`01`). An LLM groups the source elements into topics, each with learning objectives.
3. **Question generation** (`02`). For each topic, an LLM writes questions at the requested Bloom's levels. Each question references the source elements it is grounded in.
4. **Rubric and examples** (`03`). For each question, an LLM writes a rubric and example graded answers.
5. **Human review.** The instructor approved or rejected every question before release.
6. **Grading** (`04`). Every student answer is graded by an LLM. The model and prompt variant are sampled at random (see `config/`).

## Not included

Student answers, gradings, expert annotations, and generated questions are not part of this release.

## Contact

Jonathan Fürst — jonathan.fuerst@zhaw.ch
