---
title: "Second Midterm"
output: 
  html_document: 
    keep_md: yes
---

Due by 11:59 pm on Sunday, Nov. 24th.

### Overview

You will be submitting three items: [1] a README.md and [2] an R Markdown/Markdown report through GitHub, and [3] a reflection on Bb.
This is essentially a take-home exam, so you should no discuss this with anyone except your professor.
You are allowed (and expected, if necessary) to use appropriate online resources.
Be sure to cite any resource that you get help from and explain where/how you implemented it - this is part of your [reflection](#3-reflection).
You are also free to ask questions/clarifications of me as if I am the client, but I have no experience with R or GitHub.
*If you are unsure about any of the regression concepts, you can certainly ask.*

The focus of this project is programming, modeling, and communicating, though you are welcome to use anything done throughout this semester or that you find online.
All non-textbook based resources must be cited.
You must also explain how you implemented these resources (either in your narrative or your reflection).

You should start this **as early as possible** to ensure that you have time to walk away when things are not working to provide you with an opportunity to refocus with fresh eyes.
If things are not working, try starting with smaller chunks and make sure the results are doing what you think you told R to do.

Your final report should interweave code, output, and narrative.
You should not do any data manipulations manually.
The goal is to demonstrate that you can tackle all tasks with R coding, unless otherwise approved by your professor.

#### Evaluation

Your midterm project report will be evaluated using the [Midterm and Team Project Grading Standards](https://sta518.github.io/syllabus/assessment/#midterm-and-team-projects).
Your README and reflection will be evaluated using the [Meeting Preparation Grading Standards](https://sta518.github.io/syllabus/assessment/#meeting-preparation-1)
If either of your README or reflection earns an Unsatisfactory (U), your overall mark will be lowered one mark.

### Create Your `second-midterm` Repo

GitHub Classroom will automatically make a repository for you, called `second-midterm-your_github_username`, for you to work on your assignment.
Follow these instructions to get the repo:

1. Sign-in to [Bb](https://mybb.gvsu.edu)
2. Go to the **Second Midterm** assignment page.

Here, you will find a url leading to a page on GitHub Classroom.
Visit this page and follow the instructions.
When you obtain your repository, it should contain a copy of this `second-midterm-instructions.md` file, a blank `README.md` file, a starter `second-midterm.Rmd` file, and a `data` folder containing one csv file: `allendale-students.csv`.

#### 1. Edit `README.md` 

Your task here is to edit the `README.md` file in your repository to contain a sample of GitHub-flavored markdown features.
Specifically, your README should contain a brief description as to what the repo is, so that an unknown visitor landing on the repo can orient themselves.
You should also help the visitor navigate your repository (in whatever way you think is most appropriate).

Remember the resources you were directed to view during your work in the class activities and Meeting Preparations.
These are also organized in the [Additional Resources/Markdown](https://sta518.github.io/resources/markdown/) section of this site.

You can edit the README in your browser like we did in class, but I encourage you to experiment with editing it from within RStudio.
**FYI, this will be a private repo - only you and I will be able to see it.**

#### 2. Midterm Report

Efficient or "elegant" coding will result in higher marks than inefficient coding.
There is more than one way to accomplish these tasks and you should try to pick a more efficient way, when possible.
Higher marks will also be reserved for successful implementation of the `tidyverse` whenever possible.
Efficient code that accomplishes the tasks will be considered *satisfactory*, regardless of your use of the `tidyverse`.

While I have not enforced the notion of comments, you should embrace using them in this midterm project.
See Hadley's statements on comments in R for [general syntax](https://style.tidyverse.org/syntax.html#comments) and [functions](https://style.tidyverse.org/functions.html#comments-1).

Knit your completed `.Rmd` file and commit your **entire** project folder from RStudio Cloud to GitHub.

##### Data

The `allendale-students.csv` data is contained within the `data` folder of this repo.
These data are a random sample from the population of recent GVSU graduates that lived in Allendale during their time at GVSU and all had cars during their time at GVSU.
The population is further restrict to students that had at most 50% of their total college cost paid by parents.
The variable `Debt` is the response variable and all other variables are explanatory.

| Variable | Description |
|:---------|:------------|
|Distance |	Distance (in miles) from hometown to Allendale |
|Scholarship |	Financial support (in dollars) from scholarships (average per year) |
|Parents |	Percent of total cost of bachelor’s degree paid by parents (max of 50%) |
|Car |	Age of car (in years) |
|Housing |	Type of housing (on campus, off campus). *Treat “off campus” as the reference group* |
|Major |	STEM (Science, Technology, Engineering, Math), business, other. *Treat “other” as the reference group* |
|Debt |	Student debt (in dollars) accumulated by end of bachelor’s degree. *This is the response variable* |

You can assume that the data are *clean* (yay!).

##### Tasks

The specific tasks required of you for this project are described below.
They are numbered here for clarity, but your final report should not contain numbering.

###### Task 1

Create appropriate exploratory visualizations of the response variable against each explanatory variable.
Note any interesting or troublesome features.
If any transformation of the response variable is needed, this is where you should implement it.
If you implement a transformation, graphically and descriptively confirm that it was reasonably successful.

###### Task 2

Manually create indicator variables for all categorical explanatory variables.
You will use these indicator variables, in place of the original categorical explanatory variables, for the rest of this project.
*Be sure to use the reference group listed in the description of the data when creating these indicator variables.*
Also, give an explanation of how you created these indicator variables, and why you had the particular number of them that you did, as if explaining to one of your classmates.

Further, for the categorical explanatory variable with more than two categories (i.e., major), you will consider each of the corresponding individual indicator variables to operate on its own when writing your function in the next portion.
Some argue that, if a categorical variable has more than two categories, you should keep or drop all associated indicator variables as a group, but we will not worry about that in this project.
*If you do not understand this clarification, be sure to ask (as always).*

###### Task 3

Write a function to implement the *best subsets* approach to model selection.
Unlike step-wise model selection approaches (e.g., forwards selection), best subsets fits all possible models based on the explanatory variables that you specify.

Your function should 1) allow for any number of explanatory variables, which, in this project, includes all indicator variables (but none of the original categorical variables - because they were replaced by the indicator variables), 2) fit a linear model, 3) track each model's r-square ($R^2$) as the criterion used to pick the best model.
When writing your function, you many assume that the data will always have columns in the order $X_1$, $X_2$, $\ldots$, $X_p$, $Y$ (where there are $p$ explanatory variables and $Y$ is the response), and that the data are always clean.
The only input to the function should be the data set

This function will create (but not output) a tibble with a *single* column for the: model number, subset of of explanatory variables along with response variable, model formula, outcome of fitting linear model, and others as needed.
See the table below for further clarification.
This will feel similar to the `gapminder` example in Chapter 20 of R4DS, but you are not collapsing rows with nest() as the text does.

These must be created by your function.
Do not manually type any of these into your tibble.

| Model number | Subset of explanatory variables, along with response variable (all rows from original data need to be included) | Model formula | Outcome of fitting linear model |
|:----------------|:-----------------|:-----------------------|:---------------------------|
| 1 | Y, X1 (n rows by 2 columns) | Y \~ X1 | Slope for X1, y-int, r-square, etc. |
| 2 | Y, X2 (n rows by 2 columns) | Y \~ X2 | Slope for X2, y-int, r-square, etc. |
| 3 | Y, X1, X3 (n rows by 2 columns) | Y \~ X1 + X2 | Slope for X1 and X2, y-int, r-square, etc. |
| ... | ... | ... | ... |

Your function should not output all of the above, but should output the following for every model: 1) the model number, 2) the explanatory variables in the model, 3) the value of r-square ($R^2$) for that model, 4) a graph with the r-square ($R^2$) value on the vertical axis vs. the number of explanatory variables in the model on the horizontal axis.
On the graph, you should label (with the model number) the point that has the highest value of r-square ($R^2$) for each number of explanatory variables in the model.

