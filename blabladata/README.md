# blabladata — le moteur

Le cœur de conv.ai : **juillet à septembre 2016**, 30 commits.
Tout ce qui, dans le produit, relevait du traitement du langage.

```
formatting/        ramène n'importe quelle source à (label, phrase)
preprocessing/     tokenisation, étiquetage morphosyntaxique (TreeTagger)
embeddings/        TF-IDF, word2vec, doc2vec           — gensim, NLTK
classifiers/       régression logistique, forêts, réseaux — scikit-learn, Keras
ner/               reconnaissance d'entités             — CRFSuite
unsupervised/      similarité cosinus, k-means
paraphrase_detection/
misc/              récupération Intercom, traduction
```

Le pipeline complet : on normalisait les données en deux colonnes, on les nettoyait, on
les plongeait en vecteurs, puis on entraînait un classifieur d'intention. Les façades
(`sendit/`, `messenger/`, `zendesk/`) appelaient ensuite `predict.py`.

## Le lancer aujourd'hui

**Non, et pour deux raisons indépendantes.**

La première est technique : **Theano** (présent jusque dans le `.theanorc` du dépôt) est
abandonné depuis 2017, et le code vise **Keras 1**, à trois versions majeures de l'actuelle.

La seconde est plus définitive : **les données ne sont pas là.** Le README de 2016 disait
déjà de créer soi-même un dossier `data/`. Il n'a jamais été versionné, et il a disparu
avec la boîte. Les 11 modèles entraînés qui dormaient dans `tmp/` ont été retirés de
l'historique : des pickles scikit-learn de 2016 ne se relisent plus.

Ce qui reste faisable, et honnête à appeler un portage plutôt qu'une résurrection :
reprendre `embeddings/` et `classifiers/` sur scikit-learn et gensim actuels, et les
faire tourner sur un jeu de données public.

Le `requirements.txt` est à ignorer : c'est un `pip freeze` d'une installation Anaconda
entière, `anaconda-navigator` et `astropy` compris. Les vraies dépendances tiennent en
cinq lignes.
