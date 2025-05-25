# MultiGEC-2025 local ERRANT scoring

This package is intended for local scoring of hypothesis files for the MultiGEC-2025 shared task, using a modified version of ERRANT to obtain precision, recall and F0.5 scores.

Please follow the steps below, and report any issues to us. You should only need to run the setup steps 1..5 once, and then you can evaluate your dev predictions repeatedly (steps 6 and 7).

We tested this on Unix-like OS (Ubuntu 20.04, Manjaro 24.1.1 Xahea and MacOS 12.3.1) using Python 3.12.5. If you're running Windows the best thing for now is to contact us and we'll run ERRANT for you.

1. Clone this repository and move to this directory
2. Create a 'res/' directory (`mkdir res`) and place your hypothesis files inside it; their names should be '{langcode}-{corpusname}-hypo{n}-dev.md' where {langcode} is e.g. 'cs', 'de', 'et', {corpusname} can be found in the filenames used in the data repository, {n} is probably 1 during development, and everything should be **lowercase**
3. Set up a conda environment (`conda create -n multigec python=3.12.5; conda activate multigec`) or virtualenv (`python3 -m venv multigec; source multigec/bin/activate; pip install -U pip setuptools wheel`)
4. Make a directory for your scores, e.g. `mkdir out`
5. Run the following commands:
    ```
    pip install regex

    git clone https://github.com/cainesap/errant
    cd errant
    pip install -e .
    cd ../

    pip install spacy-udpipe

    python download_spacy_udpipe_models.py
    ```
6. Then run the Python program to obtain scores on your hypothesis file(s): `python errant_evaluation.py . <output_dir> dev` where the dot is important (it signifies the input directory, the one where 'ref/' and 'res/' can be found) and <output_dir> could be the 'out' directory you created above, for instance.
7. Precision, recall and F0.5 scores will be written to your output directory in a file named "scores.txt"
