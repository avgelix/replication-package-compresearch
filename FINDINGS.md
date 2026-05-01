# Findings — Sprint 2: Cost of Living EDA

## Dataset

The analysis used a global cost-of-living dataset covering **5,000 cities** across **146 countries**, filtered to **4,000 cities** with complete data (`data_quality == 1`). The dataset spans 55 numeric dimensions including food, transport, rent, utilities, and salary.

---

## 1. Salary Distribution

Monthly after-tax salary across cities showed the following central tendency:

| Statistic | Value |
|---|---|
| Mean | 1988.8 |
| Median | 1569.0 |
| Mode | 1686 |
| Std Dev | 1591.3 |
| Variance | 2532178.7 |
| Min | 35.7 |
| Max | 7935.4 |
| Skewness | 0.84 |

**Key finding:** Salary is not normally distributed. The histogram reveals a bimodal distribution with peaks around 1,000 and 3,000, and a right-skewed tail extending to approximately 12,000. The Q-Q plot confirms this — lower quantiles fit a normal distribution reasonably well, but upper quantiles deviate sharply upward, meaning high-salary cities earn significantly more than a normal distribution would predict.

This suggests the dataset contains at least two distinct economic tiers of cities rather than a single continuous distribution.

---

## 2. Salary by Country

The highest average monthly salaries were recorded in:
1. Bermuda - 5973.81
2. Switzerland - 5953.02
3. Singapore — 5973.81

The lowest average monthly salaries were recorded in:
1. Cuba — 35.75
2. Syria - 50.24
3. Ivory Coast - 131.96

The global median country-level average salary was **591**. The gap between the highest and lowest earning countries was approximately **5938**, indicating substantial global income inequality across the cities sampled.

---

## 3. Salary, Rent, and Cappuccino Cost

A scatter plot comparing monthly salary (x-axis), city-center 1-bedroom rent (y-axis), and cappuccino cost (color) revealed:

- **Positive correlation** between salary and rent: cities with higher salaries tend to have more expensive city-center apartments.
- **Cappuccino cost tracks both variables**: more expensive cities on both salary and rent dimensions also charge more for a cappuccino, suggesting it functions as a rough proxy for overall cost of living.
- The relationship appears **heteroskedastic** — variance in rent prices increases at higher salary levels, meaning high-income cities vary more widely in their rental markets than low-income cities do.

---

## 4. Which Dimensions Vary Most Across Cities?

Using the coefficient of variation (CV = std / mean) as a scale-independent measure of variability, the most variable dimensions were:

1. apt_outside_centre_price_sqm — CV: 1.23
2. apt_city_centre_price_sqm — CV: 1.13
3. preschool_monthly — CV: 0.90

The least variable dimensions were:

1. summer_dress — CV: 0.30
2. gasoline_1L — CV: 0.34
3. toyota_corolla — CV: 0.35

**Key finding:** Many columns have CV above 0.3, indicating substantial cross-city variation. The highest-variance dimensions — including international school tuition, real estate prices, and monthly salary — are also the dimensions most likely to differentiate cities from one another. Low-variance dimensions are more uniform globally and are less useful for distinguishing individual cities.

---

## 5. Correlation Structure

The full correlation matrix across all 55 numeric columns revealed widespread positive correlations, consistent with a general cost-of-living factor underlying most dimensions.

**Strongest positive correlations (r > 0.8):**

- apt_1br_city_centre_rent ↔ apt_1br_outside_centre_rent: r = 0.97
- apt_3br_city_centre_rent ↔ apt_3br_outside_centre_rent: r = 0.95
- apt_1br_outside_centre_rent ↔ apt_3br_outside_centre_rent: r = 0.91
- apt_1br_city_centre_rent ↔ salary_after_tax_monthly: r = 0.80


**Inverse correlations (r < −0.8):** there were very few strong inverse correlations among the 50+ dimensions of cost of living. Some weak ones (around -0.5):

- cinema_ticket ↔ mortgage_interest_rate_pct: r = -0.58
- coke_pepsi_0_33L ↔ mortgage_interest_rate_pct: r = -0.58
- gasoline_1L ↔ mortgage_interest_rate_pct: r = -0.57

**Key finding:** The high intercorrelation across most dimensions suggests that cost of living operates largely as a single underlying factor — expensive cities tend to be expensive across the board. This has direct implications for high-dimensional analysis: dimensionality reduction techniques (e.g., PCA) would likely capture a large proportion of variance in the first component.

---

## Summary

The cost-of-living dataset is high-dimensional, globally diverse, and internally correlated. Salary is non-normally distributed and bimodal, pointing to distinct economic tiers. Most spending dimensions co-vary strongly, suggesting a latent general cost-of-living factor. The dimensions that best differentiate individual cities are those with the highest coefficient of variation — particularly real estate, cars, schools, and salary itself.

These properties make the dataset well-suited to studying how different interface conditions support analysis of high-dimensional, correlated data — which is the core motivation for using it in this research.
