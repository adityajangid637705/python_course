# The Analysis

# 1. What are the most demanded skills for the the top most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:[2_Skill_Demand.ipynb](3_Project/2_Skill_Demand.ipynb)

### Visualize Data

``` python
fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```
### Result

![Visualization of the Top Skills for Data Nerds](3_Project\images\output.png)

### Insights

- Data Engineers require a diverse tech stack, including cloud platforms (AWS, Azure) and big data tools (Spark), making their skill set more infrastructure-focused than other roles.

- Business intelligence tools (Excel, Tableau) are more relevant for Data Analysts, highlighting their role in reporting and visualization rather than deep modeling.

- Data Science emphasizes Python over SQL, showing a stronger focus on machine learning, statistical computing, and automation, whereas SQL is more crucial for Analysts and Engineers.

# The Analysis

# 2. How are in-demnad skills trending for Data Analysis?

To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.


View my notebook with detailed steps here:
[3_Skills_Trend.ipynb](3_Project/3_Skills_Trend.ipynb)

### Visualise Data

```python

from matplotlib.ticker import PercentFormatter

df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

```
### Results

![Trending Top Skills For Data Analysis in the US](3_Project\images\Trend.png)
*Bar graph visualizating the trending top skills for data analysis in the US in 2023.*

### Insights

- SQL Dominates: SQL remained the most in-demand skill throughout 2023, with a slight decline toward the end of the year. This highlights its continued importance for Data Analysts.

- Excel's Late Surge: Excel maintained steady demand but saw a noticeable dip in the latter half of the year, followed by a strong resurgence in December, suggesting renewed interest in spreadsheet-based analytics.

- Fluctuating Demand for Other Skills: Tableau and SAS had fluctuating trends, with Tableau peaking mid-year and SAS showing a slight increase in December. This suggests that specialized visualization and statistical tools may be more niche but still valuable.

# The Analysis

# 3. How well do jobs and skills pay for Data Analysts?

To identify the highest-paying roles and skills, I only got jobs in the United States and looked at their median salary. But first I looked at the salary distributions of common data jobs like Data Scientist, Data Engineer, and Data Analyst, to get an idea of which jobs are paid the most.

View my notebook with detailed steps here:[4_Salary_Analysis.ipynb](3_Project/4_Salary_Analysis.ipynb)

### Visualize Data

``` python

sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```

### Results

![Salary Distribution in United States](3_Project\images\Distribution.png)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

### Insights

- Higher Salaries for Senior Roles: Senior Data Scientists and Senior Data Engineers have significantly higher median salaries than their junior counterparts, showing that experience leads to substantial pay growth.

- Data Science Pays More: Data Scientists and Senior Data Scientists generally earn more than Data Engineers and Data Analysts, suggesting that advanced machine learning and AI expertise are highly valued.

- Wide Salary Ranges with Outliers: Each role has a broad salary range with multiple high-end outliers, especially in senior roles, indicating that factors like location, industry, and company size heavily influence earnings.

# Highest Paid & Most Demanded Skills for Data Analysts

Next, I narrowed my analysis and focused only on data analyst roles. I looked at the highest-paid skills and the most in-demand skills. I used two bar charts to showcase these.

### Visualize Data

```python 

fig, ax = plt.subplots(2, 1)  

sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()

```

### Results

### Here's the breakdown of the highest-paid & most in-demand skills for data analysts in the US:

![Top 10 Highest Paid Skills for Data Analysis](3_Project\images\Top.png)
*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*

# The Analysis

# 4. What are the most optimal skills to learn for Data Analysts?

To identify the most optimal skills to learn ( the ones that are the highest paid and highest in demand) I calculated the percent of skill demand and the median salary of these skills. To easily identify which are the most optimal skills to learn.

View my notebook with detailed steps here:[5_Optimal_Skills.ipynb](3_Project/5_Optimal_Skills.ipynb)

### Visualize Data

``` python

from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()

```
### Results

![Most Optimal Skills for Data Analyst](3_Project\images\scatter.png)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US.*

### Insights

- SQL is the Most In-Demand Skill: With the highest percentage of job postings (~60%), SQL is a must-have skill for data analysts, even though it doesn’t command the highest median salary.

- Python Leads in Salary Potential: Python offers the highest median salary (~$98K), making it a lucrative skill for data analysts despite being required in fewer jobs compared to SQL.

- Business Tools vs. Technical Skills: Tools like Excel and PowerPoint are more frequently required but have lower salaries, whereas technical skills like Oracle, SQL Server, and Tableau offer better salary prospects.

# Visualizing Different Techonologies

Let's visualize the different technologies as well in the graph. We'll add color labels based on the technology (e.g., {Programming: Python})

### Visualize Data

``` python

from matplotlib.ticker import PercentFormatter

# Create a scatter plot
scatter = sns.scatterplot(
    data=df_DA_skills_tech_high_demand,
    x='skill_percent',
    y='median_salary',
    hue='technology',  # Color by technology
    palette='bright',  # Use a bright palette for distinct colors
    legend='full'  # Ensure the legend is shown
)
plt.show()

```

### Results

![Most Optimal Skills for Data Analyst](3_Project\images\scatter.2.png)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US with color labels for technology.*

### Insights

- SQL and Python Dominate in Demand and Salary:

   - SQL is the most in-demand skill, appearing in nearly 60% of data analyst job postings.
   - Python, while less common, offers the highest median salary (~$98K), indicating its value in advanced analytics, automation, and data science applications.

- Cloud and Database Skills Yield Higher Salaries:

   - Technologies like Oracle (cloud) and SQL Server (databases) command strong median salaries (~$96K–$92K).
   - This suggests that expertise in managing and optimizing data storage systems is highly valued.

- Business Intelligence Tools Are Widely Used but Lower-Paying:

   - Skills like Excel, PowerPoint, and Word appear frequently  ($82K–$86K).
   - While essential for reporting and visualization, these tools alone do not offer the salary advantages of technical skills like Python and databases.

#  What I Learned

- Throughout this project, I deepened my understanding of the data analyst job market and enhanced my technical skills in Python, especially in data manipulation and visualization. Here are a few specific things I learned:

- Advanced Python Usage: Utilizing libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization, and other libraries helped me perform complex data analysis tasks more efficiently.
Data Cleaning Importance: I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.

- Strategic Skill Analysis: The project emphasized the importance of aligning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry.

# Challenges I Faced

This project was not without its challenges, but it provided good learning opportunities:

- Data Inconsistencies: Handling missing or inconsistent data entries requires careful consideration and thorough data-cleaning techniques to ensure the integrity of the analysis.

- Complex Data Visualization: Designing effective visual representations of complex datasets was challenging but critical for conveying insights clearly and compellingly.

- Balancing Breadth and Depth: Deciding how deeply to dive into each analysis while maintaining a broad overview of the data landscape required constant balancing to ensure comprehensive coverage without getting lost in details.

# Conclusion

This exploration into the data analyst job market has been incredibly informative, highlighting the critical skills and trends that shape this evolving field. The insights I got enhance my understanding and provide actionable guidance for anyone looking to advance their career in data analytics. As the market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a good foundation for future explorations and underscores the importance of continuous learning and adaptation in the data field.