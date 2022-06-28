# Introduction

I completed this project as part of Udacity's Data Analyst Nanodegree. The project is based around the "WeRateDogs" Twitter page, a page which will kindly rate pictures and videos of dogs out of ten. Since dogs are all round fantastic creatures, all of WeRateDogs’ ratings are above ten. They also tag each dog with a different category out of “doggo”, “floofer”, “pupper”, or “puppo”.

An archive of this Twitter data for WeRateDogs’ tweets was provided for this project as a CSV file. Two more sources of data were also gathered as part of this project: predictions for which type of dog is present in each picture (carried out previously, not by myself, by being passed through an image classification algorithm) and additional tweet information acquired from Twitter.

I approached this project using the three steps of data wrangling: gather, assess, clean. In the gather phase, the image prediction data was downloaded using Python's Requests library. The additional Twitter information (i.e. retweet and favorite counts) was downloaded using the Twitter API. In the following assess step, I then inspected the generated data frames in order to find any quality or tidiness issues. The cleaning step subsequently involved implementing steps to fix the quality and tidiness issues that were previously identified.

Following the data wrangling process, and some exploration and analysis of the (now clean and tidy) data, was carried out, numerous interesting results were observed.

# Libraries
- Tweepy
- Request 
- Matplotlib
- Pandas
- Numpy
- os

