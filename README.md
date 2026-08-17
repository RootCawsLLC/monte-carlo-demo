# Your First Monte Carlo

An interactive law-of-large-numbers demo: flip a fair coin anywhere from 10 to 100,000 times
and watch the running proportion of heads converge on 50% while the run-to-run noise collapses.

**Live:** https://rootcawsllc.github.io/monte-carlo-demo/

![The loss-convergence panel with a US financial-services data-breach scenario selected. A table gives four iteration counts against how far each statistic moved between twelve identical runs: at 100 iterations the mean swings ±70% and the P99 ±81%; by 50,000 the mean is down to ±2.8%. The P50 column reads em-dash throughout because the median year for this scenario has no loss event at all](preview.png)

Also embedded as the *Monte Carlo* tab of the risk lab on my portfolio:
https://rootcawsllc.github.io/

## What it shows

Every Monte Carlo model rests on the same unglamorous fact: run a random process enough times and
the aggregate stops behaving randomly. Any single trial is a toss-up; the average of a hundred
thousand of them is a measurement. Swap "heads" for "we get hit this year", give the event a loss
range instead of one fixed outcome, and the same machinery becomes a rough FAIR model.

- **Running proportion chart** — plots heads ÷ flips after each flip (downsampled to 600 points),
  over a shaded 95% band derived from the binomial standard error, `SE = 0.5/√n`.
- **Sampling distribution** — runs the whole experiment 200 more times at the same `n` and bins
  the results, so you can see where your single run landed inside the spread.
- **Loss convergence** — the same question asked of a real loss model rather than a coin. Pick a
  source-backed scenario, and it runs the compound-Poisson simulation the other risk tools use at
  100, 1,000, 10,000 and 50,000 iterations, twelve times each, reporting how far the mean, P50, P90
  and P99 move between identical runs.

The third panel is the one that changes how you read the other tools. A coin has one number to
settle. A loss model has several, and they do not settle together: a mean uses every draw, while a
P99 is read off the worst one percent, so 10,000 iterations leave it roughly a hundred events to
stand on. The further into the tail you quote, the more iterations you owe the number — and "we ran
10,000 simulations" stops being a reassurance and becomes a question about which statistic you are
quoting.

## Build

Single self-contained `index.html` — React 18 via UMD CDN, no build step, no dependencies.
Styled to match the palette and type system of the RootCaws design system: powder
rose surfaces, warm ink, rose accent, Fraunces for display and Inter for UI.

## Running locally

```bash
python -m http.server 8000
```

Then open http://localhost:8000. The loss-convergence panel fetches the scenario corpus over HTTPS;
if that is unreachable it says so and the coin demo is unaffected.

## Honest limits

A training exercise, not a production model — a fair coin with independent flips. Real risk events
are neither independent nor identically distributed. The principle still holds: more observations,
less noise, better estimates.

**Twelve repeats is a small sample, and the loss table says so.** Each spread in that table is
itself an estimate with its own noise, which is the same lesson one level up. Press Run twice and
the figures move, sometimes enough to reorder the columns — so read the table for the shape of the
problem, not as a measurement of any particular statistic's convergence rate. A real convergence
study runs far more repeats at far more rungs.

**The ladder stops at 50,000 for browser reasons, not statistical ones.** Twelve runs at each of
four rungs is about a fifth of a second; extending it far enough to settle a P99 properly would
not be.

## Attribution

Loss scenarios come from [risk-benchmarks](https://github.com/RootCawsLLC/risk-benchmarks), which
derives them from [RiskShard](https://github.com/raviaxo/RiskShard) by
[raviaxo](https://github.com/raviaxo), AGPL-3.0.

## License

Copyright (c) 2026 RootCaws LLC.

[GNU AGPL v3 or later](LICENSE). If you modify this and run it as a network service, the AGPL requires you to offer your users the modified source under the same terms.
