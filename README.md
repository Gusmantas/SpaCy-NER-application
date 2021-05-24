# SpaCy-NER-application
Simple app that recognizes entities from a text. Made with python Sanic, SQLite, Vue 3 and SpaCy NLP library.


To run the app:

* Download or clone this repo
* Open it in cmd 
* Run ``python -m venv env`` to create virtual environment for python
* Navigate to: ``cd env`` -> ``cd scripts`` -> ``activate`` to activatate “activate.bat” file (mac: cd env -> cd bin -> activate)
* Navate back to initial folder ``cd ..`` -> ``cd ..``
* Run ``py -m pip install sanic databases[sqlite] spacy``
* Run ``python -m spacy download en_core_web_sm`` to install english language model (required for spacy)
* Run ``main.py`` file
* In terminal, navigate to ``cd frontend``
* Run ``nmp install`` and when it is done, run ``npm run dev``
