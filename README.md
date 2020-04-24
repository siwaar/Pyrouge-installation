# Pyrouge-installation
How to install Pyrouge for text summarization (only for Linux):

Step 1 : Install Pyrouge from source (not from pip)
git clone https://github.com/bheinzerling/pyrouge
cd pyrouge
pip install -e .

Step 2 : Install official ROUGE script
git clone https://github.com/andersjo/pyrouge.git rouge

Step 3 : Point Pyrouge to official rouge script
pyrouge_set_rouge_path ~/pyrouge/rouge/tools/ROUGE-1.5.5/
The path given to pyrouge should be absolute path !
(to get the absolute path : readlink -f directory)

Step 4 : Install libxml parser
You need to install libxml parser :
sudo apt-get install libxml-parser-perl

Step 5 : Regenerate the Exceptions DB
you need to regenerate the Exceptions DB :
cd rouge/tools/ROUGE-1.5.5/data
rm WordNet-2.0.exc.db
./WordNet-2.0-Exceptions/buildExeptionDB.pl ./WordNet-2.0-Exceptions ./smart_common_words.txt ./WordNet-2.0.exc.db

Step 6 : Run the tests
python -m pyrouge.test

You should see :
Ran 11 tests in 6.322s
OK
