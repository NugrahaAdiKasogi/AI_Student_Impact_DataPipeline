# AI Student Impact Data Pipeline

````md id="x7n2ka"
# AI Student Impact Data Pipeline

ETL (Extract, Transform, Load) pipeline project using Python, Pandas, PostgreSQL, and Supabase to process and analyze the impact of Generative AI usage on student academic performance.

---

# Project Overview

This project demonstrates a simple Data Engineering workflow by transforming raw student AI usage data into a dimensional data warehouse schema and loading it into Supabase PostgreSQL.

The project includes:
- Data Cleaning
- Data Transformation
- Star Schema Modeling
- ETL Pipeline using Python
- PostgreSQL Data Warehouse Deployment
- Cloud Database Integration using Supabase

---

# Tech Stack

- Python
- Pandas
- SQLAlchemy
- PostgreSQL
- Supabase
- Jupyter Notebook

---

# Dataset

Dataset used:
- AI Student Impact Dataset

Main topics inside the dataset:
- Student GPA
- AI Usage Habits
- Prompt Engineering Skill
- Burnout Risk
- Study Hours
- Institutional AI Policy

---

# ETL Workflow

## 1. Extract

Raw CSV dataset is loaded using Pandas.

```python
df_raw = pd.read_csv('ai_student_impact_dataset (1).csv')
````

---

## 2. Transform

Data cleaning process:

* Remove duplicate data
* Remove missing values

```python
df_cleaned = df_raw.drop_duplicates().dropna()
```

---

## 3. Data Modeling

The dataset is transformed into a Star Schema model consisting of:

### Dimension Tables

* dim_student
* dim_ai_profile
* dim_policy
* dim_risk

### Fact Table

* fact_student_ai_impact

---

# ERD (Entity Relationship Diagram)
```md
![ERD](images/ai_student_impact_erd.drawio.png)
```

Recommended folder structure:

```text
project/
│
├── images/
│   └── erd.png
│
├── notebook/
│   └── etl_pipeline.ipynb
│
├── .env
├── .gitignore
├── requirements.txt
└── README.md
```

---

# Star Schema Structure

## Dimension: dim_student

Stores student academic category information.

Columns:

* Student_ID
* Major_Category
* Year_of_Study

---

## Dimension: dim_ai_profile

Stores AI usage behavior information.

Columns:

* ai_profile_id
* Primary_Use_Case
* Prompt_Engineering_Skill
* Paid_Subscription

---

## Dimension: dim_policy

Stores institutional AI policy information.

Columns:

* policy_id
* Institutional_Policy

---

## Dimension: dim_risk

Stores burnout risk category.

Columns:

* risk_id
* Burnout_Risk_Level

---

## Fact Table: fact_student_ai_impact

Stores measurable metrics related to student academic performance and AI usage.

Columns:

* fact_id
* Student_ID
* ai_profile_id
* policy_id
* risk_id
* Pre_Semester_GPA
* Post_Semester_GPA
* Weekly_GenAI_Hours
* Traditional_Study_Hours
* Tool_Diversity
* Perceived_AI_Dependency
* Anxiety_Level_During_Exams
* Skill_Retention_Score

---

# Load Process

The transformed data is loaded into Supabase PostgreSQL using SQLAlchemy.

```python
engine = create_engine(DATABASE_URL)

dim_student.to_sql(
    'dim_student',
    con=engine,
    if_exists='replace',
    index=False
)
```

---

# Environment Variables

Store database credentials securely using `.env`.

Example:

```env
DATABASE_URL=postgresql+psycopg2://USERNAME:PASSWORD@HOST:6543/postgres
```

---

# Installation

Clone repository:

```bash
git clone https://github.com/your-username/AI_Student_Impact_DataPipeline.git
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the notebook or ETL script.

---

# Future Improvements

* Add Airflow orchestration
* Add dbt transformation layer
* Create Power BI dashboard
* Add automated data validation
* Deploy scheduled ETL pipeline

---

# Author

Nugraha Adiputra
