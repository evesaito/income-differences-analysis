# Income Differences Across Industries, Demographics, and Occupations / Senior Capstone Spring 2026

## What is this notebook?

This notebook uses 2024 American Community Survey (ACS) microdata from IPUMS USA to study annual wage differences between four industries (Manufacturing, Finance, Information, and Healthcare), and how much of those differences is related to worker characteristics and occupation. It covers data cleaning, descriptive statistics, Mincer-style wage regressions (WLS with robust standard errors), a Shapley-style decomposition of the industry gaps, and a sensitivity analysis of the occupation classification.

"Healthcare" is NAICS sector 62 (health care and social assistance).

This notebook originaly started as a group project for Senior Capstone course in Spring 2026 at Gerogia State University. Section 1-5 are the part of the original notebook, for which I was responsibil for data cleaning. I later added Section 6-8 and Appendx independently. The analysis in the original project was conducted by another group member.  

### Key findings
- Finance and Information pay about 31% and 37% more than Manufacturing; after adjusting for worker characteristics and occupation the gaps shrink to about 1% and 6%.
- Healthcare pays about 11% less before adjustment and about 17% less after adjustment (about 14% excluding social assistance).
- This Healthcare result is the most sensitive to how occupations are grouped (see the Appendix in the notebook).

![Raw vs. adjusted industry wage gaps](figures/industry_gap.png)

## Limitations
- **Descriptive, not causal.** All results are adjusted associations. The sample covers four industries only, not the whole U.S. labor market.
- **Annual wages.** "Full-time" is defined by usual weekly hours (≥ 40) only; weeks worked are not in the extract, so part-year workers may remain. Wages are top-coded at state-specific thresholds and not adjusted.
- **Sample restrictions.** The analysis sample is wage and salary workers aged 18–64 who are employed and not in school; workers in areas with indeterminable metropolitan status are excluded.
- **Standard errors.** Robust (HC1); ACS replicate weights are not used, so the survey design is only approximated.

See the Caveats in the notebook's Project Overview for details.


## Content
1. Project Overview
2. Import packages
3. Data cleaning and variable construction (Sections 1–5)
4. Descriptive statistics (Section 6)
5. Mincer-style wage regression, OLS vs. WLS with robust standard errors (Section 7)
6. Industry wage gap decomposition (Section 8)
7. Sensitivity to the occupation classification (Appendix)

## Data Used

The data are **not included** in this repository, because the IPUMS terms of use do not allow redistribution. To reproduce the results:

- Data: IPUMS American Community Survey (ACS) data
- Source: https://usa.ipums.org/usa/
- Sample: 2024 ACS
- Extracted data

|Type | Variable | Label |
|:---|:---|:---|
|H	| SERIAL| Household serial number|
|H | STATEFIP |	State (FIPS code)|
|H	| METRO	| Metropolitan status (where determinable)|
|P	|PERNUM	|Person number in sample unit|
|P	| PERWT |	Person weight|
|P	| SEX	| Sex|
|P	| AGE	| Age|
|P	|SCHOOL	|School attendance|
|P	|EDUC (general)	|Educational attainment [general version]|
|P	|EDUCD (detailed)	| Educational attainment [detailed version]|
|P	|EMPSTAT (general)|	Employment status [general version]|
|P	|EMPSTATD (detailed)	|Employment status [detailed version]|
|P	|CLASSWKR (general)	| Class of worker [general version]|
|P	|CLASSWKRD (detailed)|	Class of worker [detailed version]|
|P	|OCC	| Occupation|
|P	|IND	| Industry|
|P	| INDNAICS	| Industry, NAICS classification|
|P	| UHRSWORK	| Usual hours worked per week|
|P	| INCWAGE	| Wage and salary income|
|P	|MARST	|Marital status|
|P	|RACE (general)	|Race [general version]|
|P	|RACED (detailed)	|Race [detailed version]|
|P	|HISPAN (general)	|Hispanic origin [general version]|
|P	|HISPAND (detailed)	|Hispanic origin [detailed version]|

- Extract date: 2026-08-24
- Raw extract: 3,422,888 person records; analysis sample: 270,135 workers.
- **METRO coding:** IPUMS revised the METRO codes on 2026-01-28. The notebook assumes the revised coding (1 = not in metro area, 2 = indeterminable, 3 = not in central city, 4 = central city status indeterminable, 5 = central city). Extracts downloaded before that date use different codes and must be recoded.

The four industries were chosen for convenience, not by a systematic criterion, and the number was kept small to fit the scope of the capstone. The results therefore describe these four industries only and should not be read as a ranking of industries in general.


## How to run this notebook

1. Make sure to install uv on your computer. (https://docs.astral.sh/uv/)
2. For VS code, it is helpful to have the Python and Jupyter VS Code Extensions installed.
3. In terminal change directory to this project after cloning (usually `cd [PATH_TO_PROJECT]/Capstone`)
3. Run `uv sync` to install python packages and setup virtual environment (.venv folder).
4. Open seniorcapstone.ipynb, from VS code click "Select Kernel", and in the popup click "Python Environments", and then click the ".venv" Python environment.
5. Now the notebook is ready to run




