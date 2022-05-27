# Project Title: Wrangle and Analyze Data from [@WeRateDogs](https://twitter.com/dog_rates)

## Start Date
May 17, 2022

## End Date
May 27, 2022

## Files
1. [Main Project File](wrangle_act.ipynb): Every data analysis step is documented in this file, from gathering data to analyzing and visualizing data
2. [Act Report](act_report.ipynb): This report contains a brief exploratory data analysis, based on three research questions and their respective visualizations
3. [Wrangle Report](wrangle_report.ipynb): In this document, there is a detailed walkthrough of my data wrangling efforts, which was the focus of this endeavor
4. `data/`: This folder contains the datasets used in the project, and a few screenshots from selected tweets I used in the Act Report.

## Description

This project was undertaken as part of Udacity's [Data Analyst Nanodegree](https://www.udacity.com/course/data-analyst-nanodegree--nd002).

For this project, the goal was to wrangle WeRateDogs Twitter data to create interesting and trustworthy analyses and visualizations. The Twitter archive is great, but it only contains very basic tweet information. Additional gathering, then assessing and cleaning was required for "Wow!"-worthy analyses and visualizations.

For this project, the gathering data phase involved three datasets: 

1. `archive` table: contains the information WeRateDogs sent Udacity and I downloaded directly.

2. `fav_rt` table: contains the information I gathered from Tweepy. Namely, tweet ID, favorite count and retweet count. 

3. `image_prediction`table: WeRateDog's tweets were processed through a neural network that can identify dog breed. This dataset was downloaded programmatically.

After gathering data from multiple methods, I moved on to assessing and cleaning data.

I ended up with the following list of issues:

### Quality:

##### `archive` table:
1. `source` column includes the HTML tag
2. Erroneus datatypes (`timestamp`, `in_reply_to_status_id`, `in_reply_to_user_id`, `retweeted_status_user_id`, `retweeted_status_id`, `retweeted_status_timestamp`)
3. `name` column has 109 rows with invalid, lower case words
4. `name` column has 705 rows in which a dog name wasn't listed but instead of a null value, there is a None string as an entry instead
5. In the `text` column, because of the string quotation marks, the url link breaks if one tries to click on it
6. `doggo`, `pupper`, `puppo`, `floofer`: columns have rows in which a dog stage wasn't listed but instead of a null value, there is a None string as an entry instead
7. `doggo`, `pupper`, `puppo`, `floofer`: erroneous data type, string instead of bool
8. Retweets should be dropped

##### `image_prediction` table:

9. `p1`, `p2`, `p3`: dog breeds are separated by '_' instead of spaces ' '
10. `p1`, `p2`, `p3`: some dog breed are not capitalized
11. The neural network apparently identified that some images are not from dogs

### Tidiness:
1. The dataset could be tidily represented with the columns `favorite_count` and `retweet_count` in the `archive` table
2. Four variables in one column in the `archive` table (`dog_stage`, i.e., doggo, floofer, pupper, and puppo)
3. The dataset could be tidily represented joining the `image_prediction` table into the `archive` table to create one master dataset

For detailed information on how each issue was cleaned, please check the [main project file](wrangle_act.ipynb) or the [brief report](wrangle_report.ipynb) about my wrangling efforts.

### Brief Exploratory Data Analysis

Once the master dataset was cleaned, I moved on to a brief exploratory data analysis.

With the information available, I came up with three research questions:

#### **`1.`** What are the 5 most common dog breeds in terms of sum of favorited tweets?

The top 5 most favorited breeds are: *Golden Retriever, Labrador Retriever, Pembroke, Chihuahua, and Samoyed*.

This insight was only possible after piercing together and cleaning the master dataset. I had to group by dog breed and then get the sum of favorited tweets. Both of those columns were originally in separate datasets.

The Golden Retriever sits comfortably in the Top 1. Further analysis could entail figuring out whether it was the most favorited dog breed simply due to the fact a disproportionate amount of tweets picture a dog from this breed.

For this visualization, I grouped by dog breed and found the amount of times tweets with a specific dog breed was favorited. 

#### **`2.`** Does the dog stage influence the number of interactions a tweet receive (favorites and retweets)?

According to WeRateDog's dogtionary, the four dog stages are: doggo, pupper, puppo and floofer. 

One might think that puppers (small dogs, usually younger) get the most interactions, but the data suggests that the number of interactions puppers received are almost the same as doggos (a big pupper, usually older). 

In a distant third, comes the puppos (a transitional phase between puppo and doggos). Lastly, the floofers (any dogs with seemingly excess fur). 

As a limitation, it's worth mentioning that only a small number of tweets from the sample included the dog stage. If we had dog stage information for the whole sample, the results might have been different. 

This analysis was only possible after tidying the dog stage columns and turning them into one.

For this visualization, I grouped by dog breed and got the sum of what I called interactions. For the purpose of this analysis, interactions are the sum of the amount of times a tweet was favorited and the amount of times a tweet was retweeted. 

#### **`3.`** Does the average rating increase through time?

Although we only have tweet information from 2016 to 2017, the data seem to suggest the average rating for dogs is increasing through time. 

Without converting the timestamp column to datetime, this analysis wouldn't be possible.

For this visualization, I grouped by trimester and found the average rating for tweets with only one dog. Then, I plotted a line chart.

For detailed information on how each analysis was performed and their respective visualizations, please check the [main project file](wrangle_act.ipynb) or the [brief report](act_report.ipynb) about the exploratory data analysis.