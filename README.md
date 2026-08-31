# Analysis of 2009–2010 Colorado Student Assessment Program (CSAP) Results for Colorado 9th Graders

## Overview
This project analyzes ninth-grade student performance on the Colorado Student Assessment Program (CSAP) in math, reading, and writing for the 2009 and 2010 school years. Colorado math scores were notably low during this period, prompting increased focus on math curriculum in high schools statewide. This analysis investigates whether math passing rates improved, whether that improvement came at the cost of reading and writing performance, and whether math passing rates can be predicted from reading and writing results.

Full analysis, code, and output: [`report/Final_Project_Sanvitha_Vallem.pdf`](report/Final_Project_Sanvitha_Vallem.pdf)

## Research Questions
1. Was there a significant improvement in math passing rates between 2009 and 2010? If so, was there a decline in reading and writing performance?
2. Is there a relationship between a school's passing rate in math and its passing rates in reading and writing? How accurately can math passing rates be predicted from reading and writing results?

## Data
- Source: Colorado Department of Education (CDE) Information Marketplace
- Subjects: Math, Reading, Writing (9th grade CSAP results)
- Years: 2009 and 2010
- Schools with fewer than 31 students in either year were filtered out
- A random sample of 120 unique schools was used for the passing-rate and modeling analysis

## Methodology
- **Language/tools:** R, tidyverse, dplyr, tidyr, ggplot2
- **Data preparation:** cleaning, filtering, reshaping (pivot_wider) into per-school passing rates
- **Inference:** bootstrap resampling to estimate the sampling distribution of the mean year-over-year difference in passing rates, with 95% confidence intervals (percentile method)
- **Association analysis:** pairwise correlation and simple linear regression between subjects (Math, Reading, Writing) using 2009 data
- **Prediction:** multiple linear regression using 2009 Reading and Writing passing rates to predict 2010 Math passing rates, evaluated using RMSE on held-out 2010 data

## Key Findings
| Subject | Bootstrap Mean Difference (2010–2009) | 95% CI | Interpretation |
|---|---|---|---|
| Math | +0.0318 | [0.0187, 0.0452] | Statistically significant increase |
| Reading | +0.0021 | [-0.0123, 0.0169] | No significant change (CI includes 0) |
| Writing | -0.0343 | [-0.0492, -0.0195] | Statistically significant decrease |

**Correlations between subjects (2009):**
- Reading vs. Writing: r ≈ 0.961
- Math vs. Writing: r ≈ 0.876
- Math vs. Reading: r ≈ 0.862

**Prediction performance (RMSE on 2010 test data):**
- Reading vs. Writing model: RMSE ≈ 0.0686
- Math vs. Writing model: RMSE ≈ 0.0957
- Math vs. Reading model: RMSE ≈ 0.0939
- Multiple regression (Math ~ Reading + Writing): RMSE ≈ 0.0915

## Interpretation
Math passing rates showed a statistically significant increase from 2009 to 2010, while writing passing rates significantly declined and reading showed no meaningful change over the same period. All three subjects are strongly positively correlated at the school level — schools with higher reading and writing passing rates tend to have higher math passing rates as well. A multiple linear regression using reading and writing passing rates predicts 2010 math passing rates with reasonable accuracy (RMSE ≈ 0.09), though the model does not account for confounding factors such as teaching methods, curriculum differences, or classroom environment.

## Limitations
- Findings are correlational, not causal — the model does not control for confounding variables (e.g., school resources, instructional changes, student demographics)
- Analysis is limited to a random sample of 120 schools meeting a minimum enrollment threshold
- Only two years of data are included, limiting the ability to assess longer-term trends

## Author
Sanvitha Vallem

## License
This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
