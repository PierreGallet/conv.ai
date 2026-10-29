# sendit — the product

conv.ai's web app, and the first piece written: **May to July 2016**, 12 commits.
It is also the name the company went by at the start.

A **Meteor 1.3** application with **Angular 1 and Angular Material**. The skeleton comes
from the official Meteor-Angular tutorial — which is why the vocabulary of `parties`
still lingers in `client/parties/` and `model/parties.js`. Grafted onto it: a `prospect`
model and a server-side email method.

```
client/     pages, routes, Angular Material components
model/      parties.js (inherited from the tutorial), prospect.js
server/     methods (sendEmail), initial data loading
public/     the visuals — the typewriter, the chat screenshots
```

## Running it today

**It does not start as is.** `.meteor/release` pins `METEOR@1.3`, which runs on Node 4
and was never shipped for ARM chips. Three routes, by increasing cost:

1. **Serve `public/` statically** to see the interface again, without server or database.
2. **Docker on `linux/amd64`** with a period Meteor image — faithful, slow, uncertain.
3. **Port to Meteor 3**, which means leaving Angular 1 behind: a rewrite.

`public/` is worth a look even without a server — that is where the product's visual
care survived.
