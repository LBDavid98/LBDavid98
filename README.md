# David Hook

I build **governance and infrastructure for AI coding agents**, and the products
that come out the other side — a study app, a writing suite, an AI game master.
Most of what I ship is one of three things: a harness that makes an agent's
claims checkable, a piece of plumbing I got tired of every app re-growing badly,
or an app that needed both.

The through-line is that **self-reported success is not evidence**. An agent that
says "done, all tests pass" has produced a sentence. A receipt with a command, an
exit code and a timestamp has produced a fact. Nearly everything below is some
version of that argument.

---

## Open source

| | |
|---|---|
| **[scrumux-cli](https://github.com/LBDavid98/scrumux-cli-public)** | A governance harness for AI coding agents. Installs into a repo and makes the *record* — not the chat log, not the agent's recollection — the thing the next session works from. Four irreversible acts are refused by hooks that run before the tool does, including writing to the harness's own machinery. |
| **[react-lane-timeline](https://github.com/LBDavid98/react-lane-timeline)** | A swimlane timeline that takes both kinds of "when": a continuous fraction (`0.34`) *and* a named bucket (`now`/`next`/`later`). Those are different data models, most libraries solve one, and the other app writes its own. |
| **[react-agent-chat-window](https://github.com/LBDavid98/react-agent-chat-window)** | An embeddable in-app chat window for agent UIs, with a widget kit — so a proposal is a pair of buttons rather than a paragraph asking you to type "yes". Deliberately not a transport, not a theme, and not an opinion about your state library. |
| **[pgboss-scheduler](https://github.com/LBDavid98/pgboss-scheduler)** | pg-boss behind an HTTP API: push *or* pull delivery, HMAC-signed deliveries, timezone-aware cron that doesn't trust the container clock, and a dead-letter queue per queue **by default**. |
| **[asc-testflight-feedback](https://github.com/LBDavid98/asc-testflight-feedback)** | TestFlight beta feedback for every app on your App Store Connect team, pulled into Postgres and served over one small read API. Apple surfaces it in App Store Connect and nowhere else — there's no export, and the API resource is easy to miss. |

All MIT. Each one was extracted from a working app rather than designed in the
abstract, which is why the API arguments in those READMEs are so specific —
they're arguments I lost once already.

![react-lane-timeline: a three-lane story timeline with a tension curve](assets/react-lane-timeline.png)

---

## Things I can't open-source

These are commercial, so the code stays closed. The screenshots don't.

### Eigencards — a curriculum that knows its own shape

A calibrated spaced-repetition app for data science and ML, with an iOS client.
The interesting half is behind it: the **operator console over the content
pipeline**. 1,852 concepts and 6,254 generated cards, each card anchored on an
800–2400 difficulty scale by its depth in a hand-mapped prerequisite graph, with
an IRT-2PL pass to reconcile that anchor against how people actually answer.

You cannot review a curriculum that size in a table. So the console draws it —
the same graph four ways, and every view answers a different operator question.

**Taxonomy** — where the mass actually sits, by domain and sub-domain:

![Eigencards curriculum explorer, taxonomy view](assets/eigencards-taxonomy.png)

**Brain 3D** — 1,852 concepts projected onto anatomy, coloured by domain. Silly
on paper; it turns out to be the fastest way to see a domain that has grown a
lump where it shouldn't have one:

![Eigencards curriculum explorer, 3D brain view](assets/eigencards-brain-3d.png)

Card generation is a LangGraph pipeline in Python. Every factual claim on a card
is extracted and entailment-checked against a per-track allowlist of
authoritative sources before it ships.

### DraftNado — a local-first AI writing suite

A writing partner, not a ghostwriter: it drafts when you ask, tracks your story
so it stays consistent, and never rewrites what you wrote without your say-so.
Local-first — the manuscript is SQLite compiled to wasm, living in your browser,
not a row in someone's multi-tenant Postgres.

The **Studio** is the visual half: portraits, visual studies, manga panel
layouts, cinematics and a dialogue studio, all reading from the same World Bible
so a character stays on-model across every render.

![DraftNado's Studio — the gallery of generated assets for one story](assets/draftnado-studio.png)

The planning board underneath it — arcs as lanes, beats positioned along them,
a tension line over the top — is where
[react-lane-timeline](https://github.com/LBDavid98/react-lane-timeline) came
from. That's the usual direction of travel here: something gets built for one
app, then gets extracted once it has earned its API.

![DraftNado's planning board — an arc lane, its beats, and the chapter organizer below](assets/draftnado-planning-board.png)

### Mission Control — an AI game master that doesn't own the rules

An AI conductor for a tabletop RPG. It presents scenes, voices NPCs and applies
rules — but the authored module stays authoritative, a human moderator keeps
final control, and **the database, never the model, owns game state.** That
constraint is the whole design. A language model that holds the state will
eventually contradict it; a language model that reads the state from an
event-sourced store cannot.

Below is *The Lull* — the downtime week between missions, where a cell of players
each spend the one action a week buys them. It's the screen I'm proudest of,
because downtime is the part every system treats as bookkeeping.

![Mission Control's downtime screen — the map, the base, and the cell's week](assets/mission-control-the-lull.png)

Note the bottom bar: **one roll waiting on your confirmation.** The GM never
rolls against a player without the player saying yes first. Consent is a
mechanic, not a policy document.

---

## scrumux is open-core

The CLI is free and MIT and always will be — it installs into your repo, it keeps
working if you delete the clone, and it has no phone-home.

The **control plane** is the commercial half: one operator view across a fleet of
repos, ordered by who needs you. Ratification, blockers, drift and red checks in
one place, instead of `cd`-ing into each repo in turn to find out which is stuck.

![The scrumux control plane over a demo fleet](assets/scrumux-control-plane.png)

Commercial enquiries: **scrumux@businesskat.com**

---

<sub>Screenshots in the closed-source section are from private repositories, taken
against each project's own sample data or a purpose-built demo fleet — no
customer or third-party data appears in any of them.</sub>
