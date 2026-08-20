## Matthew Ballou

Software engineer. Laravel and PHP on the backend, TypeScript and React on the front.

By day I build Laravel applications for enterprise clients at a consultancy — trading and payments,
regulated pharmaceutical content, virtual patient observation. The repositories below are what I
build alongside that, and each one is pinned to answer a different question.

### What to look at, depending on what you want to know

**[suivre](https://github.com/mgballou/suivre)** — *can he ship a real product?*
A food and symptom journal that correlates diet and lifestyle with inflammatory flares on a lag.
Laravel 13, Inertia and React 19, Filament 5, PostgreSQL, held at PHPStan level 9 with no baseline.
→ Read [`docs/decisions/decision-log.md`](https://github.com/mgballou/suivre/blob/main/docs/decisions/decision-log.md).
Every product and architecture decision with the reasoning attached, including the ones I reversed
and what changed my mind.

**[dread-majesty](https://github.com/mgballou/dread-majesty)** — *can he hold an architectural boundary?*
An incremental game where each tier of production pays out in the tier below it.
[Playable here.](https://dreadmajesty.netlify.app) `packages/engine` is pure TypeScript: no DOM, no
React, no I/O and no clock. Time and seeds enter as arguments at the boundary, and lint enforces
that rather than convention — which is what makes every engine test a plain assertion against a
fixture, with no mocks and nothing flaky.
→ The part worth reading is the fixed-timestep simulation. Live play and offline catch-up run the
same `step` the same number of times, so there is no second code path for coming back after a week.

**[playlist-me-3](https://github.com/mgballou/playlist-me-3)** — *what does he do when a dependency dies?*
Spotify playlists built from inputs you choose. Spotify deprecated the recommendation and
audio-feature endpoints this project was built on, so the engine is now local, pure and
deterministically seeded — a recipe plus a seed reproduces a playlist exactly.
→ A fake client ships beside the live one behind the same interface, which is why demo mode, the
integration tests and the whole browser suite run with no credentials and no network. Clone it and
it works.

**[someones-pc-teambuilder](https://github.com/mgballou/someones-pc-teambuilder)** — *how does he model a domain?*
A team-building companion for competitive Pokémon: damage, speed tiers, coverage and legality.
Next.js, React 19, PostgreSQL over Drizzle.
→ Damage is integer-exact and returns all sixteen possible rolls rather than sampling one, because
the calculator has no business rolling dice. Formats are data, so nothing in the codebase switches
on a format id and adding a regulation is a data change rather than a branch.

**[suivre-insights-poc](https://github.com/mgballou/suivre-insights-poc)** — *does he check whether his ideas work?*
A simulation study asking whether Suivre's headline insight actually finds a real dietary trigger,
and how often it blames the wrong food.
→ It found the insight is real but fragile: an innocent food that travels with a real trigger gets
flagged 61% of the time, and that does not wash out with more data. The verdict made the product's
promise **weaker and later** — gate the feature at ninety days, and never show a ranking as a
confident trigger list.

### What these have in common

Every one of them keeps its domain logic free of the framework it happens to run on, and every one
has a document saying why it is built the way it is. Those two habits pay for each other. Suivre's
Actions, enums and policies were identical whether the interface was Livewire or React, which is
what made replacing the entire frontend cheap enough to be worth doing — and the decision log is
where I had to argue that the move was about fluency rather than about the component library that
triggered it.

---

[LinkedIn](https://www.linkedin.com/in/mballou/)
