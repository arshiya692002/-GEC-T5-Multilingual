# MultiGEC-2025 training data and scripts
Training data and scripts for the MultiGEC 2025 shared task. 
Access is restricted to organizers, data providers and shared task participants, and subject to the following terms of use ([link to form](https://forms.gle/VLJ18WbwsxitEBYi7)):

- access is personal. New users need to apply for access
- there are personal data in the resources. You **cannot** use proprietary models, that consume data, for experiments with the MultiGEC datasets
- you must take precautions not to re-identify the writers or inflict any harms on those who you may incidentally recognize from the data
- you are not permitted to share the data. You can quote parts of an essay (or in exceptional cases full essays) in your research papers or thesis. You are not allowed to publish (parts of) essays at open websites or in social media. This restriction does not apply to derivative products of the resource
- no commercial use is allowed
- attribution, i.e. acknowledgement of corpus authorship, is required. Relevant publications are linked to in the metadata files of each subcorpora.

Usage of the data outside of the shared task is subject to conditions in the licenses fo the individual subcorpora. These are specified in the metadata files. 

For more information about the shared task, visit [the official website](https://spraakbanken.gu.se/en/compsla/multigec-2025).
If you have any further questions for the organizers and/or want to discuss the task with other participants, you are also welcome to join the [MultiGEC-2025 Google group](https://groups.google.com/g/multigec-2025).

## Data
The MultiGEC-2025 dataset consists of 17 subcorpora, covering 12 languages: Czech, English[^1], Estonian, German, Greek, Icelandic, Italian, Latvian, Russian[^1], Slovene, Swedish and Ukrainian.

Each subcorpus contains a train and a development set, each of which consists of 2+ essay-aligned files, one containing original learner essays and one or more containing reference (i.e. corrected/normalized) texts.

### Naming conventions
Data files are named according to the following convention:

```
language/CorpusName/langcode-corpus-orig|refn-train|dev|test.md
```

where

- `language` is the name of the language, lowercased
- `CorpusName` is the name of the subcorpus
- `langcode` is the [two-letter ISO 639 code for the language](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes)
- `corpus` is the name of the subcorpus, lowercased
- `orig` indicates that the file contains original essays, whereas `ref1`, `ref2`, `refn` indicate the `n`-th reference file
- `test`, `dev` and `train` indicate the corresponding dataset splits

> __Example__: `czech/NatWebInf/cs-natwebinf-ref2-dev.md` is the second reference file for the development split of the NatWebInf Czech subcorpus.  

### File format
Internally, each file follows this simple markdown-based format:

```
### essay_id = 1
Full ext of the first essay/reference.

Whitespace, including newline characters, is preserved, but for the sake of readability TWO consecutive newline characters spearate subsequent essays.

### essay_id = 2
Full text of the second essay/reference.

...
```

`orig` and `refn` files are aligned at the essay level in the sense that reference corrections with `essay_id = Y` are relative to the essay with `essay_id = Y` in the corresponding `orig` file. 
Note, however, that __not all__ `refn` files contain corrections for __all__ essays in their `orig` counterpart (that is, some subcorpora only have a second reference for some of the essays).

## Metadata
Each subcorpus folder contains a `metadata.yaml` file that summarizes basic information in a [machine-readable format](metadata.yaml).
For some of the subcorpora, a longer description is provided in a README file. 

## Evaluation
Evaluation will be based on the following cross-lingually applicable __automatic metrics__:

- reference-based:
  - GLEU score
  - ERRANT-based Precision, Recall, F0.5 score
- reference-free: 
  - Scribendi score.

### Development phase
During the development phase, there will be two leaderboards:

- the official leaderboard with all three metrics will be available on [the shared task website](https://spraakbanken.gu.se/en/compsla/multigec-2025). It will be updated twice throughout the development phase, on November 6 and November 12
- there will also be a live leaderboard [on CodaLab](https://codalab.lisn.upsaclay.fr/competitions/20500). However, due to limitations of the platform, this will only rank  submissions based on the GLEU score.

__To evaluate your system output locally, follow the instructions given [here](local_eval/README.md)__.

### Test phase
The submissions for the test phase will be done through CodaLab; more details to come.

## Other scripts
- system submissions should be in the same format as the data files provided in this repository. This can be checked with the [`validate.py`](validate.py) script (recommended usage: `python validate.py PATH-TO-OUTFILE EXPECTED-NUMBER-OF-ESSAYS`)
- a one-shot Llama-based multilingual baseline is provided in [`baseline.py`](baseline.py) 
- the functions contained in [`multigec_2025_utils.py`](multigec_2025_utils.py) were written mostly for internal usage among shared task organizers. However, some of them can be useful to participants for parsing shared task data to Python dictionaries and vice versa

[^1]: Note that use of the Russian and English datasets requires signing an additional Terms Of Use document and an external download; see instructions in their respective folders.

