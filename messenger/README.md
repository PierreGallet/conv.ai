# messenger — le bot Facebook

Le bot Messenger de conv.ai : **juillet à septembre 2016**, 64 commits.

Un serveur **Express 4** (`engines: node 6.2.2`) qui expose un webhook. Facebook y poste
chaque message reçu par la page ; le serveur choisit une réponse et la renvoie par la
Send API. Le choix de la réponse passait par un arbre de dispatch construit à partir de
la FAQ SFR, avec un pont vers Python (`python-shell`) pour appeler les modèles de
`blabladata/`.

```
index.js                  le webhook et le serveur
controller/
  main-controller.js      l'aiguillage principal
  button-controller.js    les réponses à boutons
  python-controller.js    le pont vers les modèles
make_dispatcher_tree.js   construit l'arbre de décision depuis la FAQ
faq.json, link2answer.json, motifs.json    les données de la FAQ
views/                    pug, ejs et less pour les pages de service
```

## Le lancer aujourd'hui

**Le serveur se lance ; l'intégration Facebook, non.** Le webhook Messenger de 2016 a
disparu : il faut aujourd'hui une page Facebook, une app vérifiée et une revue manuelle
de Meta pour obtenir les permissions. Ça ne se refait pas pour une démo.

En revanche la logique de dispatch est autonome et intéressante en soi. Pour la voir
tourner, le chemin court est de remplacer le webhook par une petite page de chat locale
qui poste sur le même point d'entrée.

Le binaire `ngrok` et son archive, qui étaient versionnés ici, ont été retirés de
l'historique — 17 Mo pour un outil qui se réinstalle en une commande.
