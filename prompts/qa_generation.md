# QA Generation Prompt

Use this prompt template to generate a five-option multiple-choice question from an audio-described movie clip or clip description.

```text
You are creating a video question-answering benchmark for story-level understanding.

Given the target clip evidence, write one multiple-choice question that can be answered from the clip. The question should require understanding actions, events, character behavior, or narrative context. Avoid questions that can be answered from a single static object unless that object is narratively important.

Return exactly this format:

Question:
<one question grounded in the clip>

A. <option A>
B. <option B>
C. <option C>
D. <option D>
E. <option E>

Correct Answer: <A|B|C|D|E>

Rationale:
<brief explanation grounded in visible/audio-described evidence>

Constraints:
- The correct answer must be directly supported by the clip.
- Distractors should be plausible but contradicted or unsupported.
- Do not ask about information outside the clip.
- Do not include "all of the above" or "none of the above".
- Keep options similar in length and specificity.
```