Be sure to write a brief summary of your function that a classmate would understand.
[Task 4](#task-4) details how you will analyze the data.

Some help:

- If you have $p$ explanatory variables, there are $2^p - 1$ possible models (subsets of explanatory variables).
  We subtract 1 because $2^p$ would include the model with no explanatory variables.
  There is an R function (`rje::powerSets`) that you may find useful.
- If you use `colnames()` to extract the variable names from the second column of the above table (for each model number), you will want your function to convert that into a model formula (for each model number).
  If you go this route, research "creating a formula from a string".
- You may want to create a simpler data set with, for example, three x variables and one y variable to experiment with, in order to determine the syntax you need.
- If you cannot write a function to automatically (within the function) accomplish all of the above, then do as much of it within the function as you can, and you can do the rest "manually" (without using a function).
  This would obviously result in a lower assessment.
  If you go this route, clearly explain what you were able to do within the function and what you had to accomplish manually.

###### Task 4

Choose the best model for the `allendale-students.csv` data set based on r-square ($R^2$) *by applying your function from [Task 3](#task-3)*.
That is, you want to balance having higher values of r-square ($R^2$) against having an unnecessarily complicated model.
Do not pick a model that is more complicated if there is not "significant" gain in r-square ($R^2$), relative to simpler models.
You can decide what a "significant" gain is, but you should clearly explain what that is and how you implemented it.
Be sure to write the equation of your final model using the variable names (not numbers).

###### Task 5

Examine the residuals from the best model you chose in [Task 4](#task-4).
Note any interesting or troublesome features.
We are not worried about normality of residuals, because we did not do any statistical inference.
However, outliers, constant variance (homoscedasticity), non-random patterns, etc. are all appropriate to look for.

###### Task 6

For the explanatory variables `scholarship`, `parents`, and `housing`, fit a model that also contains (two-way) interaction terms for `housing` and `scholarship`, and for `scholarship` and `parents`.
Interpret the slopes of these two interaction terms in context.
Also, examine the residuals of this model and note any interesting or troublesome features.

#### 3. Reflection
  
After you have completed Tasks 1 and 2 go back to the **Second Midterm** assignment page on [Bb](https://mybb.gvsu.edu).
You will submit your reflection here that minimally includes:

- A *clickable* link to your Second Midterm repository.
- A reflection on what was hard/easy, problems you came across and how you solved them, helpful tutorials you read, etc.
