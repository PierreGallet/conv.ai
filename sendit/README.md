# sendit — le produit

L'interface web de conv.ai, et la première brique écrite : **mai à juillet 2016**,
12 commits. C'est aussi le nom que portait la boîte à ses débuts.

Une application **Meteor 1.3** avec **Angular 1 + Angular Material**. Le squelette vient
du tutoriel officiel Meteor-Angular — d'où le vocabulaire de `parties` qui traîne encore
dans `client/parties/` et `model/parties.js`. Greffés dessus : un modèle `prospect`
et une méthode serveur d'envoi d'e-mail.

```
client/     pages, routes, composants Angular Material
model/      parties.js (hérité du tutoriel), prospect.js
server/     méthodes (sendEmail), chargement initial des données
public/     les visuels — la machine à écrire, les captures du chat
```

## Le lancer aujourd'hui

**Il ne se lance pas en l'état.** `.meteor/release` épingle `METEOR@1.3`, qui tourne sur
Node 4 et n'a jamais été distribué pour les puces ARM. Trois voies, par coût croissant :

1. **Servir `public/` en statique** pour revoir l'interface, sans le serveur ni la base.
2. **Docker en `linux/amd64`** avec une image Meteor d'époque — fidèle, lent, incertain.
3. **Porter sur Meteor 3**, ce qui veut dire quitter Angular 1 : une réécriture.

Le dossier `public/` vaut le détour même sans serveur : c'est là qu'est resté le soin
graphique du produit.
