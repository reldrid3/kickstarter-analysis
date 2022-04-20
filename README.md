# Kickstarting with Excel

## Overview of Project

Louise Smith had a recent Kickstarter project for her play Fever reach its goal very quickly, and she tasked me with an analysis of a large dataset of Kickstarter projects - comparing how they fared and mining the dataset for potential correlations to assist in her plans for future Kickstarter initiatives.

### Purpose

In this analysis, we will be focusing in on the Theater and Plays category and subcategory, respectively, and how different variables may or may not affect a successful Kickstarter within this topic.  Two of the most important variables for setting up a Kickstarter are when (what year, which part of the year, etc.) and the Goal to complete the Kickstarter.

#### Plausible Queries

- Does starting the Kickstarter at a particular time of year make it more likely to succeed?
- Does having a small goal or a large goal make it more likely for the Kickstarter to succeed?

## Analysis and Challenges

### Analysis of Theater Outcomes Based on Launch Date

In order to visualize the outcomes within the Theater category, I created a pivot table pitting the outcomes (successful, failed, canceled) against the month in which they were created.  This table was able to be filtered by Parent Category and by Year.  This was followed by generating a line graph, which is displayed as Figure 1.

#### Figure 1
![This is a graph of the outcomes (successful, failed, and canceled) of all Kickstarter projects in the Theater category, correlated with the month in which they were launched.](/Resources/Theater_Outcomes_vs_Launch.png)

### Analysis of Outcomes Based on Goals

In order to visualize the outcomes of the Plays subcategory as a function of their set goal amount, I created a new sheet with a set of goal ranges.  Using Excel's COUNTIFS() function as an AND-connected conditional statement, I was able to count all the kickstarters greater than a certain amount, then subtracted the sum of the previous ranges to find the main range.

Sample COUNTIFS() call:
```
=COUNTIFS(Kickstarter!$D:$D,"<"&$B2,Kickstarter!$F:$F,"successful",Kickstarter!$R:$R,$K$2)
```

#### Figure 2
![This is a graph of the outcomes (successful, failed, and canceled) of all Kickstarter projects in the Plays subcategory, correlated with their set goal, sorted into ranges of mostly $5000 increments.](/Resources/Outcomes_vs_Goals.png)

### Challenges and Difficulties Encountered

None of this analysis was particularly challenging, but I do want to explicitly explain some of the features I generated in the initial worksheet.

#### Feature Generation

##### Parent Category and Subcategory

- Initially, only a combined category contained the data for the parent and subcategories.  The Text to Columns Wizard was able to separate these into two columns (Q and R), using '\' as a delimiter.

##### Date Generation

- Both the Launch Date and Deadlines were stored as Unix timestamps, measured in seconds.  The following formula allowed me to convert the timestamp to a readable Date.
```
=(((J2/60)/60)/24)+DATE(1970,1,1)
```
- Excel's Year() function, when applied to this date, allowed the creation of a column with only the year, rather than the entire date.

## Results
Two conclusions are made about the Theater Outcomes by Launch Date (2 pt).
One conclusion is made about the Outcomes based on Goals (2 pt).
There is a summary of the limitations of the dataset, and there is a recommendation for additional tables or graphs (2 pt).

- What are two conclusions you can draw about the Outcomes based on Launch Date?

- What can you conclude about the Outcomes based on Goals?

- What are some limitations of this dataset?

- What are some other possible tables and/or graphs that we could create?
