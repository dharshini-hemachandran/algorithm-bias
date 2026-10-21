# ALGORITHM BIAS: Initial Simulation Analysis

## Research question
How do alternative ranking policies trade off simulated engagement against creator exposure inequality and sponsorship concentration?

## Experimental setup
- Creators per policy: 200
- Simulation rounds: 20
- Policies compared: exposure_aware, exploration, engagement_first
- Creator characteristics are derived from the supplied dataset.
- Ranking feedback, feed exposure and sponsorship allocation are simulated.

## Results
| policy           |   rounds |   creators |   exposure_gini |   top_10_exposure_share |   sponsorship_gini |   top_10_sponsorship_share |   mean_round_engagement_proxy |
|:-----------------|---------:|-----------:|----------------:|------------------------:|-------------------:|---------------------------:|------------------------------:|
| exposure_aware   |       20 |        200 |          0.3484 |                  0.2048 |             0.2131 |                     0.1290 |                        0.6073 |
| exploration      |       20 |        200 |          0.5231 |                  0.2066 |             0.2766 |                     0.1279 |                        0.6514 |
| engagement_first |       20 |        200 |          0.6135 |                  0.2227 |             0.3127 |                     0.1352 |                        0.6778 |

## Difference from engagement-first baseline
### exposure_aware
- Exposure Gini change: -43.2%.
- Sponsorship Gini change: -31.9%.
- Engagement proxy change: -10.4%.

### exploration
- Exposure Gini change: -14.7%.
- Sponsorship Gini change: -11.6%.
- Engagement proxy change: -3.9%.

## Figures
- `figures/exposure_inequality.png`
- `figures/engagement_fairness_tradeoff.png`
- `figures/inequality_over_rounds.png`

## Limitations
- This is a simulation, not an audit of Instagram's live ranking system.
- Exposure, feedback and sponsorship rules are researcher-defined assumptions.
- The engagement proxy is not observed platform engagement caused by these policies.
- Sponsorship shares are hypothetical allocations, not observed spending.
- Results depend on the selected creators, scoring weights and simulation rules.
- No causal claim or statistical significance claim is established by this run.
- Robustness checks across alternative parameters and creator samples are still needed.

## Conclusion
In this initial simulation, policies differ in their measured exposure inequality, sponsorship concentration and engagement proxy. These results describe the implemented simulation only. Further robustness tests are required before drawing broader conclusions.
