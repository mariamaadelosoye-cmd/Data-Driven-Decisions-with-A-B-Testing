# Data-Driven Decisions with A/B Testing

## Project Overview

This project evaluates whether a new search-ranking system improves booking conversion on an online booking platform without negatively affecting the booking experience.

Using A/B testing, I compared a control group using the existing system with a variant group exposed to the new system. The analysis combines statistical hypothesis testing, effect-size calculations, and business interpretation to inform a potential rollout decision.

## Business Objective

The primary objective was to determine whether the new search-ranking system increases the proportion of sessions resulting in a booking.

Two metrics were evaluated:

* **Primary metric — Conversion rate:** The proportion of sessions that resulted in a booking.
* **Guardrail metric — Time to booking:** The average time, in minutes, taken to complete a booking among sessions that converted.

The significance level was set to α = 0.10.

## Dataset

The analysis used two datasets:

* `sessions_data.csv`: Session-level information, including user identifiers, session start times, booking timestamps, and time to booking.
* `users_data.csv`: User identifiers and their assigned experimental groups (control or variant).

The datasets were joined using `user_id`. The resulting analytical dataset contained 15,283 sessions linked to experimental group assignments.

A binary conversion variable was created, with 1 representing a session that resulted in a booking and 0 representing a session without a booking.

## Methodology

The analysis followed these steps:

1. **Data exploration:** Examined dataset structure, missing values, and available variables.
2. **Data preparation:** Joined session and user data and created the conversion variable.
3. **Sample Ratio Mismatch (SRM):** Used a chi-square goodness-of-fit test to assess whether user allocation was consistent with the expected 50/50 split.
4. **Primary metric analysis:** Applied a two-proportion z-test to compare conversion rates and calculated confidence intervals and relative uplift.
5. **Guardrail analysis:** Used an independent two-sample t-test to compare mean time to booking and examined the standardized and relative effect sizes.
6. **Business recommendation:** Combined statistical evidence, effect sizes, and analytical limitations to assess the potential rollout.

## Key Results

### 1. Sample Ratio Mismatch

* Control group: 5,009 users
* Variant group: 4,991 users
* SRM test p-value: approximately 0.85

The result did not indicate a statistically significant sample ratio mismatch at α = 0.10.

### 2. Conversion Rate

| Metric          | Control | Variant |
| --------------- | ------: | ------: |
| Conversion rate |  15.92% |  18.19% |

* **Absolute uplift:** Approximately 2.27 percentage points
* **Relative uplift:** Approximately 14.2%
* **Two-proportion z-test p-value:** Approximately 0.000198

The conversion-rate difference was statistically significant at α = 0.10. The variant achieved a higher observed conversion rate than the control group.

### 3. Time to Booking

| Metric               |       Control |       Variant |
| -------------------- | ------------: | ------------: |
| Mean time to booking | 15.01 minutes | 14.89 minutes |

* **Relative change:** Approximately −0.79%
* **Independent two-sample t-test p-value:** 0.5365
* **Cohen's d:** Approximately 0.024 in magnitude

The test did not find a statistically significant difference in mean time to booking. The observed standardized effect was negligible.

This result does not establish that the booking experience is unaffected; the analysis only included sessions that resulted in bookings.

## Recommendation

The results support further consideration of the new search-ranking system because the variant achieved a statistically significant improvement in conversion, with a relative uplift of approximately 14.2%.

A cautious rollout with continued monitoring is recommended rather than assuming that the observed improvement guarantees success in production. Monitoring should cover conversion performance and the broader booking experience.

## Skills Demonstrated

* Exploratory data analysis
* Data cleaning and preparation
* Pandas data manipulation
* A/B testing and hypothesis testing
* Chi-square goodness-of-fit testing
* Two-proportion z-tests
* Independent two-sample t-tests
* Confidence intervals and effect-size interpretation
* Statistical reasoning and business decision-making
