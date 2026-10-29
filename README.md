<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo-dark.png">
    <img src="assets/logo.png" alt="conv.ai" width="200">
  </picture>
</p>

<p align="center"><i>Answering customers without humans — Paris, 2016</i></p>

---

My first company, in 2016. The idea fit in one sentence: **use natural language
processing to answer customers instead of people** — at a time when "chatbot" was still
a new word and "transformer" meant nothing.

This repository gathers the five pieces it was made of. Each used to live in its own
repository; their history is intact here, **159 commits from May to September 2016**.

The code still carries the name **Sendit**, which is what the product was called at
first. And **SFR** shows up everywhere: they were our proving ground, and their help
centre and support threads became the dataset for everything else.

## The five pieces

| | What | When | Stack |
|---|---|---|---|
| [`sendit/`](sendit/) | The product: the web app | May → Jul. 2016 | Meteor 1.3 + Angular Material |
| [`zendesk/`](zendesk/) | Plugging into the existing support desk | Jul. 2016 | Zendesk app + Python back end |
| [`messenger/`](messenger/) | The Facebook Messenger bot | Jul. → Sep. 2016 | Express 4 + Python bridge |
| [`blabladata/`](blabladata/) | The engine: classification, embeddings, NER | Jul. → Sep. 2016 | Keras 1, Theano, gensim, scikit-learn |
| [`scraping/`](scraping/) | Collecting the training data | Sep. 2016 | Scrapy |

## How it fit together

```
  scraping/          collects help centres and support threads
      |
      v
  blabladata/        learns from them: intent, entities, similarity
      |
      +--------------+--------------+
      v              v              v
  sendit/       messenger/      zendesk/
  the product   on Facebook     inside the customer's own tool
```

`scraping` filled the dataset, `blabladata` learned from it, and the three front ends
queried the model — each one wherever the customer already was.

## What still runs, ten years on

| | State | What blocks it |
|---|---|---|
| `scraping/` | 🟢 starts | The target sites have changed: the spiders run and bring back nothing |
| `messenger/` | 🟡 the server starts | The 2016 Messenger API is gone; it now needs a Facebook page and app review |
| `zendesk/` | 🟡 the back end starts | The front end is a Zendesk Apps Framework v1 app; the framework is on v2 |
| `blabladata/` | 🔴 does not start | Theano was abandoned in 2017, Keras has had three major versions since — and **the data is not in the repository** |
| `sendit/` | 🔴 does not start | Meteor 1.3 needs Node 4 |

The Python itself aged well: not a single `print` without parentheses anywhere in the
repository. It isn't the source that rotted, it's its dependencies.

## What isn't here

- **The data.** No training corpus was ever committed.
- **The trained models.** They lived in the history — up to 79 MB each — and were removed:
  2016 scikit-learn pickles no longer load.
- **The keys.** A Google API key sat in `blabladata/misc/translate.py`, and two Facebook
  access tokens in `messenger/`. All three were stripped from the entire history.

The repository went from 282 MB to 8 MB along the way.
