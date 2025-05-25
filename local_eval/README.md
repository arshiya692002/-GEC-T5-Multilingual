# Local evaluation

To evaluate your system output locally, please use:

## Reference-based metrics
- ERRANT-based Precision, Recall, F0.5 score: instructions are given [here](errant/README.md)
- GLEU score: [the `gleu` PyPI package](https://pypi.org/project/gleu/); instructions are given [here](https://github.com/shotakoyama/gleu?tab=readme-ov-file#usage).

Note that both ERRANT and GLEU rely on line-aligned reference-hypothesis files containing one essay per line, which the ERRANT scoring program generates automatically.
We therefore suggest to run the ERRANT scoring program first and use the `.tmp` parallel files for GLEU scoring from the `errant/res` and `errant/ref` subfolders.
Alternatively, you can use the functions in [utils_transform_submissions_one_essay_per_line.py](errant/utils_transform_submissions_one_essay_per_line.py) to convert from shared task format to linewise-parallel files.

## Scribendi score
Code and instructions are given [here](https://github.com/robertostling/scribendi_score); during the __development phase__, the official leaderboard will report scores obtained with the __[Llama-3.1-8B model](https://huggingface.co/meta-llama/Llama-3.1-8B)__. Note that a different model will be used during the __test phase__. The latter will not be announced until the end of the competition.
