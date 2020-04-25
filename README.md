# Pyrouge-installation
How to install Pyrouge for text summarization (only for Linux):

## Step 1 : Install Pyrouge from source
(not from pip => pip uninstall pyrouge if it's already installed) 

    - git clone https://github.com/bheinzerling/pyrouge 
    - cd pyrouge pip 
    - install -e .

## Step 2 : Install official ROUGE script
    - git clone https://github.com/andersjo/pyrouge.git rouge

## Step 3 : Point Pyrouge to official rouge script
    - pyrouge_set_rouge_path "/workspace/Transformers_BERT/pyrouge/rouge/tools/ROUGE-1.5.5"
 The path given to pyrouge should be absolute path ! (to get the absolute path : readlink -f directory)
    - python setup.py install



## Step 4 : Install libxml parser
You need to install libxml parser :

    - cpan App::cpanminus
    - cpanm XML::DOM
    - cpanm  XML::Parser


## Step 5 : Regenerate the Exceptions DB

    - cd  rouge/tools/ROUGE-1.5.5/data/
    - rm WordNet-2.0.exc.db
    - cd WordNet-2.0-Exceptions/
    - ./buildExeptionDB.pl . exc WordNet-2.0.exc.db
    - cd ..
    - ln -s WordNet-2.0-Exceptions/WordNet-2.0.exc.db WordNet-2.0.exc.db


## Step 6 : Run the tests
    - cd ..
    - python -m pyrouge.test
    
    
You should see :
Ran 11 tests in 6.322s
OK


## Usage example
```
from pyrouge import Rouge155
from pprint import pprint

ref_texts = {'A': "Poor nations pressurise developed countries into granting trade subsidies.",
             'B': "Developed countries should be pressurized. Business exemptions to poor nations.",
             'C': "World's poor decide to urge developed nations for business concessions."}
summary_text = "Poor nations demand trade subsidies from developed nations."


rouge = Rouge155(n_words=100)
score = rouge.score_summary(summary_text, ref_texts)
pprint(score)
```
