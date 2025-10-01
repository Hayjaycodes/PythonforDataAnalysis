# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which one were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the mopst poluar job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting

View my notebook with detailed steps here:
[3_Skills_Demand.ipynb](3_Project\3_Skills_Demand.ipynb)

### Visualize Data

```python

fig, ax=plt.subplots(len(job_titles),1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    # df_plot.plot(kind='barh', x='job_skills', y='skill_percent', ax=ax[i], title= job_title)
    sns.set_theme(style="ticks")
    sns.barplot(data=df_plot, y='job_skills', x='skill_percent', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 78) #set x limit for better comparison

    for n, v in enumerate(df_plot['skill_percent']):
       ax[i].text(v + 1, n, f'{v:.0f}%', va='center')
       if i != len(job_titles) - 1:  # Remove x-ticks for all but the last subplot
        ax[i].set_xticks([])

    fig.suptitle('Likelihood of Skills Requested in UK Jobs Posting', fontsize=15)
    fig.tight_layout(h_pad=0.5) #fix the overlap

```

### Results

![Visualization of Top Skills for Data Savvy](3_Project\images\job_skills_demands_for_data_roles.png)

### Insights

- Python is a versatile skill, highly demanded across all three roles, butt most prominently for Data Scientist (69% )and Data Engineers(55%).
- SQL is the most requested skill for Data Analyst and Data Engineer, with it 43% and 60% respectively. For Data Scientist, Python is the most sought- after skill, appearing in 69% of job postings.
- Data Engineers and Data Scientist require more specialized technical skills(AWS and spark) compared to Data Analyst

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))



plt.show()

```

## Result

![Trending Top Skills for Data Analysts in the UK](3_Project\images\Trnding_skills_demand.png)
_Bar graph visualizing the trending top skills for data analysts in the UK in 2023._

## Insights:

- Alteryx is the most in-demand skill, with demand rising sharply towards the end of the year.
- Airflow shows consistent moderate demand, peaking mid-year before stabilising.
- Airtable and Asana trend lower, but appear sporadically, reflecting niche adoption.
- Assembly shows minimal demand, with almost no presence across the year.
- Overall demand dips in August but trends upwards from September to December, showing strong year-end hiring activity.

### 3. How well do jobs and skills pay for Data Analysts?

## Salary Analysis for Data Lovers

### Visualize Data

```python
sns.boxplot(data=df_uk_top6, x='salary_year_avg', y='job_title_short', order= job_order)

sns.set_theme(style = 'ticks')


plt.title('Salary Distribution in the UK')
plt.xlabel('Salary (Yearly)')
plt.ylabel('')
plt.xlim(0, 600_000)
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```

### Results

![Salary Distributions of Data Jobs in the UK](3_Project\images\pay.png)

_Box plot visualizing the salary distributioms for the top 6 data job titles_

### Insights

- Data Analysts earn the lowest among the listed roles, with salaries typically ranging between £40K–£90K and a median around £60K–£70K.
- Senior Data Analysts see a noticeable salary increase, with a median around £90K–£110K and potential earnings up to £150K, though this still lags behind Data Scientists and Engineers.
- Data Scientists and Data Engineers consistently command higher salaries, highlighting that advanced technical skills (e.g., machine learning, big data, cloud computing) are more highly rewarded.
- Outliers exist for Senior Data Analysts, with some reaching salaries above £120K, but these cases are less common compared to other senior data roles.

### Highest Paid & Most Demanded Skills for Data Analysts

### Visualize Data

```python
fig, ax =plt.subplots( 2, 1)
sns.set_theme(style= 'ticks')

#Top 10 highest paying skills for Data Analysts

sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue ='median', ax = ax[0], palette='dark:b_r')
ax[0].legend().remove()

ax[0].set_title('Top 10 Highest Paying Skills for Data Analysts')
ax[0].set_xlabel('')
ax[0].set_ylabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

# Top 10 most in-demand skills for Data Analysts
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue = 'median', ax = ax[1], palette='light:b')
ax[1].legend().remove()

ax[1].set_title('Top 10 Most In-Demand Skills for Data Analysts')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary (USD)')
ax[1].set_xlim(ax[0].get_xlim()) # Set x-axis limits to be the same as the first plot
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))
plt.tight_layout()
plt.show()


```

## Results

In-demand skills for data analysts in the UK:

![Highest Paid and Most In demand Skills for Data Analyst in the US.png](3_Project\images\compare.png)

_Two seperate bar graphs visualizing the highest paid skills and most in-demand skills for data analyst in the UK_

## Insights

- Highest-Paid (top → bottom): pandas, TensorFlow, NumPy, C++, PyTorch, Aurora, MongoDB, MySQL, AWS, Elasticsearch.
- Most In-Demand (top → bottom): Tableau, SQL, Looker, Python, Power BI, SAS, R, Excel, Go, Outlook.
