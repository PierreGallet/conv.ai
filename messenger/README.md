# messenger — the Facebook bot

conv.ai's Messenger bot: **July to September 2016**, 64 commits.

An **Express 4** server (`engines: node 6.2.2`) exposing a webhook. Facebook posted every
message the page received; the server picked an answer and sent it back through the Send
API. Picking the answer went through a dispatch tree built from SFR's help centre, with a
bridge to Python (`python-shell`) to call the models in `blabladata/`.

```
index.js                  the webhook and the server
controller/
  main-controller.js      the main routing
  button-controller.js    button replies
  python-controller.js    the bridge to the models
make_dispatcher_tree.js   builds the decision tree from the help centre
faq.json, link2answer.json, motifs.json    the help centre data
views/                    pug, ejs and less for the service pages
```

## Running it today

**The server starts; the Facebook integration does not.** The 2016 Messenger webhook is
gone: it now takes a Facebook page, a verified app and a manual review by Meta to get the
permissions. That is not worth redoing for a demo.

The dispatch logic, on the other hand, stands on its own. The short path to seeing it work
is to replace the webhook with a small local chat page posting to the same entry point.

The `ngrok` binary and its archive, which used to be committed here, were stripped from
the history — 17 MB for a tool that reinstalls in one command.

Two Facebook access tokens were also removed from the entire history.
