# Bayesian Strategic Optionality (BSON)

BSON is a project about valuing corporate investments when the future is uncertain.

Most investment methods, such as discounted cash flow (DCF) and real options, look at the value of a single investment. But an investment can also lead to other opportunities. It can help a company learn more about the market and make better decisions about what to invest in next.

BSON can be used to capture this additional value. Instead of looking at each investment on its own, this looks at how one investment can lead to others and how new information can affect future decisions.

## What's in the repository

- **Hidden regimes and Bayesian updating:** How the model represents different market conditions and updates its beliefs when new information is available.
- **The opportunity graph:** How one investment can open up other investment opportunities and the probability of each opportunity becoming available.
- **BSON valuation:** How the model calculates the value of an investment along with the opportunities it may create in the future.
- **Numerical checks:** Tests for four properties that the BSON model is expected to satisfy.
- **Policy simulation:** A simulator where all investment strategies face the same conditions, signals, payoffs and future opportunities. This makes the comparison between them fair.
- **Five investment strategies:** DCF, Bayesian myopic, real options, the BSON strategic agent, and another experiment that knows the true market condition.
- **Additional experiments:** Three tests to check where the model might fail, along with experiments that change the discount factor and the chances of future opportunities becoming available.
- **Machine learning extension:** An experiment that replaces the Bayesian filter with machine learning classifiers of different accuracy and then checks how much their predictions affect investment value.

## Main results

The results come from 800 paired trials across two seed blocks.

One result is that learning makes a difference. Updating beliefs when new information arrives gives around 25 more units of discounted value compared with always using the same starting beliefs. When the signals provide no useful information, this extra value becomes exactly zero. This is what the model predicts.

The comparison between the BSON and the real options strategy is a little more interesting. The BSON performs slightly better overall, but the confidence interval includes zero, so the overall difference is not statistically clear.

Looking at different market conditions gives a better picture. In weak regimes, BSON loses a small amount by keeping future opportunities open. In moderate and strong regimes, it gains more from those opportunities. The differences in all three regimes remain significant even after Bonferroni correction.

Another result is that the strategic agent does better when future opportunities are more likely to become available. This makes sense because an investment is worth more when it has a better chance of opening the door to other investments.

The machine learning experiment also gives an interesting result. Higher prediction accuracy does not always mean higher investment value. Two classifiers with almost the same accuracy can lead to very different results. This shows that how well a model estimates probabilities matters, not just whether it predicts the correct class.

## Properties tested

The notebook tests four properties of the BSON model using randomly generated inputs:

1. **No future opportunities:** When all edge probabilities are zero, BSON gives the same value as belief-based NPV.
2. **Non-negative network value:** Adding future opportunities cannot reduce the value of an investment.
3. **Monotonicity:** Increasing the chance of a future opportunity becoming available cannot reduce BSON value.
4. **No information, no learning gain:** When signals contain no more information than chance, the updated beliefs remain the same as the prior, and there is no gain from learning.

These tests check whether the model behaves as expected. They are numerical checks, not formal mathematical proofs.

## Running the notebook

The notebook runs on Kaggle and Google Colab.

The packages are:

- NumPy
- NetworkX
- Matplotlib
- Scikit-learn

## Scope and limitations

The model uses a simulated environment rather than real company data. Its parameters are chosen for the experiments and have not been fitted to actual corporate investments.

For example, the opportunity graph and the chances of future opportunities becoming available are given as inputs. To use BSON with a real company, these values would need to be estimated from actual business or industry data. This is something that can be explored in future work.

The valuation equation also leaves out some practical limits, such as how much money a company has available and the fact that it can only make one investment decision in each period. The simulation takes these limits into account when comparing the strategies.

This model uses Gaussian distributions to generate payoffs. This means some outcomes can be negative, or representing losses or unexpected costs.

## License

MIT
