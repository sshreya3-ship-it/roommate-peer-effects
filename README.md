# Roommate Peer Effects: Evidence from Quasi-Random Dormitory Assignment

**Authors:** Catherine Ye, Shreya  
**Course:** DSO 599 – Causal Inference with Machine Learning for Business Analytics  
**Institution:** University of Southern California, Marshall School of Business  
**Date:** December 2025

---

## 📋 Project Overview

This project examines the causal effect of roommates' academic ability on student 
performance using quasi-random dormitory assignment at a Chinese public university. 
We leverage administrative data on 5,272 students across 15,680 student-semester 
observations to estimate peer effects while addressing selection bias through 
permutation tests, covariate balance checks, and alternative estimation strategies.

**Main Finding:** A one-standard-deviation increase in roommate GPA (≈20 percentile 
points) increases own GPA by 1 percentile point (β = 0.050, p < 0.001). Effects are 
47% stronger in academically homogeneous rooms and vary by within-room rank.

---

## 📁 Repository Structure
```
├── data/              # Raw data files (CSV format)
├── code/              # Jupyter notebook with complete analysis
├── output/            # Generated figures and tables
├── report/            # Final PDF report
└── README.md          # This file
```

---

## 🔢 Data Description

**Source:** Administrative records from a Chinese public university (2011-2012 cohorts)

**Sample:**
- 5,272 unique students
- 15,680 student-semester observations
- Two cohorts: 2011 (N=2,568) and 2012 (N=2,704)
- Observation window: 2-4 semesters per student

**Key Variables:**
- `gpa_post`: Student GPA percentile in current semester (0-1 scale)
- `gpa_prior`: Student GPA percentile in previous semester (0-1 scale)
- `rm_avg`: Average of three roommates' prior GPA percentiles
- `rm_diff`: Range of roommates' prior GPA percentiles (heterogeneity measure)
- `or_indorm`: Within-room rank (1=highest, 4=lowest)
- `gender`, `major`, `cohort`, `semester`: Control variables

**Data Files:**
1. `Data_GPA_Prior_Post_Actual.csv` - Main panel dataset (15,680 observations)
2. `Data_Student_Dorm_GPA_Actual.csv` - Student-level characteristics

---

## 🔬 Methodology

**Identification Strategy:**
- Quasi-random dormitory assignment within cohort × gender × major strata
- OLS regression with fixed effects (cohort, semester, gender, major)
- Permutation tests for validation (1,000 iterations)

**Robustness Checks:**
- Inverse Probability Weighting (IPW)
- Nearest Neighbor Matching
- Covariate balance tests
- Alternative specifications

**Main Specification:**
```
GPA_Post = α + β₁·GPA_Prior + β₂·RM_Avg + Cohort_FE + Semester_FE + Gender_FE + Major_FE + ε
```

---

## 📊 Key Results

| Model | RM_Avg Coefficient | Std. Error | p-value | R² |
|-------|-------------------|------------|---------|-----|
| (1) Bivariate | 0.3650*** | 0.0114 | <0.001 | 0.059 |
| (2) + GPA_Prior | 0.0618*** | 0.0050 | <0.001 | 0.666 |
| (3) Full Controls | 0.0500*** | 0.0050 | <0.001 | 0.669 |

**Heterogeneity Analysis:**
- Peer effects 47% stronger in homogeneous rooms (β₄ = -0.089, p = 0.089)
- Rank effects moderated by room composition (β₅ = -0.022, p = 0.012)

**Robustness (Q4 vs Q1 comparison):**
- OLS (implied): 2.52 percentile points
- IPW: 2.64 percentile points
- Matching: 2.73 percentile points

---

## 💻 Code Requirements

**Python Packages:**
```
pandas >= 1.3.0
numpy >= 1.21.0
matplotlib >= 3.4.0
seaborn >= 0.11.0
statsmodels >= 0.13.0
scipy >= 1.7.0
scikit-learn >= 1.0.0
```

**Installation:**
```bash
pip install -r code/requirements.txt
```

**Running the Analysis:**
1. Open `code/DSO599_RoommateGrade_Final.ipynb` in Jupyter or Google Colab
2. Update the data path in the first code cell
3. Run all cells sequentially (Runtime > Run all)

---

## 📄 Files and Outputs

**Main Analysis Notebook:**
- `code/DSO599_RoommateGrade_Final.ipynb` - Complete analysis with 5,223 lines


## 📚 References

- Sacerdote, B. (2001). Peer effects with random assignment: Results from Dartmouth 
  roommates. *Quarterly Journal of Economics*, 116(2), 681-704.
- Zimmerman, D. J. (2003). Peer effects in academic outcomes: Evidence from a natural 
  experiment. *Review of Economics and Statistics*, 85(1), 9-23.
- Carrell, S. E., Fullerton, R. L., & West, J. E. (2009). Does your cohort matter? 
  Measuring peer effects in college achievement. *Journal of Labor Economics*, 27(3), 
  439-464.

---

## 🙏 Acknowledgments

We thank Professor Mladen Kolar and the DSO 599 teaching team for guidance and feedback 
throughout this project.

---

*Last updated: December 2025*
