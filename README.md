# YallaMorph

**YallaMorph: A Benchmark for Evaluating Arabic Morphological Generation in Large Language Models**

YallaMorph is a large-scale benchmark for evaluating the ability of Large Language Models (LLMs) to perform **controlled Arabic morphological generation**.

Given an Arabic **lemma**, **part-of-speech (POS)**, **gloss**, and a set of target **morphosyntactic features**, the task is to generate the corresponding fully diacritized Arabic surface form or forms. The benchmark also includes morphologically invalid feature configurations for which no valid form exists.

YallaMorph covers:

* Verbs
* Nouns
* Adjectives
* Baseword morphology
* Cliticized forms
* Morphologically invalid configurations

The benchmark contains **663,804 evaluation instances** across **4,795 sampled lemmas**.

## Repository Structure

```text
YallaMorph/
│
├── sample_data/
│   └── ...
│
├── output_data/
│   └── ...
│
├── prompts/
│   ├── english/
│   │   ├── zero_shot/
│   │   └── few_shot/
│   │
│   └── arabic/
│       ├── zero_shot/
│       └── few_shot/
│
└── README.md
```

### `sample_data/`

Contains sample instances from the YallaMorph benchmark.

Each benchmark instance specifies a lexical item and the morphological features that the model must realize.

Depending on the POS, these features include:

**Verbs**

* Aspect
* Person
* Gender
* Number
* Voice
* Mood

**Nouns and Adjectives**

* Gender
* Number
* Case
* State

Clitic-aware instances additionally contain positional proclitic and enclitic features.

### `output_data/`

Contains model predictions produced during the YallaMorph experiments.

The experiments evaluate multilingual and Arabic-focused LLMs under different prompting configurations.

Model outputs are generated using a fixed JSON output format and subsequently processed for evaluation.

### `prompts/`

Contains the prompts used to evaluate the models.

Prompts are available in:

* **English**
* **Arabic**

and under two prompting settings:

* **Zero-shot**
* **Few-shot (10-shot)**

The prompts are POS-specific, with separate configurations for:

* Verbs
* Nouns
* Adjectives
* Clitic-aware generation

The few-shot prompts include **10 in-context examples** selected from data that is disjoint from the benchmark evaluation instances.

## Task

Given an input such as:

```text
Lemma: ...
POS: ...
Gloss: ...

Morphological Features:
...
```

the model must generate the Arabic form corresponding to the complete morphological specification.

A specification may have:

1. A single valid Arabic form
2. Multiple valid Arabic forms
3. No morphologically valid realization

The expected output format is:

```json
{
  "arabic_forms": ["form1", "form2"],
  "status": "OK"
}
```

For morphologically impossible configurations:

```json
{
  "arabic_forms": null,
  "status": "IMPOSSIBLE"
}
```

## Benchmark Design

YallaMorph is constructed from the lemma inventory and morphological analyses of **CamelMorph MSA**, accessed through **CAMeL Tools**.

The benchmark sampling strategy considers several linguistic and distributional dimensions, including:

* Lemma frequency
* Root class
* Paradigm completeness
* Stem complexity

The benchmark contains two complementary evaluation subsets:

**Baseword**
: Evaluates core Arabic inflectional morphology.

**Cliticization**
: Evaluates the interaction between inflected forms and Arabic proclitics/enclitics.

## Benchmark Statistics

| POS Group                  | Baseword Instances | Cliticized Instances |
| -------------------------- | -----------------: | -------------------: |
| Active Perfective Verbs    |              9,234 |               45,738 |
| Passive Perfective Verbs   |              8,964 |                8,820 |
| Command Verbs              |              7,794 |                6,480 |
| Active Imperfective Verbs  |             39,150 |              181,800 |
| Passive Imperfective Verbs |             39,150 |               37,800 |
| Nouns                      |            101,898 |               67,950 |
| Adjectives                 |             32,076 |               76,950 |
| **Total**                  |        **238,266** |          **425,538** |

**Total benchmark size: 663,804 instances.**

## Paper

**YallaMorph: A Benchmark for Evaluating Arabic Morphological Generation in Large Language Models**

Mahmoud Reda, Salam Khalifa, Reham Marzouk, and Nizar Habash

Computational Approaches to Modeling Language (**CAMeL Lab**), New York University Abu Dhabi.

If you use YallaMorph in your research, please cite:

```bibtex
@inproceedings{reda2026yallamorph,
  title     = {YallaMorph: A Benchmark for Evaluating Arabic Morphological Generation in Large Language Models},
  author    = {Reda, Mahmoud and Khalifa, Salam and Marzouk, Reham and Habash, Nizar},
  year      = {2026}
}
```

> The final ACL/EMNLP citation information will be updated once the proceedings citation is available.

## Acknowledgments

This work was conducted at **CAMeL Lab, New York University Abu Dhabi**.

We gratefully acknowledge the support and contributions of the CAMeL Lab community and collaborators involved in the development of YallaMorph.

## License

## License

YallaMorph is released under the following licenses:

* **Benchmark data, sample data, prompts, documentation, and other research artifacts:** Creative Commons Attribution 4.0 International (**CC BY 4.0**).
* **Source code and scripts:** **MIT License**.

YallaMorph is constructed using morphological resources from CamelMorph MSA. Users should also comply with the licenses and attribution requirements of the underlying resources.

Model-generated outputs included in this repository were produced using their respective language models and may additionally be subject to the terms and conditions of the corresponding model providers.
