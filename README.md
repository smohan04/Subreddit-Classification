# Subreddit Classification

## r/NBA vs r/NBADiscussion 
### Contents:
- [Purpose](##Purpose)
- [Data](##Data)
- [Model Results](##Model-Results)
- [Conclusions and Recommendations](##Conclusions-and-Recommendations)


## Purpose:
The goal of this project is to import data from two similar subreddits and train a classifer to distinguish between these two subreddits. We will also try to identify distinguishing features of these subreddits. Models will be created using KNN, Logistic Regression and Random Forest. Accuracy scores will be used to measure the effectiveness of each model. We also will look at whether each subreddits posting rules have an effect on the content promoted. 



## Data:
We will collect data from two subreddits:
* r/NBA
* r/NBADiscussion
Both of theses subreddits target similar audiences, fans of the National Basketball Association. While r/NBA is for NBA news and discussions, r/NBADiscussion is tailored specifically to promote high quality discussion.
This difference is highlighted by the rules of each subreddit:


NBA
* 1.Be civil and respectful
* 2.No trolling or baiting users
* 3.No racist, sexist, or homophobic language
* 4.No reposts
* 5.No fake news
* 6.No self-promotion
* 7.No NSFW content
* 8.Posts and comments must be relevant to the NBA
* 9.Stats/Player Tweets/Quotes/Misc. Media are self-post only and must be sourced

NBADiscussion
* 1.Keep it civil.
* 2.Submit high quality content.
* 3.This is a discussion subreddit. Support claims with substantiated arguments.
* 4.Vote based on if the post or comment meets the standard of quality you expect from this subreddit.
* 5.No spam.
* 6.Attack the argument, not the person.
* 7.Most arguments can't be deconstructed in a sentence. Top level comments have a char. minimum of 100
* 8.Present descriptive, clear, and concise titles.
* 9.Present your own argument.
* 10.Posts like "Thoughts?" or "Discuss" are low effort and will be removed.
* 11.Post enough content to provide a jumping-off point. The char. minimum for posts is 350.


### Initial Findings

Notice, in NBADiscussion there is a minimum character requirement for post body content as well as for top level comments. Posts have a quality requirement in the NBADiscussion subreddit and voting is supposed to be based of if the post meets these requirements. NBA posts do not minimum character length requirements, nor do they have strict quality requirements. 
Notice, posts from NBADiscussion have a higher chance of containing a '?' then those from NBA. 
* NBADiscussion = 39% of titles have a question mark
* NBA = 5.1% of titles have a question mark

* NBADiscussion = 60.7% of post body have a question mark
* NBA = 10% of post body have a question mark

The discrepancy in question mark counts in post body's could be due to the fact that body word counts in NBADiscussion are so much highter. 

Exclamation marks are more likely to occurr in the title of NBA posts but in the body of posts, exclamation marks are more likely to be found in NBADiscussion. The high number of exclamation marks in the body could just be due to the high character count of NBADiscussion posts. 

Periods are more likely to occurr in the title of NBA posts but in the body of posts, periods are more likely to be found in NBADiscussion. The high number of periods in the body could just be due to the high character count of NBADiscussion posts.

Run t-test on lengths and words counts to see if there is a statistically significant difference between the two subreddits.
* significance level: 𝛼=0.05
* null hypothesis: 
    * There is no significant difference in character length of subreddit post titles and post body text between subreddits. 
    * There is no significant difference in word counts of subreddit post titles and post body text between subreddits.

### Features Created
* title_length - character length of the title of each post
* title_word_count - word count of the title of each post
* body_length - character length of the body of each post
* body_word_count - word count of the body of each post
* title_question_mark - binary number indicating whether the title has a question mark or not
* body_question_mark - binary number indicating whether the body has a question mark or not
* title_exclamation_mark - binary number indicating whether the title has a exclamation mark or not
* body_exclamation_mark - binary number indicating whether the body has a exclamation mark or not
* title_period -binary number indicating whether the title has a period or not
* body_period - binary number indicating whether the title has a period or not

        
#### Note:  
* title length/word count is positively correlated with the subreddit (longer titles mean its more likely to belong to NBA subreddit) 
* body length/word count is negative correlated with the subreddit (longer body text means its more likely to be long to NBADiscussion subreddit)

Use body word count and title word count for analysis instead of length values because word count and length are highly correlated. Using word count instead of length values because it is easier to interpret word count.

Punctuation seems to be highly correlated with subreddits. Question marks in titles and periods in body paragraphs are highly correlated with NBADiscussion while periods in the title lean towards NBA.  

Out of 1000 posts in NBA, 731 have an empty body compared to only 39 out of the 995 NBADiscussion posts. Note that NBADiscussion has a minimum body char length of 350.


## Model Results

| Data                                           | KNN Train | KNN Test | LR Train | LR Test  | RF Train | RF Test  |
|------------------------------------------------|-----------|----------|----------|----------|----------|----------|
| Word Counts Only (title and body)              | 0.912433  | 0.877755 | 0.838903 | 0.827655 | 0.977272 | 0.873747 |
| Title Vectorized (c)                           | 0.766042  | 0.619238 | 0.962566 | 0.819639 | 0.998663 | 0.787575 |
| Title Vectorized and Word Counts (cvec)        | 0.921791  | 0.877755 | 0.915775 | 0.861723 | 0.999331 | 0.879759 |
| Body Vectorized (c)                            | 0.866978  | 0.803607 | 0.978609 | 0.889779 | 0.978609 | 0.871743 |
| Body Vectorized and Word Counts (cvec)         | 0.915106  | 0.887775 | 0.959893 | 0.879759 | 0.981951 | 0.873747 |
| Title & Body Vectorized (c)                    | 0.841577  | 0.811623 | 0.989973 | 0.897795 | 0.999331 | 0.863727 |
| Title & Body Vectorized  Word Counts (cvec) | 0.915106  | 0.889779 | 0.969919 | 0.897795 | 0.999331 | 0.865731 |

## Conclusions and Recommendations
The models all performed well on classifying data. This may be due to the large word count differences between the two subreddits. Taking out stop words seems to decrease accuracy and this again may be due to large word count. Adding punctuation improved scores probably due to the high correlations of punctuations. 

NBADiscussion subreddits seem to ask more questions and have large word counts in the body of the post. NBA bodies usually are smaller and their titles are larger. This is in line with polices of the NBADiscussion subreddit which has minimum character counts for posts bodies and expect titles to be concise. Also, posts have higher amount of question marks because they may ask more questions to spur discusssion. 

#### Further Areas of Study
* Sentiment analysis of each subreddit

* Study vocabulary used in each subreddit

* Study vectorized data again but account for word count

