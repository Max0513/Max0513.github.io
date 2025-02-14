---
layout: post
title: Analysis of Work Force Turn Over Using Python
image: "../img/posts/distribution_of_monthly_hours_average.png"
tags: [Python, EDA, Machine learning]
---

Saliford Motors has noticed a high turnover rate from their work force. They ask for a machine learning algorithm that would help them screen for possible departures in their work force based on data they collected from past employees.

- [00. Project summary](#overview-summary)
    - [Context](#overview-context)
    - [Data](#overview-data)
    - [Executive Summary of EDA](#overview-eda)
- [01. Insight Deep Dive](#overview-dive)
- [02. Presentation of the Model](#overview-model)
    - [Model Score](#overview-score)
    - [Model Results](#overview-results)
- [03. Chalenges and what I would do differently](#overview-chalenges)
- [04. Folder Organisation](#overview-organisation)




# Project summary  <a name="overview-summary"></a>

## Context  <a name="overview-context"></a>

<br>

Saliford Motors has noticed a high turnover rate from their work force. They ask for a machine learning algorithm [ML] that would help them screen for possible departures in their work force based on data they collected from their employees, past and present. If succesful, the ML model could give Saliford an opportunity for action in preventing the departure before it takes place. 

An initial EDA using `python` revealed key insights as to where company leadership could further investigate to hopefully reveal the exact causes of departure.

A Tree Based Classification model with an f1 accuracy score of about 94% was then computed to help screen employees for potential risk of leaving Saliford, based on different metrics collected by the company.

<br>


Full GitHub Repository: [Github link](https://github.com/Max0513/Turn-over-analysis---Saliford-)

<br>


## Data  <a name="overview-data"></a>


<br>

## Executive Summary of EDA  <a name="overview-eda"></a>

- Satisfaction is the greater influencer in the outcome variable.
- High work hours (Above 220 hours a month) increase the risk of departure.
- The promotion system of *Saliford* might contribute to higher turnover.
- 3 to 5 project count looks to be ideal for retention.
- Years 4 and 5 need further investigation over the satisfaction level decrease in the work force.

<br>

# Insight Deep Dive   <a name="overview-executive"></a>

Data exploration revealed valuable insights about Saliford's work force:

<br>

*Following charts show how the **Monthly hours** worked by Saliford's employees relate to their **tenure**.*


 
  
![alt text](/img/posts/distribution_of_monthly_hours_average.png) 

<br>

![alt text](/img/posts/monthly_hours_per_project.png)


<br>

>Insight 1 : Burn out looks to be a significant factor in departures

- Employees working outside of the `160 to 220 hours a month` range are at much higher risk of turnover, the average in the US being 176 hours. A recommended maximum for monthly hours could be set to 220 hours to help this issue.

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
- Around `17% of employees who did not receive a promotion in the last 5 years departed`, dropping to 4% if they did.
- Implementing a structure with more echelon could add a sense of progression in the work force wich might boost moral and lead to lower turnover.
- The `number of promotions` do not appear related to the **number of hours worked**, **the number of project participated in** nor to the **last evaluation of the worker**. They do however, appear to be correlated to their **satisfaction levels**. 

<br>

>Insight 4 : Aiming for 3 to 5 projects per employee could help lower departures.

| **Project Number** | **Count_of_departure** | **Percent_of_departure** |
|---|---|---|
| 3 | 3520 | 1 % |
| 4 | 3685 | 6 % | 
| 5 | 2233 | 15 % | 
| 6 | 826 | 45 % | 
| 2 | 1582 | 54 % |
| 7 | 145 | 100 % |



It is worth noting that as stated before, the **time spent working on project** seems a more likely indicator than the **number of project**. It is a fact however, that a higher project count tends to lead to a greater time spent on those projects.


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

- `Yellow` top/left box shows retained employees that where **correctly predicted** as such.
- `Light Purple` bottom/right box shows departed employees that were **correctly identified**.
- `Bright Purple` Boxes show **incorrectly identified** data. 

<br>

## Model results <a name="overview-results"></a>

In a tree based model, gini impurity more or less refers to the probability of misclassifying an observation.

<br>

*The graph below shows metrics graphed by gini importance*.

![alt text](/img/posts/gini_importance.png)

The ML model also points to satisfaction levels as the first concern regarding prediction of turnovers. Investigating what exactly is affecting satisfaction levels should be viewed as a priority. 

<br>

# Challenges and what I would do differently <a name="overview-chalenges"></a>

<br>

>Investigate the three areas from the scatter chart further .

- Investigate performance statistics for employees between 0.3 and 0.5 in satisfaction_levels that are also in the 125 to 175 average_montly_hours range to confirm hypothesis about possible layoff due to low performance.
- Investigate salary and promotion metrics for employees between 0.75 and 1 satisfaction_levels that also fit the 225 hours and more category to confirm hypothesis about the group leaving for a higher paid job due to lack of advancement.
- Run EDA over the new dataframes created by the filtering of the three target zones to see if they tell a different story.

<br>

> Investigate for access to higher quality data.

- Year since promotion would be better than promotion in last 5 years.
- distinction between layoff and resignation in the left dimension would lead to cleaner insights.
- age is a relevant dimension that could had value to the analysis.
- distance from home could had valuable insights to the data and to the model.
- salary column could have a higher level of detail for more control, there is no way to know what a 'High' salary is currently.

<br>

>Investigate the three outlier departments, looking for a patern that could had to the story.
Segmenting the data by department and running a statistical analysis on dimensions such as average_montly_hours, staisfaction_levels or promotion_last_5_years might help figure out missing pieces of the puzzle.

<br>

> Generate dashboards for management to better track important metrics.

- Machine learning models can be a great tool, but it is an imperfect tool. Management must be equipped with good data visualisation tools to add human insight which is as much if not more valuable to solving business problems.

<br>

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

