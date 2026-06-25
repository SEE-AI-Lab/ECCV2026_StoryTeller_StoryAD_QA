# StoryAD-QA Data

The public QA release is in:

```text
StoryAD-QA/
```

Each CSV has the same schema:

```text
file, raw_response, question, option_A, option_B, option_C, option_D, option_E, correct_answer, rationale
```

`dataset_summary.csv` lists the number of questions in each file.

The same rows are also available as split files:

- `StoryAD-QA-questions/`: question/options CSVs without `correct_answer` or `rationale`
- `StoryAD-QA-answer-key/`: answer-key CSVs with `file`, `row_index`, `correct_answer`, and `rationale`

This folder contains QA annotations and answer keys only. It does not include videos, audio, frames, subtitles, or other movie media.
