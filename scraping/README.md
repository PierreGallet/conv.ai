# scraping — la collecte

De quoi nourrir `blabladata/` : **septembre 2016**.
Un projet **Scrapy** et trois araignées.

```
spiders/sfr_spider.py      la FAQ et les fils d'entraide SFR — la source principale
spiders/airbnb_spider.py   le centre d'aide Airbnb
spiders/google_spider.py   les résultats de recherche
items.py, pipelines.py     le schéma collecté et son traitement
format.py                  mise au format (label, phrase) attendu par blabladata
```

Les sorties de l'époque sont restées dans le dépôt : `sfr.json`, `airbnb_tot.json`,
`link2answer.json`. C'est le seul endroit de conv.ai où il reste des données réelles.

## Le lancer aujourd'hui

**Oui.** Scrapy est toujours maintenu et le projet a la structure attendue :

```bash
uv venv && uv pip install scrapy
scrapy crawl sfr -o sortie.json
```

Mais **les trois spiders ne ramèneront rien**. Ils visent des sélecteurs CSS et XPath
écrits en 2016 ; les trois sites ont été refaits depuis, et Google bloque aujourd'hui ce
genre de collecte. Pour les voir fonctionner, il faut les pointer sur une page figée —
par exemple le `airbnb.html` conservé ici.

Les `.pyc` de Python 2 qui étaient versionnés ont été retirés de l'historique.
