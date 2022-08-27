# Data_wrangling_analysis_Project UDACITY
## #WeRateDogs wrangling

## Introduction

Real-world data rarely comes clean. Using Python and its libraries, I gathered data from a variety of sources and in a variety of formats, assessed its quality and tidiness, then clean it. I documented my wrangling efforts in a Jupyter Notebook, and showcased them through analyses and visualizations using Python (and its libraries).

The dataset I wrangled (and analyzing and visualizing) was the tweet archive of Twitter user [@dog_rates](https://twitter.com/dog_rates), also known as [WeRateDogs](https://en.wikipedia.org/wiki/WeRateDogs). WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10. The numerators, though? Almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because ["they're good dogs Brent."](http://knowyourmeme.com/memes/theyre-good-dogs-brent) WeRateDogs has over 4 million followers and has received international media coverage.

WeRateDogs [downloaded their Twitter archive](https://support.twitter.com/articles/20170160) and sent it to Udacity via email exclusively for us to use in this project. This archive contains basic tweet data (tweet ID, timestamp, text, etc.) for all 5000+ of their tweets as they stood on August 1, 2017. More on this soon.

![dog_image](https://user-images.githubusercontent.com/40744059/187034099-60ac111f-4477-43e6-b845-8c2b73d91ed9.png)


## Data Wrangling Process
This project was performed following the below process:

* Gathering Data
* Assessing Data
* Cleaning Data
* Storing Data
* Analyzing and Visualization
* Reporting
### Gathering Data
I gathered data from 3 different sources: csv, tsv, and scraped tweet
* The WeRateDogs Twitter archive: it's a csv file
* The tweet image predictions: This file (image_predictions.tsv) is present in each tweet according to a neural network. It is hosted on Udacity's servers and I used the Requests library and the following URL: [link](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv)
* Data from the Twitter API: Gather each tweet's retweet count and favorite ("like") count at the minimum. Using the tweet IDs in the WeRateDogs Twitter archive, query the Twitter API for each tweet's JSON data using Python's [Tweepy](http://www.tweepy.org/) library 
### Assessing Data
I visually and programmatically assessed the dataset to detect issues:

#### Quality Issue detected are:

##### Twitter_archive
* Timestamp and retweeted_status_timestamp datatype should be datatime
* [tweet_id, retweeted_status_id, retweeted_status_user_id] should be object and not float[avoid operation
being perform]
* floofe, pupper,puppo,doggo has alot of missing value, indicated as None instead of NaN
* Name has irrelevant names like "a","not","all","by","the","my" etc
* there are more than 1 dog stage e.g doggo and pupper(12), doggo and floofer(1), doggo and puppo(1)
* Duplicated value in expanded_url
##### Tweet_data
* tweet_id, create_date has incorrect datatype
##### dog_pred
* duplicated values in jpg_url

#### Tidiness issues are:
##### Twitter_archive
* [Doggo, puppo, pupper,floofer] should be in one column as "stages"
* source having unnecessary html tags 'Twitter for iPhone'
* in_reply_to_status_id and in_reply_to_user_id are not original data
* Only the original tweet is needed, drop all retweet columnsi.e retweeted_status_id,
* retweeted_status_user_id, retweeted_status_timestamp
##### Tweet_data
* create_date exist in Twitter_archive as timestamp. therefore, create date should be drop
##### dog_pred
* Ensure that all rows contain at least one true prediction
### Cleaning Data
A copy of each DataFrame was created (Twitter_archive_df, Tweet_data_df, and dog_pred_df). In order to fix each quality/tidiness issue, I followed a three-stage model of programmatic data cleaning:
* Define 
* Code 
* Test.
### Storing Data
Following the cleaning process, I merged the 3 cleaned datasets into 1 using pandas.merge(how=inner, on=tweet_id) library. Then, I saved the file as a CSV
### Analyzing and Visualization
I analyzed the dataset to answer the following questions
* Which device is used to tweet the most?
* Top tweet IDs with the most average likes
* When and in what month did the most tweets occur?
* What are the most common dog names
