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

After counting the data, a line graph with the results was created, as shown in Figure 2.

#### Figure 2
![This is a graph of the outcomes (successful, failed, and canceled) of all Kickstarter projects in the Plays subcategory, correlated with their set goal, sorted into ranges of mostly $5000 increments.](/Resources/Outcomes_vs_Goals.png)

### Challenges and Difficulties Encountered

None of this analysis was particularly challenging, but I do want to explicitly explain some of the features I generated in the initial worksheet, which may pose a challenge to some.

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

### Conclusions

#### Theater Outcomes by Launch Date

- The month with the most successes was May.  This implies that people may be more likely to fund Kickstarters in late Spring and early Summer.  As summer goes on, there is a clear downward trend in the number of successes.
- Those months also had some of the higher number of failures - there are also more Kickstarters created from May through August.  Of those, **May** is definitely an ideal month.
- If you are looking for a winter launch date, **February** had a clear spike in successful Kickstarters, and may be ideal for a non-summer Kickstarter.

#### Outcomes Based on Goals

- The only goal ranges with more successes than failures are $0->$15,000 and $35,000->$45,000.  All others had more failures than successes, and it may be prudent to avoid those amounts.
- Of those ranges, $5,000->$15,000 was rather close, so ideal ranges would be from $0->$5,000 and $35,000-$40,000.
- This suggests that there are two potential budgets for projects.  For a small project, try to keep the goal less than $5,000, while a larger project may want a goal near $40,000.

### Limitations and Additional Exploration

Some of the limitations of this dataset include a lot of missing data that may be relevant to predict the outcome of a Kickstarter.  Some examples of this would include:
- The professional presentation and production value of the Kickstarter.
- How often were there updates on the project?
- Was it the first project from a producer, or do they have a following?

Other exploration we could do with the data we currently have includes:
- More statistical analysis.  Instead of comparing # of successes vs failures, perhaps a ratio might be more prudent.
- Analysis whether something was a Staff Pick or under a Spotlight, which may have increased interest and chance of success (data we already have).
- Charting the outcomes vs. the number of backers - finding out if successes are more correlated with many donors or a few large donors may change the methods of advertising and targeting for the show.
