# The Analysis

## What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targetting.

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](2_Project/images/2_Skills_Count.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```

### Results
![Visualization of Top Skills for Data Nerds](2_Project/images/skill_demand_all_data_roles.png)

### Insights

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills(AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).


## 2. How are in_demand skills trending for Data Analysts?

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter

df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
```

### Results

![Trending Top Skills for Data Analysts in US](2_Project/images/Skill_Trend.png)
*Bar graph visualizing the trending top skills for data analysts in the US in 2024.*

### Insights:
- SQL consistently tops the chart throughout 2024 as the most in-demand skill for data analysts in the U.S. Even with slight fluctuations, its demand stays well above 13%, peaking at over 14% in January.
- Excel follows SQL as the second most requested skill, maintaining over 10% demand. Noticeable dip from May through October suggests that companies may be leaning toward more modern tools in the middle of the year.
- Python and Tableau are neck and neck, hovering between 7%–8% likelihood in job postings. They cross each other mid-year, with Tableau momentarily overtaking Python in August.
- SAS trails behind all other skills, never crossing 6%. It even dips below 5% mid-year, with a slight recovery by December.
- There's no explosive growth for any new skill — stability dominates the year. Tools like SQL and Excel are "evergreens," while Python and Tableau are "rising specialists."


## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds

### Visualize Data 

```python
sns.boxplot(data=df_US, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```

### Results

![Salary Distributions of Data Jobs in the US](2_Project/images/Salary_boxplot.png)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

#### Insights

- Senior roles (Senior Data Scientist, Senior Data Engineer, Senior Data Analyst) consistently earn more than their non-senior counterparts. Median salaries for senior titles are significantly higher, with Senior Data Scientists and Senior Data Engineers positioned at the top.
- Both Data Engineers and Data Scientists have overlapping salary ranges. Data Engineers (both senior and standard) show a higher upper range than equivalent Data Scientists, possibly reflecting demand in data infrastructure.
- Senior roles exhibit wider salary distributions, with larger box plots and more frequent outliers, indicating both greater earning potential and variability.
- Data Analyst and Senior Data Analyst positions have the lowest medians and lower upper incomes compared to engineering and scientist roles. Significant salary jump is observed when progressing from Data Analyst to Data Scientist or Data Engineer positions.
- Outliers for all roles suggest some individuals earn substantially above the typical range, possibly due to location, company size, or niche expertise.
- Career Progression: Targeting engineering or scientist paths, and planning for senior roles, offers better long-term earning opportunities.
- Salary Negotiation: Leverage knowledge of upper-range outliers as benchmarks, especially when possessing unique skills.
- Role Comparison: Consider lateral moves (e.g., Data Analyst to Data Engineer/Scientist) for quicker salary growth rather than only seeking seniority in analyst paths.

### Highest Paid & Most Demanded Skills for Data Analysts

#### Visualize Data

```python

fig, ax= plt.subplots(2, 1)

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, ax=ax[1], hue='median', palette='light:b')

plt.show()

```

#### Results

![The Highest Paid & Most In-Demand Skills for Data Analysts in the US](2_Project/images/Highest_Paid_and_Most_In_Demand_Skills_For_Data_Analysts_in_the_US.png)
*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*


#### Insights
- Niche tools like dplyr, bitbucket, gitlab, solidity offer salaries near $190K+. AI-related skill hugging face is among top earners — GenAI pays big. Tools like ansible, couchbase, mxnet pay well but are less common — rarity = $$$.
- Core tools: python, r, sql, tableau, power bi — used in most analyst roles. Business tools like excel, powerpoint, word are still highly valued.

