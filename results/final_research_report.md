# ALGORITHM BIAS
## Popularity Feedback Loops, Creator-Market Economics & Multi-Objective Recommendation

**Research project:** Dharshini H., Issac Samuel, Teena Baskar, Abhilash Mahata

## Abstract
This project investigates how recommendation-ranking objectives may affect creator exposure concentration and simulated sponsorship opportunity. Two public social-media datasets were analyzed, and a multi-round simulation compared engagement-first, exploration-based, and exposure-aware ranking policies. The simulation suggests that alternative ranking objectives can reduce exposure inequality, with a trade-off in the engagement proxy. These findings are conditional on the model assumptions and do not establish how any real platform's proprietary algorithm behaves.

## Research questions
1. How does engagement-oriented ranking distribute exposure across creators in a repeated simulation?
2. How does simulated exposure concentration relate to hypothetical sponsorship allocation?
3. How do engagement-first, exploration-based, and exposure-aware policies compare on exposure inequality and engagement proxy?
4. What trade-offs emerge when ranking objectives prioritize less-exposed creators?

## Data
- Instagram Analytics Dataset: 29,999 posts and 23 columns.
- Social Media Sponsorship and Engagement Dataset: 52,214 posts and 27 columns.

The datasets were used for descriptive analysis and to inform simulation inputs. The available data do not provide a controlled audit of Instagram's live recommendation algorithm or longitudinal real-world exposure histories.

## Method
An engagement-rate prediction experiment used a chronological train/test split and pre-outcome features. The mean baseline achieved MAE 0.018392 and RMSE 0.024337. Gradient boosting, random forest, and the neural network did not outperform the baseline, so predictive success is not claimed.

A separate simulation selected the 200 creators with the highest mean views and ran 20 rounds per policy. Ranking scores combined normalized engagement, popularity, novelty, or an exposure-deficit correction. Position-based exposure was assigned using a rank-decay function. A hypothetical sponsorship score combined cumulative exposure, engagement-weighted exposure, and follower count.

The revised V2 engine also includes a visibility-feedback term. Its results are reported separately from the original engine because the model formulation changed.

## V2 simulation results
| policy            |   exposure_gini |   top_10_exposure_share |   sponsorship_gini |   top_10_sponsorship_share |   mean_engagement_proxy |
|:------------------|----------------:|------------------------:|-------------------:|---------------------------:|------------------------:|
| engagement_first  |          0.6126 |                  0.2225 |             0.3121 |                     0.1354 |                  0.6754 |
| exploration_35    |          0.3452 |                  0.2035 |             0.2088 |                     0.1281 |                  0.6017 |
| exposure_aware_35 |          0.129  |                  0.1387 |             0.1317 |                     0.1019 |                  0.5221 |
| exploration_50    |          0.0292 |                  0.0562 |             0.0938 |                     0.0658 |                  0.4951 |
| exposure_aware_50 |          0.1204 |                  0.0826 |             0.102  |                     0.0677 |                  0.4582 |

Compared with engagement-first, exposure-aware 35% produced an exposure Gini reduction of **78.9%**, a sponsorship Gini reduction of **57.8%**, and an engagement-proxy change of **-22.7%**.

These are simulation-specific comparisons, not observed platform effects. The policy weights and feedback rules are researcher-defined assumptions.

## Ranking-weight sensitivity
| policy            |   fairness_weight |   exposure_gini |   top_10_exposure_share |   sponsorship_gini |   top_10_sponsorship_share |   mean_round_engagement_proxy |
|:------------------|------------------:|----------------:|------------------------:|-------------------:|---------------------------:|------------------------------:|
| engagement_first  |              0    |          0.6135 |                  0.2227 |             0.3127 |                     0.1352 |                        0.6778 |
| exploration_20    |              0.2  |          0.6102 |                  0.2227 |             0.3116 |                     0.1353 |                        0.6762 |
| exploration_35    |              0.35 |          0.5231 |                  0.2066 |             0.2766 |                     0.1279 |                        0.6514 |
| exploration_50    |              0.5  |          0.0221 |                  0.0543 |             0.0931 |                     0.0653 |                        0.4937 |
| exposure_aware_20 |              0.2  |          0.5688 |                  0.2227 |             0.2963 |                     0.1364 |                        0.6719 |
| exposure_aware_35 |              0.35 |          0.3484 |                  0.2048 |             0.2131 |                     0.129  |                        0.6073 |
| exposure_aware_50 |              0.5  |          0.0262 |                  0.0559 |             0.0924 |                     0.0656 |                        0.4918 |

The sensitivity experiment indicates that results depend strongly on the chosen weights. Near-uniform exposure under high exploration weights should not automatically be interpreted as a realistic or optimal recommendation policy.

## Predictive modelling results
| model             |     MAE |    RMSE |       R2 |
|:------------------|--------:|--------:|---------:|
| Mean baseline     | 0.01839 | 0.02434 | -0       |
| Gradient Boosting | 0.01841 | 0.02436 | -0.00166 |
| Random Forest     | 0.0187  | 0.0247  | -0.03036 |
| Neural Network    | 0.01892 | 0.02494 | -0.04987 |

The tested models did not beat the mean baseline. This negative result is retained rather than presenting an unsupported claim of predictive performance.

## Limitations
1. Both datasets are observational and do not establish causal effects of ranking.
2. The simulation uses researcher-defined ranking scores, rank-decay exposure, feedback, and sponsorship allocation rules.
3. The selected 200 creators are not necessarily representative of all creators.
4. Sponsorship allocation is hypothetical and is not a measurement of actual brand spending or creator income.
5. Policy labels and weight configurations should be standardized and validated before final publication.
6. Further work should test multiple random seeds, additional creator samples, alternative feedback strengths, and explicitly normalized ranking weights.

## Conclusion
Within this simulation, engagement-first ranking produced greater exposure concentration than several exploration-based and exposure-aware alternatives. Reducing concentration came with a lower engagement proxy, illustrating a multi-objective trade-off rather than a universally optimal ranking policy. Further validation is needed before drawing conclusions about real recommendation systems or creator markets.

## Reproducibility
Scripts and CSV outputs used in this project are stored in the project directory. Generated results should be interpreted alongside the exact simulation version that produced them.
