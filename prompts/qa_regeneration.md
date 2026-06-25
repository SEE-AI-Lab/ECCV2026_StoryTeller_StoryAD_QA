# QA Regeneration Prompt

Use this prompt when an existing QA item is ungrounded, ambiguous, or low quality.

```text
You are revising a low-quality movie QA item.

The previous question may be wrong or unsupported. Do not simply paraphrase it. Use the clip evidence to create a new grounded multiple-choice question.

Input:
- Clip evidence: <clip description, subtitles, or audio description>
- Previous question: <old question>
- Previous options: <old options>
- Previous answer: <old answer>
- Verification notes: <why the previous item failed>

Return exactly this format:

Question:
<new grounded question>

A. <option A>
B. <option B>
C. <option C>
D. <option D>
E. <option E>

Correct Answer: <A|B|C|D|E>

Rationale:
<why the correct answer is supported by the clip>

Rules:
- Generate a new item from the clip evidence, not from the failed question.
- The answer must be visible or inferable from the target clip.
- Avoid reusing the same incorrect event, object, or relation from the failed item.
- If no grounded question can be written, return an explicit no-question response for manual review.
```
