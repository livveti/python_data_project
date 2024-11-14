 Overview

# The Analysis

## 1. What are the key skills for the top 3 trending data roles?

Click here to View my notebook with detailed steps:
[2_Skill_Demand.ipynb](3_Project/2_Skill_Demand.ipynb)

### Visualizing Data
```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, title in enumerate(job_titles):
    df_plot = df_skills_count[df_skills_count['job_title_short'] == title].head(5)
    df_plot[::-1].plot(kind='barh', x='job_skills', y='skill_count', ax=ax[i], title=title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)
    
fig.suptitle('Count of Top Skills in Top trending Roles', fontsize=15)
fig.tight_layout()
plt.show()
```
### Results

![Visualization of Top Skills for Top Data Roles](3_Project/Images/skill_demand_top3_data_roles.png)

### Takeaways

## 2. How are the top skills trending for Data Analysts in the US?

```python
from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    y_position = df_us_da_plot.iloc[-1, i]
    
    if df_us_da_plot.columns[i] == 'python':
        y_position += 2
    elif df_us_da_plot.columns[i] == 'tableau':
        y_position -= 2 
    
    plt.text(
        11.2, y_position, 
        df_us_da_plot.columns[i], 
        va='center', 
        ha='left'
    )

```
### Results
![Visualiztion of Top Skills Trend for Data Analyst in the US](3_Project/Images/us_data_analysts_top_skills_trend.png)
*Line graph visualizes the trending top skills for data analysts in the US in 2023.*

### Takeaways

## 3. How Well do jobs and salary pay for Data Analysis?

#### Visualize Data

```python
sns.barplot(data=df_da_top_pay, x='median', y=df_da_top_pay.index, ax=ax[0], hue='median', palette='dark:salmon_r')

sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()

```

#### Results

![Salary Distributions for Data Jobs in the US](3_Project/Images/top_6_roles_salary_scatter.png)
*Box Plot visualizes the distributions of salary for the top 6 data job titles*

### Takeaways

## Analyzing Top-Paying Skills & Most Demanded Skills


#### Visualize Data

```python
sns.boxplot(data=df_us_top6, x='salary_year_avg', y='job_title_short', order = job_order_list)
plt.title('Salary Distribution in the United Stats')
plt.xlabel('Yearly Salary ($USD)')
plt.ylabel('')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))
plt.xlim(0, 600000)
plt.show()
```

#### Results

![Top Paid Skills Vs, Top Demand Skills](3_Project/Images/top_pay_vs_top_demand.png)
*Box Plot visualizes the distributions of salary for the top paid skills and top demanded skills*

### Takeaways

## 4. What is the most Optimal skill to learn for Data Analyst?

#### Visualize Data

```python
from adjustText import adjust_text
from matplotlib.ticker import PercentFormatter
sns.scatterplot(
    data=df_plot, 
    x='skill_percent',
    y='median_salary',
    hue='technology'
)
plt.show()

```

#### Results

![Optimal Skills to Learn for Data Analysts in the US](3_Project/Images/optimal_skills_scatter.png)
*Scatter Plot visualizes the most optimal skills for data analysts in the US*

### Takeaways