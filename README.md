# e2e-Dutch

Code for e2e coref model in Dutch. The code is based on the [original e2e model for English](https://github.com/kentonl/e2e-coref), and modified to work for Dutch.

Installation:

    pip install setuptools virtualenv
    git clone https://github.com/andreasvc/crac2020.git
    cd crac2020
    virtualenv venv
    source venv/bin/activate
    pip install -r requirements.txt
    pip install -e .
    bash scripts/setup_all.sh

Get models:

    wget https://github.com/andreasvc/crac2020/releases/download/v0.1.1/models.tar.gz
    tar -xzf models.tar.gz

There are three models:

- riddlecoref: trained on novels (preprocessing: Alpino tokenizer).
- sonar1aligned: trained on SoNaR-1 with Lassy Small sentence and token boundaries (preprocessing: Alpino tokenizer).
- sonar1: trained on SoNaR-1 (preprocessing: SoNaR-1 sentence and token boundaries).

Example:

    $ cat test.txt
    "Ik heb op Obama gestemd vanwege zijn mooie toespraken", zei ze.
    $ python3 scripts/predict.py riddlecoref test.txt
    [...]
    #begin document (example);

    example 0       ``      -
    example 1       Ik      (0)
    example 2       heb     -
    example 3       op      -
    example 4       Obama   (1)
    example 5       gestemd -
    example 6       vanwege -
    example 7       zijn    (1)|(2
    example 8       mooie   -
    example 9       toespraken      2)
    example 10      ''      -
    example 11      ,       -
    example 12      zei     -
    example 13      ze      (0)
    example 14      .       -

    #end document

