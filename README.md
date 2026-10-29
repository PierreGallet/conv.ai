# conv.ai

Ma première boîte, en 2016. L'idée tenait en une phrase : **utiliser le traitement
automatique du langage pour répondre aux clients à la place des humains**, à une époque
où « chatbot » était un mot neuf et où « transformer » ne voulait rien dire.

Ce dépôt rassemble les cinq briques qui la composaient. Elles vivaient chacune dans leur
dépôt ; leur historique est intact ici, **159 commits de mai à septembre 2016**.

Le code porte encore le nom **Sendit**, comme le produit s'appelait au départ.
Et **SFR** revient partout : c'était le terrain d'essai, leur FAQ et leurs fils de
support ont servi de jeu de données à tout le reste.

## Les cinq briques

| | Quoi | Quand | Stack |
|---|---|---|---|
| [`sendit/`](sendit/) | Le produit : l'interface web | mai → juil. 2016 | Meteor 1.3 + Angular Material |
| [`zendesk/`](zendesk/) | L'intégration au support existant | juil. 2016 | App Zendesk + back Python |
| [`messenger/`](messenger/) | Le bot Facebook Messenger | juil. → sept. 2016 | Express 4 + pont Python |
| [`blabladata/`](blabladata/) | Le moteur : classification, embeddings, NER | juil. → sept. 2016 | Keras 1, Theano, gensim, scikit-learn |
| [`scraping/`](scraping/) | La collecte des données d'entraînement | sept. 2016 | Scrapy |

## Comment ça s'emboîtait

```
  scraping/          collecte les FAQ et les fils de discussion
      |
      v
  blabladata/        apprend dessus : intention, entites, similarite
      |
      +--------------+--------------+
      v              v              v
  sendit/       messenger/      zendesk/
  le produit    sur Facebook    dans l'outil du client
```

`scraping` remplissait le jeu de données, `blabladata` apprenait dessus, et les trois
façades interrogeaient le modèle — chacune là où se trouvait le client.

## Ce qui tourne encore, dix ans après

| | État | Ce qui bloque |
|---|---|---|
| `scraping/` | 🟢 se lance | Les sites visés ont changé : les spiders tournent et ne ramènent rien |
| `messenger/` | 🟡 le serveur se lance | L'API Messenger de 2016 est fermée : il faut une page Facebook et une revue d'app |
| `zendesk/` | 🟡 le back se lance | Le front est une app Zendesk v1, le framework est en v2 |
| `blabladata/` | 🔴 ne se lance pas | Theano est abandonné depuis 2017, Keras a changé trois fois de version majeure — et **les données ne sont pas dans le dépôt** |
| `sendit/` | 🔴 ne se lance pas | Meteor 1.3 demande Node 4 |

Le code Python est resté lisible : pas un seul `print` sans parenthèses dans tout le
dépôt. Ce ne sont pas les sources qui ont vieilli, ce sont leurs dépendances.

## Ce qui n'est pas là

- **Les données.** Aucun corpus d'entraînement n'a jamais été versionné.
- **Les modèles entraînés.** Ils étaient dans l'historique, jusqu'à 79 Mo pièce, et en ont
  été retirés : des pickles scikit-learn de 2016 ne se relisent pas aujourd'hui.
- **Les clés.** Une clé d'API Google traînait dans `blabladata/misc/translate.py` ;
  elle a été retirée de tout l'historique.

Le dépôt est passé de 282 Mo à 54 Mo dans l'opération.
