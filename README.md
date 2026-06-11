# Bayesian Strategic Optionality (BSON)

A valuation framework for sequential corporate investment under technological
uncertainty. The standard tools, discounted cash flow and single asset real
options, value a project by its own cash flows. They miss the fact that one
investment often unlocks a chain of follow on opportunities and that a firm
learns about the world as it goes. BSON prices that chain explicitly.

## What the repository contains

The notebook builds the model from the ground up and runs every experiment end
to end. The sections are:

- The hidden regime model and the Bayesian filter.
- The opportunity graph with edge emergence probabilities.
- The recursive BSON valuation and four theorems verified numerically.
- A paired-world simulator where every policy faces an identical sequence of
  regimes, signals, payoffs, and unlock outcomes, so differences come from the
  policy alone.
- Five policies: DCF, Bayesian myopic, real options, the strategic agent, and
  an oracle that knows the true regime and serves as an upper reference.
- Three falsification tests, a discount factor sweep, and an edge probability
  sweep.
- A machine learning extension that replaces the exact filter with classifiers
  of varying quality and measures what predictive accuracy is worth in
  discounted cash terms.

## Main results

All numbers come from 800 paired trials across two seed blocks. The simulation
is fully seeded, so every figure reproduces exactly on re-run.

The learning result is large and unambiguous. Acting on updated beliefs rather
than a fixed prior is worth about 25 units of discounted value, and that value
falls to exactly zero when signals carry no information, which is the behavior
the theory predicts.

In aggregate, the strategic agent beats per node real options by a small margin 
whose confidence interval grazes zero. The effect becomes clear once results are
split by regime where the agent pays a small insurance cost in weak regimes
and earns a larger premium in moderate and strong regimes. All three
regime conditional margins survive Bonferroni correction. The premium also
grows monotonically as opportunities become more reliable to unlock which is
the comparative static the valuation equation implies.

The machine learning extension shows that the mapping from model accuracy to
portfolio value is steeply nonlinear and that two filters with nearly equal
accuracy can give very different value, so posterior calibration matters
more than top label accuracy when pricing a predictive model.

## Theorems

Four properties are stated and checked across random inputs

1. With all edge probabilities at zero, BSON equals belief NPV.
2. The network premium is always nonnegative.
3. BSON is monotone nondecreasing in every edge probability.
4. At chance-level signal accuracy the posterior equals the prior, so the
   learning value is identically zero.

## How to run

The notebook runs on Kaggle or Colab with no GPU and no internet access. A full
run takes upto a few minutes on CPU. The only dependencies are numpy, networkx,
matplotlib, and scikit-learn, all preinstalled in those environments.

The integrity checks near the main experiment confirm that results are deterministic and independent of 
evaluation order before any numbers are reported.

## Scope and limitations

The environment is synthetic and calibrated by construction rather than fit to
data. The opportunity graph and its edge probabilities are model inputs, the
way volatility is an input to an option pricing model; estimating them from
real corporate data is a separate problem and is a part of future work. The
valuation equation abstracts from cash constraints and from the one action per
period limit, both of which the rollout simulation handles when it scores
actual decisions. Payoff draws are Gaussian and may come out negative which
reads as a cost overrun and is deliberately not truncated since truncation
would bias the values the strategic agent relies on.

## License

MIT
