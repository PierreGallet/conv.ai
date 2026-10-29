# zendesk — plugging into the support desk

Bringing conv.ai where the support teams already worked: **July 2016**, 47 commits.

```
zendesk_app_front/    the Zendesk app: Handlebars (.hdbs), shown in the sidebar
zendesk_app_back/     the Python service the app called
  routes/             the entry points
  machine_learning/   doc2vec, preprocessing, data migration
  config/
```

An agent opened a ticket; the app showed, in their sidebar, the answers the model found
relevant. The agent accepted or corrected — and the correction went back as training data.

## Running it today

**The back end starts.** It is plain Python with no exotic dependency; it just needs a
clean environment rebuilt around it.

**The front end does not.** It is a Zendesk Apps Framework **v1** app; the framework is on
v2 and v1 is no longer served. And even ported, it would need a Zendesk instance to show it.

The training corpora that used to be committed here — a 22 MB Wikipedia extract and a
19 MB sentence file — were stripped from the history.
