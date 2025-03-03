---
layout: post
title: Analysis of Work Force Turn Over Using Python
image: "../img/posts/distribution_of_monthly_hours_average.png"
tags: [Python, EDA, Machine learning]
---

In this project, we analyse survey data to gather insights regarding the high emnployee turnover rate at Saliford Motors. We than construct a ML model to predict who is at risk of leaving.

- [00. Project summary](#overview-summary)
    - [Context](#overview-context)
    - [Action](#overview-action)
    - [Data](#overview-data)
    - [Executive Summary of EDA](#overview-eda)
- [01. Insight Deep Dive](#overview-dive)
- [02. Presentation of the Model](#overview-model)
    - [Model Score](#overview-score)
    - [Model Results](#overview-results)
- [03. Chalenges and what I would do differently](#overview-chalenges)
- [04. Folder Organisation](#overview-organisation)

<br>

<br>

___

# Project summary  <a name="overview-summary"></a>

## Context  <a name="overview-context"></a>

<br>

Saliford Motors, a global-wide car manifacturer of over 100 000 employees, distributed along multiple departments is looking for help regarding the results of a recent employee survey.

Currently, there is a high rate of turnover among Salifort employees. (Note: In this context, turnover data includes both employees who choose to quit their job and employees who are let go). Salifort’s senior leadership team is concerned about how many employees are leaving the company. Salifort strives to create a corporate culture that supports employee success and professional development. Further, the high turnover rate is costly in the financial sense. Salifort makes a big investment in recruiting, training, and upskilling its employees. 

Senior leadership suggests the design of a machine learning algorithm [ML] that would help them screen for possible departures based on data they collected from their employees, past and present. If succesful, the ML model could give Saliford an opportunity for action in preventing the departure before it even takes place. 

## Action  <a name="overview-action"></a>

<br>

To begin with, an initial EDA using `python` revealed key insights as to where company leadership could focus their attention to hopefully reveal the exact causes of the high turnovers that affects Saliford's culture and finances.

A Tree Based Classification model with an f1 accuracy score of about 94% was then computed to help screen employees for potential risk of leaving Saliford, based on different data collected in the company survey. The model also strengthened intuitions that where guided by the EDA over the key metrics that predict departures.

<br>


Full GitHub Repository: [Github link](https://github.com/Max0513/Turn-over-analysis---Saliford-)

<br>

## Data  <a name="overview-data"></a>

<br>


*The data contained 14999 entries of which 3008 rows where duplicates. Most ouliers present were found in the year_spent_company column (6.87% of values).* 
    
*Most relevant correlations found were between **number_project and average_montly_hours** and between **satisfaction_level and left**.*
    
*16.6% of data is categorised as **left** so the dataset is moderatly imbalanced.*
  
*EDA revealed no clear non-sensical data present.*

<br>

<br>

<br>

**satisfaction_level (int64)** : Self-reported satisfaction of employee

**last_evaluation (int64)** : Score of employee's last performance review

**number_project (int64)** : Number of projects contributed in the last year

**average_montly_hours (int64)** : Average worked hours per month in the last year

**time_spent_company (int64)** : Number of years employee has been working at Saliford Motors

**work_accident (int64)** : Whether employee has been involved in a work accident [1] or not [0]

**left (int64)** : Whether employee is still employed at Saliford [0] or has left [1]

**promotion_last_5years (int64)** : Whether employee got promoted in the last 5 years

**department (str)** : Employee's department

**salary (str)** : Whether employee's salary is considered 'high', 'medium' or 'low' based on undefined numbers

<br>

## Executive Summary of EDA  <a name="overview-eda"></a>

**Satisfaction is the greater influencer in the outcome variable.**

- Data analysis revealed -0.35 correlation score with the outcome variable. 'satisfaction_levels' is also the greatest contributer to the model's predictions.

<br>

**High work hours (Above 220 hours a month) increase the risk of departure.**

- 52% of turnovers occur over an average of 220 hours per month.

<br>

**The promotion system of *Saliford* might contribute to higher turnover.**

- 98.3% of workers did not receive a promotion in the last 5 years, which increased the probability of leaving from 4% to 17% in the analysed data.
- Promotions seem to mostly be attributed over the average monthly hours worked. Monthly hours worked are a contributor to high turnover rates.

<br>

**3 to 5 project count looks to be ideal for retention.**

- 45% of employees who took on 6 projects left the company going up to 100% when taking on 7 projects.
- The requiered time spent on the job seems to be the cause, rather than the count of project itself.  

<br>

**Years 4 and 5 since hired need further investigation over a massive drop in satisfaction level which seems a large predictor variable of leave**

- Satisfaction levels are steadily decreasing through year 4, down to an average of 14% of satisfaction in the departed employees category. 

- Retained employees tell a different story, decreasing to a minimum average of 48% at year 5 and then rising back up.

<br>

<br> 

___

# Insight Deep Dive   <a name="overview-dive"></a>

<br>

[ - Link to EDA Notebook - ](https://github.com/Max0513/Turn-over-analysis---Saliford-/blob/main/Notebooks/data_cleanup.ipynb)

<br>

Data exploration revealed valuable insights about Saliford's work force:

<br>

*Following charts show how the **Monthly hours** worked by Saliford's employees relate to their **tenure**.*



![alt text](/img/posts/distribution_of_monthly_hours_average.png)



<br>

![alt text](/img/posts/monthly_hours_per_project.png)


<br>

>Insight 1 : Burn out looks to be a significant factor in departures

- Employees working outside of `160 to 230 hours a month` are at much higher risk of turnover, the average in the US being 176 hours. A recommended maximum for monthly hours could be set to 220 hours to help this issue.

- 100% of workers assigned **7 projects** left the company, dropping to 45% when assigned 6.

- Regardless of number of projects assigned, departures seem to be correlated to the time required by those project rather than to the number of projects itself.


<br>

>Insight 2 : three departments stand out from the rest and would require further investigation.

<br>

*The chart below shows **percent of departure** by departement.*

![alt text](/img/posts/departure_by_department.png)

<br>

>Insight 3 : The promotions system does not look ideal for retention.

- **98.3%** of workers `did not receive a promotion` in the last 5 years.
- Approximatively `17% of employees who did not receive a promotion in the last 5 years departed`, dropping to 4% if they did.
- Implementing a structure with more echelon could add a sense of progression in the work force wich might boost moral and lead to lower turnover.
- The `number of promotions` do not appear related to the **number of hours worked**, **the number of project participated in** nor to the **last evaluation of the worker**. They do however, appear to be correlated to their **satisfaction levels**. 

<br>

>Insight 4 : Aiming for 3 to 5 projects per employee could help lower departures.

| **Project Number** | **Count_of_departure** | **Percent_of_departure** |
|---|---|---|
| 2 | 1582 | 54 % |
| 3 | 3520 | 1 % |
| 4 | 3685 | 6 % | 
| 5 | 2233 | 15 % | 
| 6 | 826 | 45 % | 
| 7 | 145 | 100 % |



It is worth noticing that as stated before, the **time spent working on project** seems a more likely indicator than the **number of project**. It is a fact however, that a higher project count tends to lead to a greater time spent on those projects.


<br>

>Insight 5 : Satisfaction levels are dipping in the four year category.

 **50%** of the company reports a **satisfaction level above 0.66** with **37% at or above 0.75** which is not bad but `levels drop around the 4 years mark`.

| **Years_at_Company** | **Average_Satisfaction** |
|---|---|
| 2 | 0.70 | 
| 3 | 0.65 | 
| 4 | 0.52 | 
| 5 | 0.58 | 
| 6 | 0.57 | 
| 7 | 0.64 | 
| 8 | 0.67 | 
| 10 | 0.66 | 

<br>

![alt text](/img/posts/satisfaction_per_years_at_company.png)



- Regardless of departure, `satisfaction levels drop at the 4 years employment mark`.
- Satisfaction of departed personnel follows a downward trend until year 5 and then picks back up at year 5, suggesting that those that leave for satisfaction reasons might mostly do so by year 4. It is possible departures in year 5 and 6 might be due to other reasons.

<br>

*Chart below shows **departures** tend to follow the trend in **satisfaction levels**. `Years 4 and 5 have the highest turnover rates`.*

![alt text](/img/posts/leave_per_years_at_company.png)

<br>

>Insight 6 : We can speculate on possible reasons for leaving using data from scatter chart.

<br>

*Scatter chart below shows 3 distinct areas of departures:*

![alt text](/img/posts/scatter_plot_satisfaction_vs_hours.png)

- *High work hours, low satisfaction*: Could correlate to **burn out**.
- *High work hours, high satisfaction*: Possible resignation **for a higher paid job**.
- *Low work hours, low satisfaction*: Could have been terminated for **low performance**. 

<br>

<br>

___

# Presentation of the  model  <a name="overview-model"></a>

The chosen model is the `Tree based machine learning model`.

- The required task is **classification**.

- EDA revealed a fair proportion of relevant **outliers** so an outlier resilient model would be ideal.

- Logistic regression fits requirements, but the tree model has higher interpretability and could add valuable insights to stakeholder by studying the branches, it then seems like a good first choice in a world where making both and comparing would require too much time. We can always go back and code a Regression model to compare for better accuracy.

<br>

## Model score  <a name="overview-score"></a>


*Through 5 fold Cross-Validation grid search, with f1 score as the chose scoring metrics, using 3598 data point *(About 30% of the data)* as test data, the chosen model has the following parameters and scores:*

![alt text](/img/posts/model_results_table.png)

98% **Accuracy**: Represents the number of correct predictions out of the total number of predictions.

97% **Precision**: Tells us that out of the predicted departures, 97% were correct.

92% **Recall**: Tells us that out of the actual departures, 92% were correctly identified.

94% **F1**: is the harmonic mean of precision and recall, giving us a well balanced metric for imbalanced classifications.

<br>

*The following **Confusion matrix** show the repartition of the 3598 predicted data points*

![alt text](/img/posts/confusion_matrix.png)

- `Yellow` top/left box shows retained employees who where **correctly predicted** as such.
- `Light Purple` bottom/right box shows departed employees who were **correctly identified**.
- `Bright Purple` Boxes show **incorrectly identified** data. 

<br>

## Model results <a name="overview-results"></a>

In a tree based model, gini impurity represents to the probability of misclassifying an observation. From it, we can calculate a metrics known as gini importance more or less refers to the impact of the feature in the final classification of the model.

<br>

*The graph below shows metrics graphed by gini importance*.

![alt text](/img/posts/gini_importance.png)

The ML model also points to satisfaction levels as the first concern regarding prediction of turnovers. Investigating what exactly is affecting satisfaction levels should be viewed as a priority. 

<br>

<br>

___

# Challenges and what I would do differently <a name="overview-chalenges"></a>

<br>

>Investigate the three areas from the scatter chart further .

- Investigate performance statistics for employees between 0.3 and 0.5 in satisfaction_levels that are also in the 125 to 175 average_montly_hours range to confirm hypothesis about possible layoff due to low performance.
- Investigate salary and promotion metrics for employees between 0.75 and 1 satisfaction_levels that also fit the 225 hours and more category to confirm hypothesis about the group leaving for a higher paid job due to lack of advancement.
- Run EDA over the new dataframes created by the filtering of the three target zones to see if they tell a different story.

<br>

> Investigate for access to higher quality data.

- Year since promotion would be better than promotion in last 5 years.
- distinction between layoff and resignation in the outcome variable would lead to cleaner insights.
- age is a relevant dimension that could had value to the analysis.
- distance from home could had valuable insights to the data and to the model.
- salary column could have a higher level of detail for more control, there is no way to know what a 'High' salary is currently.

<br>

>Investigate the three outlier departments, looking for a patern that could had to the story.

Segmenting the data by department and running a statistical analysis on metrics such as average_montly_hours, staisfaction_levels or promotion_last_5_years might help figure out missing pieces of the puzzle.

<br>


<br>

___

# Folder Organization <a name="overview-organisation"></a>


├── LICENSE            <- Open-source license if one is chosen

├── README.md          <- The top-level README for developers using this project

├── data

│   ├── interim        <- Intermediate data that has been transformed

│   └── raw            <- The original, immutable data dump

│

├── models             <- Trained and serialized models, model predictions, or model summaries

│

├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),

│                         the creator's initials, and a short '-' delimited description, e.g.

│                         '1.0-jqp-initial-data-exploration'

│

├── references         <- Data dictionary

│

└─ reports            <- Generated analysis as HTML, PDF, LaTeX, etc.

  └── figures        <- Generated graphics and figures to be used in reporting

