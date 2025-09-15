# Trending Skills & Salary Analysis for Data Analysts (US)

This project explores the relationship between required job skills and salaries for Data Analysts in the U.S., using real job posting data. I analyze which skills are most in-demand, which skills pay the highest, and how those skills have trended over time.

---

## 🗂 Project Structure

- `3_Project/` — main folder containing the notebooks, datasets, and plots.  
- Exploded data of skills, grouped statistics (count, median salary).  
- Two key visualizations: one for top-pay skills, one for most in-demand skills.  
- Time-series chart of trending skills across months (showing likelihood in job postings).

---

## 🔍 Pipeline & Methods

1. **Explode job skills**  
   - Convert each row’s list of skills into separate rows.  
   - Enables counting and salary statistics per skill.  

2. **Compute statistics**  
   - Group by each `job_skill`:  
     - `skill_count` → how many job postings mention the skill  
     - `median_salary` → median of yearly salary for jobs requiring that skill  

3. **Top-10 subsets**  
   - **Top Paid Skills**: skills sorted by highest `median_salary`.  
   - **Most In-Demand Skills**: skills sorted by highest `skill_count`.

4. **Plotting**  
   - Horizontal bar plots (sns / pandas) for those Top-10 subsets.  
   - Ensured descending order via sorting + inverting y-axis.  
   - Used `matplotlib.ticker.PercentFormatter` to format axes (salary in `$K`, etc.).  
   - Time series line plot for selected skills showing monthly trend; annotated final values.  

---

## 📊 Key Findings (Sample Results)

| Skill              | Skill Count     | Median Salary        |
|---------------------|------------------|------------------------|
| `SQL`               | ~2,500           | \$180K (example)      |
| `Excel`             | ~2,200           | \$150K                |
| `Python`            | ~1,800           | \$170K                |

> *These numbers are illustrative based on the Top-10 charts.*  

- Skills like **SQL, Python, Excel, Tableau** appear both high in count *and* offer strong median salaries.  
- Some less popular skills with high salaries (e.g. specialized tools) show fewer postings but a big pay premium.  
- Time-series chart shows SQL was consistently hovering ~50-55% of postings, while Excel dipped then recovered; other skills like Tableau / Power BI had lower but noticeable presence.

---

## ⚙ Challenges & Solutions

- **Label overlapping in plots**  
  - Initially, skill labels overlapped when placed at the same x-position.  
  - Solved by adjusting label positions individually or using `order=` in seaborn + `invert_yaxis()` to preserve descending order.  

- **Huge `.ipynb` files / long git history**  
  - Handling large notebook diffs caused VS Code’s Git Timeline to load slowly.  
  - Kept repository clean and ignored unnecessary files; used `.gitignore` for large data / interim files.  

- **Import & formatting issues**  
  - Example: `PercentFormatter` must be imported from `matplotlib.ticker`, not from top-level `matplotlib`.  

---

## 🗣 How to Interpret This

- A **high median salary** doesn’t always mean many postings. Some rare skills pay well but aren't widely requested.  
- “Most in-demand” skills show what job descriptions most often list, important for resume / job prep.  
- Trends over time help anticipate what skills are rising / falling in demand.

---

## 🚀 How to Use / Next Steps

Feel free to clone / fork this repo and:

- Run notebooks to reproduce plots with updated data.  
- Add more skills (e.g. ML, Python libs) to see their trends.  
- Compare different geographies (Canada, UK, etc.).  
- Build a dashboard to interactively show skill vs salary vs demand.

---

## 📋 Dependencies

- Python 3.x  
- Pandas  
- NumPy  
- Seaborn  
- Matplotlib (Ticker formatters)  
- (Optional) `adjustText` for label placement

---


