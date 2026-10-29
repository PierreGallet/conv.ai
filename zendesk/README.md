# zendesk — l'intégration au support

Amener conv.ai là où les équipes support travaillaient déjà : **juillet 2016**, 47 commits.

```
zendesk_app_front/    l'app Zendesk : Handlebars (.hdbs), affichée dans la barre latérale
zendesk_app_back/     le service Python appelé par l'app
  routes/             les points d'entrée
  machine_learning/   doc2vec, prétraitement, migration de données
  config/
```

L'agent ouvrait un ticket, l'app affichait dans sa barre latérale les réponses que le
modèle jugeait pertinentes. L'agent validait ou corrigeait — et la correction repartait
en donnée d'entraînement.

## Le lancer aujourd'hui

**Le back se lance**, c'est du Python sans dépendance exotique ; il faut lui refaire un
environnement propre.

**Le front, non.** C'est une app Zendesk Apps Framework **v1** ; le framework est en v2
et v1 n'est plus servi. Et même porté, il faudrait une instance Zendesk pour l'afficher.

Les corpus d'entraînement qui étaient versionnés ici — un extrait Wikipédia de 22 Mo et
un fichier de phrases de 19 Mo — ont été retirés de l'historique.
