# blabladata — the engine

conv.ai's core: **July to September 2016**, 30 commits.
Everything in the product that had to do with language.

```
formatting/        brings any source down to (label, sentence)
preprocessing/     tokenisation, part-of-speech tagging (TreeTagger)
embeddings/        TF-IDF, word2vec, doc2vec            — gensim, NLTK
classifiers/       logistic regression, forests, nets   — scikit-learn, Keras
ner/               named entity recognition             — CRFSuite
unsupervised/      cosine similarity, k-means
paraphrase_detection/
misc/              Intercom export, translation
```

The full pipeline: normalise the data into two columns, clean it, embed it into vectors,
then train an intent classifier. The front ends (`sendit/`, `messenger/`, `zendesk/`) then
called `predict.py`.

## Running it today

**No, and for two independent reasons.**

The first is technical: **Theano** — still present down to the `.theanorc` in this
repository — was abandoned in 2017, and the code targets **Keras 1**, three major versions
behind the current one.

The second is more final: **the data is not here.** The 2016 README already told you to
create a `data/` folder yourself. It was never committed, and it disappeared with the
company. The 11 trained models that slept in `tmp/` were stripped from the history:
2016 scikit-learn pickles no longer load.

What remains doable — and honest to call a port rather than a revival — is to take
`embeddings/` and `classifiers/` onto current scikit-learn and gensim, and run them on a
public dataset.

Ignore `requirements.txt`: it is a `pip freeze` of an entire Anaconda install,
`anaconda-navigator` and `astropy` included. The real dependencies fit in five lines.

A Google API key sat in `misc/translate.py` and was stripped from the entire history.
