# Convergence Lab

How many trials does it take before a Monte Carlo answer stops moving? A fair coin first, from
ten flips to a hundred thousand, then the same question asked of a loss model, where the tail
settles far more slowly than the average.

**Live:** https://rootcawsllc.github.io/monte-carlo-demo/ — when to use it, how to use it, and how to take the pattern into an organisation.

![The lab at 1,000 flips. On the left, a ladder of twelve flip counts with 1K selected, the run's heads count and share, and a verdict on how far a repeat run would move. On the right, the running share of heads on a logarithmic flip axis inside a shaded 95% band; a zoomed histogram of where 200 repeated runs finished, with a strip beneath showing how narrow that window is against 0–100%; and the loss-model study for a US financial-services data-breach scenario, a table of how far the average, median, 1-in-10 and 1-in-100 figures moved between twelve identical runs at four iteration counts](preview.png)

Also embedded as the *Convergence Lab* tab of the risk lab on my portfolio.

## What it shows

- **One run, flip by flip.** The share of heads after every flip, drawn on a log axis so the
  early wander and the late settling get the same room. The shaded band is where 95% of fair-coin
  runs sit at each flip count, from the binomial standard error `0.5/√n`.
- **Two hundred runs, where they finished.** The whole experiment repeated 200 times at the same
  flip count, keeping only the finishing share. The axis zooms to the window the finishes occupy,
  and a strip underneath shows that window against the full 0–100% range, so the tightening is
  visible in the labels rather than lost in an ever-thinner spike.
- **The same question, asked of a loss model.** Pick a source-backed scenario and the tool runs
  the compound-Poisson simulation the other risk-lab tools use at 100, 1,000, 10,000 and 50,000
  iterations, twelve times each. Each cell reports how far that statistic moved between identical
  runs as a share of its own value, with a bar so the columns can be compared at a glance.

The third panel is the one that changes how you read the other tools. A coin has one number to
settle. A loss model has several, and they do not settle together: an average is built from every
simulated year, while a 1-in-100 figure is read off the worst one percent, so ten thousand
iterations leave it about a hundred years to stand on. The further into the tail you quote, the
more iterations you owe the number.

## Build

Single self-contained `index.html`: React 18 via UMD CDN, no build step, no dependencies. Styled in
the RootCaws palette: powder-rose surfaces, warm ink, rose accent, Fraunces for display type and
Inter for everything else.

## Running locally

Serve the directory with any static server so the relative fetch of `risk-benchmarks.json`
works, for example:

```bash
python -m http.server 8000
```

Then open http://localhost:8000. If the benchmarks file is unreachable the loss panel says so and
the coin is unaffected.

## Honest limits

A training exercise, not a production model: a fair coin with independent flips. Real risk events
are neither independent nor identically distributed. The principle still holds: more observations,
less noise, better estimates.

**Twelve repeats is a small sample, and the loss table says so.** Each spread in that table is
itself an estimate with its own noise, which is the same lesson one level up. Run it twice and the
cells move, sometimes enough to reorder them, so read the table for the shape of the problem rather
than as a measurement of any statistic's convergence rate.

**The ladder stops at 50,000 for browser reasons, not statistical ones.** Twelve runs at each of
four rungs takes well under a second; extending it far enough to settle a 1-in-100 figure
properly would not.

## Attribution

Loss scenarios come from [risk-benchmarks](https://github.com/RootCawsLLC/risk-benchmarks), which
derives them from [RiskShard](https://github.com/raviaxo/RiskShard) by
[raviaxo](https://github.com/raviaxo), AGPL-3.0. See [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

## License

Copyright (c) 2026 RootCaws LLC.

[GNU AGPL v3 or later](LICENSE). If you modify this and run it as a network service, the AGPL requires you to offer your users the modified source under the same terms.
