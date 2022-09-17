# Introduction/overview:
_goals of the project, as well as challenges or limitations foreseen_

Project Weatherman is designed to build weather forecasting models for Michigan based on data from other weather stations in the area. Before modern weather forecasting was invented, say 1922, people in the US could call someone hundreds of miles to the west and ask what the weather was in that location.  Since most US weather systems move west to east the person placing the call could expect that in a few hours or days that weather would reach them. 

We will try to replicate this using machine learning.  By feeding in hourly weather data from hundreds of weather stations we plan to build models that can predict, with a reasonable accuracy compared to dummy models, what the “weather” will be in 4, 24, or 48 hours.   We believe that shorter timeframes will be more accurate in the modeling.  A stretch goal of the project is to build a web interface where users can input a weather station and the program will pull in live data from the government API and input it into the model for that station.

There are several challenges with this approach.  First will be the amount of data, we will need hundreds of thousands of data points to achieve accurate models.  In addition each location will need to have an individual model built for it.  Our current data source has 78 locations just for Michigan, so if we tried to scale this to the entire country it would be 12000+ models.  Additionally we may need a model for every time period, so 3 models per location.  Finally we have to determine how we define weather?  Will we predict temperature, precipitation, chance of precipitation, or a combination?  We plan to start with building models for Michigan and just one weather variable and scale from there. 
  
Another challenge will be achieving significant results.  Not even the sophisticated models the government uses are completely accurate, our model may return results that are statistically random, even at the 4 hour mark.  

# Specific contributions that each team member will make to the project.
Plankheet - Data transformation for Modeling, model evaluation - Stretch goal - building web interface.  
JCarroll - supervised model hyper-parameter optimization lead and supervised model data visualization creation. 
RLayedra - Assist win the hyper-parameter tuning. Because of the scope of this project, this task will need all hands on deck to produce and share the best model.

# Timeline
Week 1 - Project Formulation
Week 2 - Draft Proposal - Initial Data Exploration
Week 3 - Continue Data Exploration
Week 4 - Build Trial Models - Evaluate to find best scoring technique
Week 5 - 6 Expand Models to multiple locations
Week 7 - 8 Write report, build final visuals, stretch goal

# Part A (Supervised learning)
## Learning approaches and feature representations that are appropriate to this problem: 

We will first explore how a gradient boosted decision tree model will perform in this prediction problem, because they are known to have high accuracy with moderate memory and runtime requirements. Additionally, they can generally perform well in a high feature space which may be the case for this prediction task with data from several stations and times. The primary objective with evaluating this model will be optimization of the number of estimators, learning rate, and tree depth parameters.  

We have a couple of exciting feature representations we wish to explore.  First our plan isn’t to do this as a true time series, as we aren’t predicting the future of a weather station based on its past, but more using all the other stations data as features to predict what the weather will be in set intervals in the future.  However we do plan to contrast this approach against looking at the data as a time series.  Is using other stations more effective or less?  We predict that if the weather is stable then they will be the same, but as storm fronts come through time series approach will be less effective.  Additionally what happens if we include the “home” station weather as a feature, does that change the effectiveness of the model?

## External datasets or tools that might be incorporated to help with the problem:
The primary data acquisition will be from the meteostat python library, which aggregates weather data from various sources. However, there may be a need to supplement this with some geolocation data for the model to better learn the spatial relationships between the weather stations.

## The evaluation and visualization methods planned:
 There are multiple ways in which we’ll evaluate our models, primarily though (especially with respect to temperature predictions) we will evaluate model performance accuracy using the R-squared metric. 
We will visualize how the accuracy scores change with various iterative changes in the hyper-parameters, using line graphs. We will also use line charts to compare how our model compares to dummy classifiers.

# Part B (Unsupervised learning)
## Question(s) about the dataset’s structure to answer/ goals to achieve:
We’ll explore clustering this data into regions (weather stations); we might  be able to use information from these clusters to include as features in our supervised models. We also want to explore what features to include, how many weather stations are needed to train a decent model, and is that consistent over time (allowing us to work toward our stretch goal).  
What data manipulation will be necessary for this dataset to prepare it?
Grouping the dataset by stations will be our first step. We can do additional EDA based on the results we get.  We will need to transform the data so that station X has the other stations weather attributes as features from Y hours in the past.  For example, station KGRR (Grand Rapids) - we would input all the other weather stations past 24 hour temperature as features 

## Unsupervised learning approaches and feature representations that are appropriate for this problem:
Our supervised learning model will be mostly responsible for our predictions; depending on our results from the supervised learning tasks, dimensionality reduction along with anomaly detection in our clusters might be a possibility to fine-tune or supervised learning models.
We will use PCA and other techniques for feature reduction, otherwise we will have over 12000+ other other stations weather data as features.  Ideally we would like to identify the 10-20 stations that have the most predictive power for a particular station, so we can build them into our stretch goal.  

## External datasets or tools that might be incorporated to help with the problem:
The same dataset used for our supervised learning will be used for these tasks.

## Evaluate methods:
Our objective is to to use the unsupervised learning tasks to enhance our prediction. We lack domain expertise in weather prediction so interpreting the clusters and/or dimensionality reduction thru PCA will be challenging.

## Visualizations that would be appropriate as part of evaluation:
A combination of Biplots, scatter plots, and line plots will be used to explore and interpret the results.
