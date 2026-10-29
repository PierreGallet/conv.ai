# scraping — the collection

What fed `blabladata/`: **September 2016**.
A **Scrapy** project and three spiders.

```
spiders/sfr_spider.py      SFR's help centre and community threads — the main source
spiders/airbnb_spider.py   Airbnb's help centre
spiders/google_spider.py   search results
items.py, pipelines.py     the collected schema and its processing
format.py                  into the (label, sentence) format blabladata expects
```

The outputs from back then are still in the repository: `sfr.json`, `airbnb_tot.json`,
`link2answer.json`. This is the only place in conv.ai where real data survives.

## Running it today

**Yes.** Scrapy is still maintained and the project has the expected layout:

```bash
uv venv && uv pip install scrapy
scrapy crawl sfr -o output.json
```

But **the three spiders will bring back nothing**. They target CSS and XPath selectors
written in 2016; all three sites have been rebuilt since, and Google now blocks this kind
of collection outright. To watch them work, point them at a frozen page — the `airbnb.html`
kept here, for instance.

The Python 2 `.pyc` files that used to be committed were stripped from the history.
