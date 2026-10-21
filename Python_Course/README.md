# The Analysis

## 1. What skills are in demand for the top 3 most popular data roles?

I identified the most popular data roles based on the number of job advertisements. This allowed me to filter for the top 5 skills demanded for the top 3 data roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting.

View my notebook with detailed steps here:
[2_Skills_Demand.ipynb](3_Project\2_Skills_Demand.ipynb).

### Visualise the Data

```Python
#Set up the plot
fig, ax = plt.subplots(len(job_titles),1)

#For loop to create plot for each job_title item
for i, job_title in enumerate(job_titles):
    
    #Set the theme
    sns.set_theme(style='ticks')
    
    #Subset the data for our top 3 job titles and top 5 skills
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == job_title].head(5)
    
    #Plot using seaborn
    sns.barplot(data=df_plot, x='skill_perc', y='job_skills', ax=ax[i],         hue='skill_count', palette='dark:r_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlim(0,max(df_skill_perc['skill_perc'])*1.05)
    ax[i].set_xlabel('')
    ax[i].legend().set_visible(False)

    #Specify data labels
    for n, v in enumerate(df_plot['skill_perc']):
        ax[i].text(x=v+0.5, y=n, s=f'{v:.0f}%', va='center')
    
    #Set x axis for the 3rd plot only
    if i != 2:
        ax[i].set_xticks([])
    
#Set the figure title and global options
fig.suptitle('Likelihood of Skills Requested in UK Job Postings', fontsize=15)
fig.tight_layout()
plt.show()
```
### Results

![Visualisation of Top Skills for Data Jobs](3_Project/Figures/Skills_Demand.png)

### Insights

* SQL and Python are versatile skills which are in demand across Data Analyst, Data Engineer, and Data Scientist roles.
* SQL is the most requested skill amongst Data Analysts (43 %) and Data Engineers (60 %), respectively.
* Data Engineers and Data Scientists require more specialised technical skills (Azure, AWS, Spark) compared to data analysts who are expected to be more proficient in data management and analysts tools (Excel, Power BI, Tableau).
