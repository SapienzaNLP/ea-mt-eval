# Entity-Aware Machine Translation Evaluation

This repository contains tools and scripts for evaluating machine translation quality with a focus on entity translation accuracy. It includes implementations of both COMET and M-ETA (Manual Entity Translation Accuracy) evaluation metrics.

## Quick Links
- [Notebook: Evaluation with M-ETA](notebooks/entity_eval.ipynb)
- [Notebook: Evaluation with COMET](notebooks/comet_eval.ipynb)
- [Notebook: Translation with OpenAI API](notebooks/openai_api.ipynb)

## Table of Contents
- [The EA-MT Shared Task](#the-ea-mt-shared-task)
  - [Task Description](#task-description)
  - [Why is this task important?](#why-is-this-task-important)
- [Overview of the Codebase](#overview-of-the-codebase)
- [Supported Target Languages](#supported-target-languages)
- [Evaluation Metrics](#evaluation-metrics)
  - [COMET](#comet)
  - [M-ETA](#m-eta)
- [Installation](#installation)
- [Data Format](#data-format)
  - [JSONL Format](#jsonl-format)
- [Usage](#usage)
    - [Translation](#translation)
    - [Evaluation](#evaluation)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## The EA-MT Shared Task
The [EA-MT (Entity-Aware Machine Translation) shared task](https://sapienzanlp.github.io/ea-mt/) is part of the SemEval-2025 workshop. The task is to evaluate machine translation systems with a focus on entity translation accuracy.
- [Task Description](#task-description)
- [Why is this task important?](#why-is-this-task-important)

### Task Description
We invite participants to develop machine translation systems that can accurately translate text that includes potentially challenging named entities in the source language. The task is to translate a given input sentence from the source language (English) to the target language, where the input sentence contains named entities that may be challenging for machine translation systems to handle. The named entities may be entities that are rare, ambiguous, or unknown to the machine translation system. The task is to develop machine translation systems that can accurately translate such named entities in the input sentence to the target language.

### Why is this task important?
We believe that the ability to accurately translate named entities is crucial for machine translation systems to be effective in real-world scenarios. Named entities are entities that are referred to by proper names, such as people, organizations, locations, dates, and more. Named entities are often challenging even for human translators, as sometimes there are cultural or domain-specific references that are not easily translatable. This happens more often for some entity types or categories, such as movies, books, TV series, products, and more.

## Overview of the Codebase

This codebase provides functionality for:
- Evaluation using M-ETA metric for entity translation accuracy
- Evaluation using COMET metric for overall translation quality
- Translation using OpenAI's API
- Support for multiple language pairs with English as source

### Supported Target Languages
- Arabic (ar_AE)
- Chinese Traditional (zh_TW) 
- French (fr_FR)
- German (de_DE)
- Italian (it_IT)
- Japanese (ja_JP)
- Korean (ko_KR)
- Spanish (es_ES)
- Thai (th_TH)
- Turkish (tr_TR)

## Evaluation Metrics
For this edition of the shared task, we will be using the harmonic mean of two evaluation metrics:
- [COMET](https://github.com/Unbabel/COMET)
- M-ETA (Manual Entity Translation Accuracy)

Therefore, the final evaluation score will be the harmonic mean of the two scores, i.e.:
```
Final Score = 2 * (COMET * M-ETA) / (COMET + M-ETA)
```

### COMET
COMET is a metric for evaluating the quality of machine translation systems. It is based on the idea of comparing the output of a machine translation system to the output of a human translation system. COMET uses a pre-trained model to generate a score for each translation, which is then used to evaluate the quality of the translation.
- You can find more information about COMET [here](https://github.com/Unbabel/COMET).

### M-ETA
M-ETA (Manual Entity Translation Accuracy) is a metric for evaluating the accuracy of entity translation in machine translation systems. At a high level, given a set of gold entity translations and a set of predicted entity translations, M-ETA computes the proportion of correctly translated entities in the predicted entity translations.

```
M-ETA = (Number of correctly translated entities) / (Number of entities in the reference translations)
```

In general, we say that a predicted entity translation is correct if it is an exact match with at least one of the reference entity translations, which have been manually annotated by human evaluators.


## Installation
We recommend using `conda` to manage the environment and dependencies. If you don't have `conda` installed, you can download it [here](https://docs.conda.io/en/latest/miniconda.html).

1. Create a virtual environment:
```bash
# Create a new environment
conda create -n ea-mt-eval python=3.10

# Activate the environment
conda activate ea-mt-eval
```

2. Install requirements:
```bash
pip install -r requirements.txt
```

## Data Format

The data should be organized in the following structure:
```
data/
├── predictions/
│   └── <model_name>/
│       └── validation/
│           ├── ar_AE.jsonl
│           ├── de_DE.jsonl
│           └── ...
└── references/
    ├── sample/
    ├── test/
    └── validation/
```

### JSONL Format
Each line contains a JSON object with:
- `id`: Unique identifier
- `source_language`: Source language code
- `target_language`: Target language code
- `text`: Source text
- `prediction`: Translated text (for predictions)
- `targets`: List of reference translations (for references)

## Usage

### Translation
Use the OpenAI API for translation by running the notebook:
```bash
jupyter notebook notebooks/openai_api.ipynb
```

Requires setting the `OPENAI_API_KEY` environment variable.

### Evaluation
Two evaluation notebooks are provided:

1. COMET Evaluation (Overall Quality):
```bash
jupyter notebook notebooks/comet_eval.ipynb
```

2. M-ETA Evaluation (Entity Accuracy):
```bash
jupyter notebook notebooks/entity_eval.ipynb
```

## License
This project is licensed under the Creative Commons Attribution-ShareAlike 4.0 International License - see the LICENSE.txt file for details.

## Acknowledgements
Simone gratefully acknowledges the support of Future AI Research ([PNRR MUR project PE0000013-FAIR](https://fondazione-fair.it/en/)), which fully funds his fellowship at Sapienza University of Rome since October 2023.