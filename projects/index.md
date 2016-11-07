---
layout: default
---

# Projects

In my spare time, I like to parse data and draw insights from it. In related efforts, I've worked through some Coursera courses and am sharing this all here. Code is documented in the data science python and R projects.

## Visualizing Ethnic Cuisines App

I created an app that you can find [here](https://lit-bastion-17263.herokuapp.com). It is written with Flask and deployed with Heroku. So far it is still a work in process.

I was interested in finding what distinguishes ethnic cuisines from each other. I scraped recipes from foodnetwork.com and cleaned the ingredients lists. I created wordclouds for each ethnic cuisine, then I applied LDA to the full dataset (~200 MB) to detect patterns in the lists of recipes. I found that, at least with the data I presently have, around 5 categories appear which are robust and seem to correspond roughly to ingredients commonly found in Asian, Eastern European, Western European, and Mexican (or Latin American) dishes. Visualizations are available at the link provided.

The next steps in the analysis are to apply tfidf to the sets of ingredients and attempt the LDA analysis again. Additionally, I would like to create a classifier which can assign ethnicity to user defined lists of ingredients. Since much of the data does not have an ethnicity assigned to it, I would like to create labels through LDA and build the classifier that way.

## Data Science with Python

We test whether university towns significantly different mean housing prices during recessions from non-university towns. We run a t-test to compare the ratio of the mean price of houses in university towns the quarter before the recession starts compared to the recession bottom. We find that university towns have a lower market loss during recessions. 

The following data files are used in this project:

From the Zillow research data site there is housing data for the United States. In particular the datafile for all homes at a city level has median home sale prices at a fine grained level.

From the [Wikipedia page](https://en.wikipedia.org/wiki/List_of_college_towns) on college towns is a list of university towns in the United States which has been copy and pasted into the file university_towns.txt.

From the Bureau of Economic Analysis, US Department of Commerce, the GDP over time of the United States in current dollars, in quarterly intervals. For this project, we only look at GDP data from the first quarter of 2000 onward.

<a href="housing_prices_college_towns/index.html">Housing Prices in University Towns</a>

In this project we access the twitter Application Programming Interface (API) using python. We estimate the public's perception (sentiment) of terms and phrases, and analyze the relationship between location and mood based on a sample of twitter data. We find the most commonly occurring terms in tweets in our corpus of data, the happiest US state, and the ten most common hashtags.

<a href="housing_prices_college_towns/index.html">Analysis of Twitter Data</a>

## Data Science with R

In this project, we work with data from the SeaFlow environmental flow cytometry instrument. We use a dataset that represents a 21 minute sample from the vessel in a file seaflow_21min.csv. This sample has been pre-processed to remove the calibration “beads” that are passed through the system for monitoring, as well as some other particle types. We put up plots showing clustering in the dataset and compare and visualize a decision tree, random forests, and a support vector machine in classifying the type of particle given a set of features.

<a href="seaflow_cytometry/index.html">Seaflow Cytometry Analysis</a> 

Using devices such as Jawbone Up, Nike FuelBand, and Fitbit it is now possible to collect a large amount of data about personal activity relatively inexpensively. These type of devices are part of the quantified self movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. One thing that people regularly do is quantify how much of a particular activity they do, but they rarely quantify how well they do it.

In these projects, I am dealing with data from accelerometers on the belt, forearm, arm, and dumbell of 6 participants. They were asked to perform barbell lifts correctly and incorrectly in 5 different ways. More information is available from the website here (see the section on the Weight Lifting Exercise Dataset).

<a href="cleaning_data_project/index.html">Cleaning and Tidying Data</a> 

<a href="practical_machine_learning_project/index.html">Machine Learning Prediction</a>

BRFSS is an ongoing surveillance system designed to measure behavioral risk factors for the non-institutionalized adult population (18 years of age and older) residing in the US. The BRFSS was initiated in 1984, with 15 states collecting surveillance data on risk behaviors through monthly telephone interviews.

The BRFSS objective is to collect uniform, state-specific data on preventive health practices and risk behaviors that are linked to chronic diseases, injuries, and preventable infectious diseases that affect the adult population. Factors assessed by the BRFSS in 2013 include tobacco use, HIV/AIDS knowledge and prevention, exercise, immunization, health status, healthy days — health-related quality of life, health care access, inadequate sleep, hypertension awareness, cholesterol awareness, chronic health conditions, alcohol consumption, fruits and vegetables consumption, arthritis burden, and seatbelt use.

<a href="BRFSS_Statistics/index.html">BRFSS Analysis</a>

Health policy researchers and the media download the Hospital Compare database as an easy way to obtain a large set of data regarding outcome of care for a number of different conditions including heart attack, pneumonia, and heart failure.

<a href="programming_R_healthcare/index.html">Hospital Outcome Ranker</a> 

<a href="Inference_project/index.html">Central Limit Theorem and Inference</a>
