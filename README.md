# Socioeconomic Factors and ACT Performance

> This project explores how the socioeconomic characteristics of a school's surrounding community relate to its students' average ACT scores, using U.S. high school data from the 2016–2017 school year.

---

## Project Overview

Provide a short and concise overview of the project. Mention the problem it solves, the data used, and the key outcomes or findings.

- **Objective:** Clearly state the main goal of the project.
- **Domain:** (e.g., Healthcare, Finance, E-commerce, etc.)
- **Key Techniques:** (e.g., Regression, Classification, Clustering, NLP, Time Series)

---

## Project Structure

```
├── data/                 # Raw and processed data
├── code/                 # Jupyter notebooks and Python scripts
├── reports/              # Generated reports and visualizations
├── requirements.txt      # Dependencies
└── README.md             # Project documentation
```

---

## Data

- **Sources:**
  - [EdGap](https://www.edgap.org/): school ACT averages and census-tract socioeconomic measures ([Excel file used in this project](https://raw.githubusercontent.com/brian-fischer/DATA-5100/main/EdGap_data.xlsx))
  - [NCES Common Core of Data (CCD)](https://nces.ed.gov/ccd/files.asp): 2016–2017 public school directory file (`ccd_sch_029_1617_w_1a_11212017.csv`)
- **Description:**
  - EdGap: 7,986 schools, 7 columns (Excel). Includes school ID, census-tract unemployment rate, percent of adults with a college degree, percent of children in married-couple families, median household income, school average ACT score, and percent of students on free or reduced-price lunch.
  - CCD: 102,183 schools, 65 columns (CSV). Includes school ID, state, ZIP code, school type, school level, and charter status.
  - The two data sets are merged on the NCES school ID. After filtering to high schools and cleaning, the final data set (`education_clean.csv`) has 7,227 schools and 13 columns.
- **License:** EdGap and NCES CCD data are publicly available. CCD data is produced by the U.S. Department of Education and is in the public domain.

---

## Analysis

Describe the notebooks and/or scripts used to perform the analysis. Specify the order in which the code should be run to reproduce the results.

---

## Results

Include a short discussion of the findings and what they imply.

---

## Authors

- Your Name - [@yourhandle](https://github.com/yourhandle)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- Tools/libraries used
- Tutorials or papers referenced
- Inspiration or collaborators
