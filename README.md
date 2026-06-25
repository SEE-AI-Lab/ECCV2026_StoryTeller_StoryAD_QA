# StoryAD-QA

Official release scaffold for the ECCV 2026 paper:

**StoryTeller: Training-Free Long-Form Audio Description with Narrative Memory**

StoryAD-QA is the question-answering benchmark released with StoryTeller. It is designed to evaluate whether generated audio descriptions preserve story understanding, not only whether they overlap lexically with reference descriptions.

## Why We Release StoryAD-QA

Audio description (AD) systems are often evaluated with captioning metrics such as CIDEr, SPICE, BLEU, and ROUGE-L. These metrics are useful, but they mostly compare local word overlap. They do not directly test whether a generated description preserves the story: who the characters are, what they did earlier, why a current scene matters, and how events connect across time.

StoryTeller addresses this problem with a training-free framework for long-form movie AD. It builds explicit narrative memory, tracks identity across scenes, and retrieves story-relevant context before generating descriptions. StoryAD-QA supports the paper's evaluation goal: measure whether AD outputs contain enough narrative information to answer grounded questions about the movie.

The benchmark is released so that other researchers can:

- evaluate long-form AD systems with story-level QA rather than only lexical metrics
- compare methods on grounded multiple-choice questions over fixed temporal windows
- audit prompts used for QA generation, regeneration, and verification
- reproduce the paper's QA-style evaluation protocol

## What Is Included

```text
data/
  StoryAD-QA/                    # public QA CSVs with answer keys
  StoryAD-QA-questions/          # questions/options only
  StoryAD-QA-answer-key/         # answer keys and rationales
  dataset_summary.csv            # per-file question counts
evaluation/
  evaluate_storyad_qa.py         # multiple-choice accuracy evaluator
  requirements.txt
prompts/
  qa_generation.md
  qa_regeneration.md
  qa_verification.md
docs/
  index.html                     # GitHub Pages project website
  assets/style.css
```

This repository releases QA annotations, answers, prompts, and evaluation code. It does **not** release videos, movie audio, frames, subtitles, or copyrighted media.

## Dataset

The main public CSVs are in:

```text
data/StoryAD-QA/
```

Each row has:

```text
file, raw_response, question, option_A, option_B, option_C, option_D, option_E, correct_answer, rationale
```

- `file`: clip identifier/path used for alignment
- `question`: multiple-choice question
- `option_A` ... `option_E`: answer choices
- `correct_answer`: gold label, one of `A` through `E`
- `rationale`: explanation for the answer
- `raw_response`: original formatted model response used to create the row

Current public release size: **2,572 QA pairs**.

For convenience, the same release is also split into:

- `data/StoryAD-QA-questions/`: `file`, `raw_response`, question, and options only
- `data/StoryAD-QA-answer-key/`: `file`, `row_index`, `correct_answer`, and `rationale`

The combined files are the authoritative release for reproducibility. The split files are useful if you want to distribute questions separately from answers for evaluation or annotation.

| File | Questions |
|---|---:|
| `movie_qa_v5_30s_gemini-3-flash-preview.csv` | 858 |
| `movie_qa_v5_60s_gemini-3-flash-preview.csv` | 430 |
| `movie_qa_v5_120s_gemini-3-flash-preview.csv` | 212 |
| `movie_qa_v5_240s_gemini-3-flash-preview.csv` | 109 |
| `movie_qa_v9_60s_gemini-3-flash-preview.csv` | 449 |
| `movie_qa_v9_90s_gemini-3-flash-preview.csv` | 294 |
| `movie_qa_v9_120s_gemini-3-flash-preview.csv` | 220 |

## Evaluation

Prepare a prediction CSV:

```text
file,prediction
```

where `prediction` is one of `A`, `B`, `C`, `D`, or `E`.

Run:

```bash
pip install -r evaluation/requirements.txt
python evaluation/evaluate_storyad_qa.py \
  --gold data/StoryAD-QA/movie_qa_v5_30s_gemini-3-flash-preview.csv \
  --predictions path/to/predictions.csv
```

The evaluator reports total examples, evaluated examples, missing predictions, invalid predictions, accuracy, and per-answer accuracy.

## Prompts

The `prompts/` folder contains the prompt templates used for:

- QA generation
- QA regeneration for failed/low-quality items
- QA verification against clip evidence

We include prompts because StoryAD-QA is partly a methodological release: the paper's evaluation depends on how questions are generated, repaired, and checked.

## GitHub Pages

The `docs/` folder contains a project website mockup suitable for GitHub Pages.

Recommended setup:

1. Push this folder as the root of the repository.
2. In GitHub settings, enable Pages from the `main` branch and `/docs`.
3. Use the Pages URL in the paper.

## Media And Licensing

This release intentionally excludes videos and any derived media. The `file` field is an identifier for alignment with the evaluation clips used in the paper. Users are responsible for ensuring lawful access to any underlying video content.

The final public license should be approved by the authors before release. A placeholder `LICENSE` file is included.

## Citation

Please cite the ECCV 2026 StoryTeller paper when using StoryAD-QA. Update `CITATION.cff` after final paper metadata is available.
