# Introduction

I completed this project as part of Udacity's Data Analyst Nanodegree. The project is based around the "WeRateDogs" Twitter page, a page which will kindly rate pictures and videos of dogs out of ten. Since dogs are all round fantastic creatures, all of WeRateDogs’ ratings are above ten. They also tag each dog with a different category out of “doggo”, “floofer”, “pupper”, or “puppo”.

An archive of this Twitter data for WeRateDogs’ tweets was provided for this project as a CSV file. Two more sources of data were also gathered as part of this project: predictions for which type of dog is present in each picture (carried out previously, not by myself, by being passed through an image classification algorithm) and additional tweet information acquired from Twitter.

I approached this project using the three steps of data wrangling: gather, assess, clean. In the gather phase, the image prediction data was downloaded using Python's Requests library. The additional Twitter information (i.e. retweet and favorite counts) was downloaded using the Twitter API. In the following assess step, I then inspected the generated data frames in order to find any quality or tidiness issues. The cleaning step subsequently involved implementing steps to fix the quality and tidiness issues that were previously identified.

Following the data wrangling process, and some exploration and analysis of the (now clean and tidy) data, was carried out, numerous interesting results were observed.

### Libraries
- Tweepy
- Request 
- Matplotlib
- Pandas
- NumpyThe main notebook for the analysis is `wrangle_act.ipynb`.

## Data Gathering 
I gathered data from three sources. I manually downloaded the twitter archive data, `twitter-archive-enhanced.csv`. I programmatically downloaded the image prediction data, `image-predictions.tsv` using the Python request library. I used the Twitter API to gather data about `favorite count` and `retweet count`.   The `twitter-archive-enhanced.csv` contains data about tweets from `WeRateDogs` from 2015-2017. Here's a preview of the `twitter-archive-enhanced.csv` data

## Assessing

### Quality issues

Here are some quality issues I noticed in the data via visual and programmatic assessment.

**twitter_archive data**

1. Missing values in `in_reply_to_status_id`, `in_reply_to_user_id`, `retweeted_status_id`, `retweeted_status_user_id`, `expanded_urls` and `retweeted_status_timestamp` columns.

2. `tweet_id` is an `integer` instead of an `object`. The variables `in_reply_to_status_id`, `in_reply_to_user_id`, `retweeted_status_id`, `retweeted_status_user_id` are of the type `float` intead of `object`.

3. There are some `None` values in the `name` variable.

4. The `timestamp` variable is of the *object* datatype instead of *datetime*.

5. Retweeted data is included in the dataset.

6. The values `a`, `an`, `the`, and `just` in the `name` column are not dog names.

7. HTML formatting in the `source` column.


**image_prediction data**

7. `tweet_id` is an integer instead of object.

8. Not all animals in the dataset are dogs. Some are hen, snail, etc

9. Underscores (`_`) in dog breed name. Inconsistent breed names.


### Tidiness issues

1. In the `image prediction data` DataFrame, `p1_dog`, `p2_dog`, `p3_dog` contain the same information. They tell us if the object in the image is *a dog*. There should be just one column that tells us the breed of dog in the image based on the confidence score of the neural network in `p1_conf`, `p2_conf`, and `p3_con`.

2. There are four different columns for the *dog's status*: `dodoggo, floofer, pupper, puppo`. 

*Others*

3. The `image prediction data` and the `tweets api data` DataFrame can be merged as one.
4. Multiple URLs in the `expanded_urls` column of the `df_twitter_archive` dataframe.


## Cleaning

1. Retweeted data is included in the dataset. Not all the tweets are about dog ratings and some of them are retweets. If the value in the `retweeted_status_id` is not null, it means that tweet is a retweet. It should be removed from the dataframe. I filtered the data to show records were the `retweeted_status_id` is null. These records are not retweets.


2. There are missing values in the following columns `in_reply_to_status_id`, `in_reply_to_user_id`, `retweeted_status_id`, `retweeted_status_user_id`, `expanded_urls` and `retweeted_status_timestamp`. These columns won't be useful now. So I dropped them.


3. The `tweet_id` variable is of the type *integer* instead of *object* in both the `twitter archive data` and `image_prediction data`. I converted these variables to the `object` datatype. I won't be using them for any sort of calculation since they are primary keys. 


4. The `timestamp` variable is of the *object* datatype instead of *datetime*. I converted it to *datetime* format.


5. The values `a`, `an`, `the`, and `just` in the name column of the `twitter archive data` are not dog names. I replaced these values with `None`, since the names are unknown.

6. The is HTML formatting in the `source` column of the `twitter archive data`. I had to remove these formatting. After removing the formatting, the actual source of the tweet could be seen.


7. There are four different columns for the dog's status: dodoggo, floofer, pupper, puppo. This is a structural issue. Also, some dogs are `doggo-pupper`, while others are `doggo-puppo`. I created a new column `dog_status` to show if the dog is doggo, floofer, pupper, puppo, doggo-pupper or doggo-puppo.


8. Not all animals in the `image prediction data` are dogs. I removed the records of animals that are not dogs. I used the `p1_dog`, `p1_conf`, `p2_dog`, `p2_conf`, `p3_dog` and `p3_conf` variables to do this. First, I checked the prediction with the highest confidence score between `p1_conf`, `p2_conf`, and `p3_conf`. Then I checked the corresponding value of `p*_dog` to know if it was `TRUE` or `FALSE`. I created a new column `is_dog` to tell if the image is a dog or not. `TRUE` means the image is a dog, `FALSE` means the image is not a dog. I removed records that were not dog images from the `image prediction data`.



9. There should be just one column that tells us the breed of dog in the image based on the confidence score of the neural network in `p1_conf`, `p2_conf`, and `p3_con`. I created a new column `dog_breed`. It is based on which column has the highest confidence score between `p1_conf`, `p2_conf`, and `p3_conf`. The dog breed is the corresponding value of `p*`. For instance, if `p1_conf` has the maximum confidence score, then the dog breed is `p1`. I created a function to do this.



10. I removed unnecessary column from the `image prediction data`. I removed the columns `p1_conf`, `p2_conf`, `p3_conf`, `p1`, `p2`, `p3`, and `is_dog`.


11. I fixed inconsistencies in the `dog_breed` column. I replaced the underscore character `_` with a space ` `. I ensured that all the texts are in lower case.



12. I merged all the three cleaned DataFrames on the `tweet_id`, and saved it in a file called "twitter_archive_master.csv".
- os

### Files
- Image_prediction.csv 