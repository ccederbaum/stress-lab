# Private Credit Stress Lab

**Live demo: Live demo: [https://ccederbaum.github.io/stress-lab/](https://ccederbaum.github.io/stress-lab/)** (English / French)

An interactive stress test of a fictional private debt fund. Move four sliders (base rate, default rate, recovery, PIK share) and see what happens to the fund's equity return, covenant breaches and the losses absorbed by each tranche.

## Why this project

Private credit is often described as a stable asset class, partly because loans are not marked to market every day. I wanted a simple way to see what happens to a fund when rates stay high and defaults rise, and to explain who absorbs the losses first.

## How to use it

- Pick a preset (Base case, Higher for longer, Rate shock, Recession, Stagflation) or move the sliders.
- The headline figure is the equity IRR over 5 years, compared with the base case.
- The sentence under it explains in plain language what is happening in the selected scenario.
- Tick "Covenant breaches push defaults up" to link rate stress to defaults.

## Model assumptions

| Item | Assumption |
|---|---|
| Portfolio | 40 fictional loans, about EUR 400m, floating rate (Euribor + 5% to 7%) |
| Borrower leverage | 4.0x to 7.5x debt / EBITDA, randomly generated (fixed seed) |
| Covenant breach | Interest coverage (EBITDA / interest) below 1.3x |
| Fund structure | Senior 55% at Euribor + 2.50%, mezzanine 15% at Euribor + 6.50%, equity 30% |
| Fees | 0.8% of performing assets per year |
| Horizon | 5 years, annual steps, no reinvestment |
| Defaults | Constant annual rate on the performing balance |
| Contagion (optional) | Effective default rate = chosen rate x (1 + 2 x share of loans in breach), capped at 50% |
| Recoveries | Used to repay the senior first, then the mezzanine |
| PIK | Chosen share of interest is capitalised instead of paid in cash |
| Cash shortfalls | Accrued and settled before any later distribution, or at maturity |
| Equity return | IRR on annual distributions plus residual value at year 5 |

## What the model shows

A rate shock alone barely hurts the equity in this setup, because both the loans and the fund's own debt are floating rate, so most of the effect cancels out. The damage comes from defaults, including the defaults that higher rates trigger through covenant breaches. A fund with fixed-rate liabilities or hedges would behave differently.

## Limitations

- Fictional data and a deliberately simple model, for illustration only.
- Deterministic (expected-loss) approach: no randomness, no default clustering by sector.
- No hedging, no fixed-rate debt, no carried interest, no tax.
- Not investment advice.

## Tech

A single static HTML file with vanilla JavaScript. No dependencies, no build step, no server. The language switch (EN / FR) follows the browser language by default.

## Roadmap

- Calibrate default and PIK assumptions on public data from US business development companies (SEC filings).
- Add a slider for the share of fixed-rate debt in the fund.

## Built with

Developed with AI assistance (Claude, by Anthropic). The assumptions are documented above and open to challenge.

## Author

Christopher Cederbaum, https://www.linkedin.com/in/ccederbaum/
