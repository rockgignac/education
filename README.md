# Do Socioeconomic Factors Predict ACT Scores?

## Project Overview

A school's average ACT score is often used as one way to measure how well the school is doing, but schools do not all start from the same place. This project tests whether school performance, measured by the average ACT score, is predicted by socioeconomic factors. It uses 2016–2017 data on 7,227 U.S. high schools from EdGap and the National Center for Education Statistics (NCES). The socioeconomic factors are the unemployment rate, percent of adults with a college degree, percent of children in married-couple families, and median household income of the census tract around each school, plus the percent of the school's students on free or reduced-price lunch. As an additional predictor, the project also looks at whether charter schools score differently after taking these factors into account.

The key finding is that socioeconomic factors do predict average ACT scores. A model with just three predictors (free or reduced-price lunch, percent of adults with a college degree, and unemployment rate) explains about 63% of the variation in ACT scores. The percent of students on free or reduced-price lunch is by far the strongest predictor. Charter status does not make a significant difference once the socioeconomic factors are included.

## Data

The data come from two sources:

- EdGap: school average ACT scores (or the ACT equivalent of SAT scores), free or reduced-price lunch rates, and census-tract socioeconomic measures: https://www.edgap.org/
  - The Excel file used in this project is loaded from the course GitHub repository: https://raw.githubusercontent.com/brian-fischer/DATA-5100/main/EdGap_data.xlsx
- NCES Common Core of Data (CCD): the 2016–2017 public school directory, which includes each school's state, ZIP code, school type, school level, and charter status: https://nces.ed.gov/ccd/files.asp

The two data sets are joined using the NCES school ID.

- EdGap: 7,986 schools and 7 columns
- CCD: 102,183 schools and 65 columns
- School year: 2016–2017

Files in this repository:

- Raw data: `data/ccd_sch_029_1617_w_1a_11212017.csv` (the EdGap file is loaded from the URL above)
- Clean data: `data/education_clean.csv` (7,227 high schools; columns: `id`, `rate_unemployment`, `percent_college`, `percent_married`, `median_income`, `average_act`, `percent_lunch`, `year`, `state`, `zip_code`, `school_type`, `school_level`, `charter`)

## Analysis

All data cleaning and analysis are in the notebook `Education_final.ipynb`.

**Data cleaning** (notebook sections "Loading the Data" through "Saving the Clean Data"):

1. Loaded the EdGap and CCD data and inspected the size, column types, and missing values of each data set.
2. Made pair plots of the EdGap variables to look at the relationships between them.
3. Renamed the columns to lowercase snake_case names and kept only the CCD columns needed for the analysis.
4. Converted the school ID in both data sets to the same type and joined them on the school ID (7,898 of 7,986 schools matched).
5. Replaced impossible values (ACT averages below 1 and negative free lunch percentages) with missing values.
6. Kept only high schools, checked for duplicate rows (none were found), and mapped the number of schools in each state.
7. Removed the 3 schools with a missing ACT average and filled in the missing predictor values with an iterative imputer.
8. Saved the clean data to `data/education_clean.csv`.

**Analysis** (notebook section "Modeling"):

1. Fit simple linear regression models of average ACT score on free or reduced-price lunch and median income, and checked the fit with residual plots.
2. Fit a quadratic model for median income and compared it to the linear model using an ANOVA F-test and the mean absolute error (MAE).
3. Fit a multiple linear regression model with all five socioeconomic predictors.
4. Fit a reduced model without the two predictors that were not significant and compared it to the full model using R-squared, MAE, and an ANOVA F-test.
5. Created standardized versions of the predictors so their coefficients could be compared directly.
6. Added charter status as an additional predictor and compared the charter model to the reduced model.

## Results

- **Best model:** The reduced model with free or reduced-price lunch, percent of adults with a college degree, and unemployment rate explains about 63% of the variation in ACT scores (R-squared of 0.628), and its predictions are off by about 1.15 ACT points on average. Adding percent married and median income did not improve the model (ANOVA p-value of 0.81).
- **Strongest predictor:** After standardizing the predictors, the effect of free or reduced-price lunch (-1.78 points per standard deviation) is about 6 times bigger than percent college (0.28) and about 14 times bigger than unemployment (-0.12).
- **Median income:** Income alone explains only about 21% of the variation, and its relationship with ACT scores levels off at high incomes. It is not significant once the other predictors are included because it overlaps with them.
- **Charter schools:** Charter schools have a lower average ACT score (19.02 vs. 20.36), but they also serve more students on free or reduced-price lunch. After controlling for the socioeconomic factors, the difference is small (-0.18 points) and not significant (p-value of 0.128).

These results suggest that a school's ACT average depends heavily on the poverty level of its students. The data only covers 20 states and one school year, so the results may not apply to the whole country.

The full write-up of the results is in `[communication document file name]`.

## Authors

Rock Gignac — [GitHub](https://github.com/rockgignac)

## License

This project is licensed under the MIT License. See the `LICENSE` file for details. The NCES data are in the public domain.

## Acknowledgments

- EdGap.org for providing the school ACT and socioeconomic data.
- The National Center for Education Statistics for providing the Common Core of Data.
- AI tools were used to help learn the Python syntax and methods for the regression models, as noted in the notebook.
