---
layout: post
title: Saliford turn over analysis
image: "../img/distribution_of_monthly_hours_average.png"
tags: [Python, EDA, Machine learning]
---

- [00. Project summary](#overview-summary)
    - [Context](#overview-context)
    - [Process](#overview-process)
    - [Summary of EDA](#overview-eda)
    - [Buisness Takeaways](#overview-takeaway)
- [01. Presentation of the Model](#concept-model)
    - [Model Score](#overview-score)
    - [Model Results](#overview-results)
- [02. Chalenges and what I would do differently](#overview-chalenges)
- [03. Next step](#overview-next)
- [04. Folder Organisation](#overview-organisation)




# Project summary  <a name="overview-summary"></a>

## Context  <a name="overview-context"></a>

<br>

This project is a fictive analysis based on data provided by Kaggles.com, originating from the google career certificate for data analysis.

The mandate is to generate insight on the high turnover rate of Saliford Motor based on a company survey containing 11991 non-null, non-duplicated entries figuring 10 columns of data each. 

`The project resulted on valuable insights for the stakeholders to reflect upon as well as in a Tree based classification model with a prediction f1 score of about 94%.`

View full project: [Github link](https://github.com/Max0513/Turn-over-analysis---Saliford-)

<br>

*Notes*: 

- View data dictionary in references folder for more information on the different metrics used in the analysis.

- A folder structure template is also available at the end of this readme.

<br>

## Process  <a name="overview-process"></a>

An initial EDA using `python` revealed key insights as to where company leadership could further the investigation in hopes to reveal precise causes of departure.

A prediction model was then computed to help screen employees for potential risk of leaving Saliford, based on different metrics collected by the company.

<br>

## Summary of EDA  <a name="overview-eda"></a>

- Satisfaction is the greater influencer in the outcome variable.
- High work hours (Above 220 hours a month) increase the risk of departure.
- The promotion system of *Saliford* might contribute to higher turnover.
- 3 to 5 project count looks to be ideal for retention.
- Years 4 and 5 need further investigation over the satisfaction level decrease in the work force.

<br>

## Business takeaways   <a name="overview-takeaway"></a>

Data exploration revealed valuable insights about Saliford's work force:

<br>

*Following charts show how the **Monthly hours** worked by Saliford's employees relate to their **tenure**.*


 
  
![alt text](/img/posts/distribution_of_monthly_hours_average.png) ![alt text](/img/posts/monthly_hours_per_project.png)


<br>

>Insight 1 : Burn out looks to be a significant factor in departures

- Employees working outside of the `160 to 220 hours a month` range are at much higher risk of turnover, the average in the US being 176. A recommended maximum for monthly hours could be set to 220 hours to help this issue.

- 100% of workers assigned **7 projects** left the company, dropping to 45% when assigned 6.

- Regardless of number of projects assigned, departures seem to be correlated to the time required by those project rather than to the projects themselves.


<br>

>Insight 2 : three departments stand out from the rest and would require further investigation.

*The chart below shows **percent of departure** by departement.*

![alt text](/img/posts/departure_by_department.png)

<br>

>Insight 3 : The promotions system does not look ideal for retention.

- **98.3%** of workers `did not receive a promotion` in the last 5 years.
- Around `17% of employees who did not receive a promotion in the last 5 years departed`, dropping to 4% if they did.
- Implementing a structure with more echelon could be a consideration to add a sense of progression in the work force.
- The `number of promotions` do not appear related to the **number of hours worked**, **the number of project participated in** nor to the **last evaluation of the worker**. They do however, appear to be correlated to their **satisfaction levels**. *(View EDA for further details)*

<br>

>Insight 4 : Aiming for 3 to 5 projects per employee could help lower departures.


![alt text](/img/posts/table_departure_per_years.png)

- It is worth noting that as stated before, the **time spent working on project** seems a more likely indicator that the **number of project**.

- Increasing project number does however correlate to an increase in monthly hours worked.

<br>

>Insight 5 : Satisfaction levels are dipping in the four year category.

 **50%** of the company reports a **satisfaction level above 0.66** with **37% at or above 0.75** which is not bad but `levels drop around the 4 years mark`.

<p align="center">

 ![alt text](/img/posts/table_satisfaction_by_year.png) ![alt text](/img/posts/satisfaction_per_years_at_company.png)

</p>

- Regardless of departure, `satisfaction levels drop at the 4 years employment mark`.
- Satisfaction of departed personnel follows a downward trend until year 5 and then picks back up at year 5, suggesting that those that leave for satisfaction reasons might mostly do so by year 4. Suggesting departures in year 5 and 6 might be due to other reasons.

<br>

*Chart below shows **departures** tend to follow the trend in **satisfaction levels** drop. `Years 4 and 5 have the highest turnover rates`.*

![alt text](/img/posts/leave_per_years_at_company.png)

<br>

>Insight 6 : We can speculate on possible reasons for leaving using data from scatter chart.

*Scatter chart below shows 3 distinct areas of departures:*

![alt text](/img/posts/scatter_plot_satisfaction_vs_hours.png)

- *High work hours, low satisfaction*: Most likely left from **burn out**.
- *High work hours, high satisfaction*: Most likely left **for higher paid job**.
- *Low work hours, low satisfaction*: Most likely fired for **low performance**. 

<br>

# Presentation of the  model  <a name="overview-model"></a>

The chosen model is the `Tree based machine learning model`.

- The required task is **classification**.

- EDA revealed a fair proportion of relevant **outliers** so we need an outlier resilient model.

- Logistic regression fits requirements, but it seems the tree model could add valuable insights to stakeholder by studying the branches, it then seems like a good first choice in a world where making both and comparing would require too much time.

<br>

## Model score  <a name="overview-score"></a>


*A model with the following parameters and scores was selected for use, selecting the f1 score as the best predictor score.*

![alt text](/img/posts/model_results_table.png)

Using 3598 data point *(About 30% of the data)* as test_data, we could predict departure with an `f1 score of about 94%`.

<br>

*The following **Confusion matrix** show the repartition of the 3598 predicted data points*

![alt text](/img/posts/confusion_matrix.png)

- `Yellow` top/left box shows retained employees that where **correctly predicted** as such.
- `Light Purple` bottom/right box shows departed employees that were **correctly identified**.
- `Bright Purple` Boxes show **incorrectly identified** data. 

<br>

## Model results <a name="overview-results"></a>

In a tree based model, gini importance more or less refers to the degree to which the metric influences the classification of the model.

<br>

*The graph below shows metrics graphed by gini importance*.

![alt text](/img/posts/gini_importance.png)

- Once again we see another example of the effect of satisfaction level over the turn over rate.

<br>

# Challenges and what I would do differently <a name="overview-chalenges"></a>

- I had to figure out a clear organization method to present the project. I settled on the cookiecutter data template that I adapted to my needs
- I lost a day of work due to forgetting to commit progress, had to learn the hard way to always backup and update files.

<br>

# Next steps for the project <a name="overview-next"></a>

>Deploy the model on Streamlit for ease of access.

<br>

>Investigate the three areas from the scatter chart further .

- Investigate performance statistics for employees between 0.3 and 0.5 in satisfaction_levels that are also in the 125 to 175 average_montly_hours range to confirm hypothesis about possible layoff due to low performance.
- Investigate salary and promotion metrics for employees between 0.75 and 1 satisfaction_levels that also fit the 225 hours and more category to confirm hypothesis about the group leaving for a higher paid job due to lack of advancement.
- Run EDA over the new data frames created by the filtering of the three target zones to see if they behave differently.

<br>

>Construct a logistic regression model to compare for better prediction score with the tree model.

<br>

> Get access to higher quality data.

- Year since promotion would be better than promotion in last 5 years
- distinction between layoff and resignation.
- male / female category could had further insights to the EDA as well as shed light on possible discrimination in the present or future.
- age column is a relevant information to work with.
- distance from home could had valuable insights to the data.
- salary column could have a higher level of detail for more control, there is no way to know what a 'High' salary is currently.

<br>

> Generate dashboards for management to better track important metrics.

- Machine learning models can be a great tool, but it is an imperfect tool. Management must be equipped with good data visualisation tools to add human insight which is as much if not more valuable to solving problems.

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

