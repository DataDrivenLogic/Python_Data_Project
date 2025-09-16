# 📊 Data Analyst Skills & Salary Analysis (US)

---

## 📘 Introduction
This project analyzes job postings for **Data Analyst roles in the US** to understand:
- Which skills are most in-demand  
- Which skills offer the highest pay  
- How these skills have trended over time  

The goal is to provide practical insights for job seekers and professionals looking to align their skill sets with market demand.

---

## 🛠 Background
With the growing demand for data-driven decision-making, the role of a **Data Analyst** has become more important than ever. Employers often list multiple technical and business skills in job postings.  

By analyzing a dataset of job postings, I wanted to:
- Identify **top-paying skills**  
- Highlight the **most common skills** requested  
- Explore **yearly/monthly trends** for popular skills  

---

## 🧰 Tools Used
- **Python** (Data cleaning, transformation, and visualization)  
- **Pandas** (Data manipulation, grouping, aggregation)  
- **Matplotlib** & **Seaborn** (Data visualization)  
- **Jupyter Notebooks / VS Code** (Experimentation & documentation)  
- **Git & GitHub** (Version control & project sharing)  

---

## 📈 Analysis

### 1. Exploding job skills  
In the dataset, each job posting contained a list of required skills. To analyze them properly, I used the `explode()` function to convert list entries into individual rows.  

```python
df_exploded = df.explode('job_skills')
```
✅ Now each skill could be counted and analyzed independently.

2. Grouping by skill

Next, I grouped the data by each skill to calculate:

skill_count → how many job postings mentioned the skill
```
median_salary → median salary for jobs requiring that skill

skill_stats = df_exploded.groupby('job_skills').agg(
    median_salary=('salary_year_avg', 'median'),
    skill_count=('job_skills', 'count')
)
```

✅ This gave me a summary table of skills vs demand vs salary.

3. Top 10 lists

From the grouped data, I created two subsets:

Top Paid Skills → sorted by median_salary

Most In-Demand Skills → sorted by skill_count
```
df_top_pay = skill_stats.sort_values(by='median_salary', ascending=False).head(10)
df_top_demand = skill_stats.sort_values(by='skill_count', ascending=False).head(10)
```

✅ This allowed me to focus on the most relevant skills in the market.

4. Visualizations
🔹 Top 10 Highest Paid Skills
```
sns.barplot(data=df_top_pay, x='median_salary', y=df_top_pay.index, palette='Blues_r')
plt.title("Top 10 Highest Paid Skills for Data Analysts")
plt.xlabel("Median Salary (USD)")
plt.ylabel("Skills")
plt.show()
```

📊 Result: Specialized tools appeared in this list, often with fewer postings but higher salaries.

🔹 Top 10 Most In-Demand Skills
```
sns.barplot(data=df_top_demand, x='skill_count', y=df_top_demand.index, palette='Greens_r')
plt.title("Top 10 Most In-Demand Skills for Data Analysts")
plt.xlabel("Count of Job Postings")
plt.ylabel("Skills")
plt.show()
```

📊 Result: SQL, Excel, and Python dominated the demand side, being required in the majority of postings.

🔹 Trending Skills Over Time

To check how skills evolved month by month, I used a line plot.
```
from matplotlib.ticker import PercentFormatter

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills For Data Analyst in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()
plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))
```
# Annotate the lines with labels at their last point
```
for i, col in enumerate(df_plot.columns[:5]):
    plt.text(len(df_plot)-1.1, df_plot[col].iloc[-1], col)

plt.show()
```

📊 Result:

SQL stayed consistently high (~50% of postings).

Excel dipped slightly mid-year but recovered.

Python and Tableau remained steady around 25–30%.

SAS showed lower but steady demand.

📚 What I Learned

How to use explode() for list-like columns in Pandas.

Difference between dropna(subset=...) (DataFrame filter) vs Series.dropna() (column filter).

Usage of PercentFormatter for percentage-based axes.

Building multiple plots using fig, ax = plt.subplots() and accessing with ax[i].

Fixing overlapping labels by adjusting x/y positions or using adjustText.

Git & GitHub basics: init → add → commit → push → managing remotes.

🔍 Insights

SQL, Python, and Excel are the must-have skills for Data Analysts.

SQL dominated 2023, appearing in half of all postings.

Excel and Python were close contenders, often mentioned together.

Visualization tools (Tableau, Power BI) are increasingly relevant.

Some niche tools are rare but offer higher salaries.

🏁 Conclusion

This project highlights that:

The strongest skill combination for Data Analysts is SQL + Excel + Python.

Market demand generally aligns with salaries, but niche skills create pay premiums.

Trends show stability in core tools, with BI/visualization growing steadily.

✅ Next Steps:

Extend the analysis to other job titles (Data Scientist, Engineer).

Build an interactive dashboard for skills & salaries.

Expand to international markets for global insights