# Indian Job Market Ananlysis With Python 

An end-to-end exploratory data analysis project examining Indian data job trends, salaries, in-demand skills, and technology requirements using Python.

## Overview 

Welcome to my analysis of the Indian data job market, with a focus on opportunities in Data Engineering, Data Analytics, and related technology roles. This project was developed to better understand the skills, technologies, and salary trends shaping India's rapidly evolving data industry. The objective is to identify the most valuable technical skills and gain insights that can guide students and aspiring professionals toward informed career decisions.

The analysis is based on a comprehensive dataset of job postings used in Luke Barousse's Python course. The dataset includes information such as job titles, salary estimates, locations, and required technical skills. Using Python for data cleaning, exploration, and visualization, this project investigates key questions surrounding skill demand, salary distribution, technology trends, and the relationship between compensation and in-demand skills within the Indian job market.

## The Questions 

This project explores the Indian data job market by answering the following key questions:

1. **Where are Data Analyst opportunities concentrated across India, which companies hire the most Data Analysts, and what common job benefits and perks do they offer?**

2. **Which technical skills are most in demand across the three most common data-related roles?**

3. **What are the current trends in the demand for Data Analyst skills?**

4. **How do salaries vary for Data Analysts based on different technical skills and job requirements?**

5. **Which skills provide the best balance of high demand and high salary, making them the most valuable for aspiring Data Analysts to learn?**

## Tools Used

This project was built using a combination of Python libraries and development tools to clean, analyze, visualize, and manage the data efficiently.

- **Python** – The core programming language used for data cleaning, exploratory data analysis (EDA), and generating insights from the Indian data job market dataset.

### Python Libraries

- **Pandas** – Used for data manipulation, preprocessing, aggregation, and analysis.
- **NumPy** – Assisted with numerical operations and efficient array computations.
- **Matplotlib** – Used to create a variety of visualizations for analyzing trends and distributions.
- **Seaborn** – Helped build aesthetically pleasing and statistically informative charts.

### Development Environment

- **Jupyter Notebook** – Served as the primary environment for performing interactive analysis, documenting observations, and presenting findings.
- **Visual Studio Code** – Used for project organization, writing reusable Python scripts, and managing the overall project structure.

### Version Control

- **Git & GitHub** – Used for version control, tracking project progress, and hosting the complete source code and documentation, ensuring reproducibility and easy collaboration.

## Data Preparation & Cleaning

Before beginning the analysis, the dataset was cleaned and transformed to ensure consistency, accuracy, and reliability. The preprocessing pipeline involved importing the required libraries, loading the dataset, converting data types, and preparing columns for analysis.

### Importing Required Libraries

The following libraries were used throughout the project for data manipulation, visualization, and processing:

```python
import ast
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from datasets import load_dataset
```

### Loading the Dataset

The dataset was imported using the `datasets` library and converted into a Pandas DataFrame for further analysis.

```python
dataset = load_dataset("lukebarousse/data_jobs")
df = dataset["train"].to_pandas()
```

### Data Cleaning

To make the dataset analysis-ready, the following preprocessing steps were performed:

- Converted the `job_posted_date` column to the `datetime` format.
- Transformed the `job_skills` column from string representations into Python lists using `ast.literal_eval()`.
- Handled missing values where necessary to avoid errors during analysis.

```python
df["job_posted_date"] = pd.to_datetime(df["job_posted_date"])

df["job_skills"] = df["job_skills"].apply(
    lambda x: ast.literal_eval(x) if pd.notna(x) else x
)
```

### Filtering the Dataset

Since this project focuses exclusively on the **Indian data job market**, the dataset was filtered to include only job postings located in **India**.

```python
df_india = df[df["job_country"] == "India"].copy()
```

This filtered DataFrame served as the foundation for all subsequent exploratory analysis and visualizations.

## 1. Where are Data Analyst jobs most common in India, which companies hire the most analysts, and what benefits are commonly offered?

To gain an overview of the Indian Data Analyst job market, I filtered the dataset to include only **Data Analyst** roles located in **India**.

I then explored the geographic distribution of jobs, identified the companies with the highest number of openings, and analyzed common job benefits such as work from home opportunities, degree requirements, and health insurance. This analysis provides a snapshot of the hiring landscape before exploring skills and salary trends.

For Full Code : [Open Notebook](Project/1_EDA.ipynb)


### Results

- **Top Job Locations for Data Analysts in India**

![Locations](images/eda1file1.png)


- **Most Common Job Benefits & Requirements**

![Insights](images/eda2.png)

- **Top Companies Hiring Data Analysts**

![Companies](images/eda3.png)


### Insights

- Data Analyst opportunities are concentrated in India's major technology and business hubs.
- A small number of companies contribute a significant share of the available Data Analyst openings.
- Most employers continue to prefer candidates with a formal degree, while work-from-home and health insurance benefits vary across job postings.
- These findings provide a strong foundation for understanding the Indian job market before analyzing skill demand and salary trends.

## 2. Which technical skills are most in demand across the three most common data roles?

To identify the most sought-after technical skills, I analyzed job postings for the three most common data roles in India. After extracting and counting individual skills from each posting, I calculated the percentage of jobs requiring each skill. This highlights the core technologies employers expect candidates to possess across different career paths.

For Full Code: [2. EDA](Project/2_Skill_Count.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)
sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)

    sns.barplot(
        data=df_plot,
        x='skill_percent',
        y='job_skills',
        ax=ax[i],
        hue='skill_count',
        palette='dark:b_r'
    )

    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 75)

fig.suptitle("Likelihood of Skills Requested in Indian Job Postings")
plt.show()
```

### Results

**Likelihood of Skills Requested Across the Top 3 Data Roles in India**

*(Insert Skills Demand Chart)*

### Insights

- SQL and Python consistently rank among the most in-demand skills, making them fundamental across multiple data careers.
- Data Analyst, Data Engineer, and Data Scientist roles each require a unique combination of technical skills, reflecting the different responsibilities associated with each role.
- Data Engineering positions emphasize technologies related to databases, cloud platforms, and big data processing, while Data Analyst roles prioritize data querying, visualization, and reporting tools.
- Understanding these skill requirements helps aspiring professionals tailor their learning path based on the specific data role they intend to pursue.