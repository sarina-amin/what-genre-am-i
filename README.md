# What Genre Am i?

The goal of this project was to classify songs into different genres based on their respective lyrics, with the help of additional audio features. The main reason why I chose this project was to learn more about Natural Language Processing.

Please note this project is still a work in progress, I have evaluated my results from modelling so far but plan to update it with different technologies in the future. 

### Table of Contents
* [Technologies Used](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#technologies-used)
* [Packages Used](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#packages-used)
* [Methods Used](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#methods-used)
* [The Project](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#methods-used)
    * [Gathering Data](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#gathering-data)
    * [Cleaning and Feature Engineering](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#cleaning-and-feature-engineering)
    * [Exploratory Data Analysis and Natural Language Processing](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#exploratory-data-analysis-and-natural-language-processing)
    * [Modelling](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#modelling)
* [Final Thoughts and Areas for Further Exploration](https://github.com/sarina-amin/what-genre-am-i/blob/master/README.md#final-thoughts-and-areas-for-further-exploration)

### Technologies Used
* Python
* Jupyter Notebook

### Packages Used
* Pandas
* Scikit-learn
* Matplotlib
* Seaborn
* Spotipy

### Methods Used
* Machine Learning (Classification)
* Data Visualisation
* Natural Language Processing

## The Project

### Gathering Data

I collected my data from two main sources:
* The 380,000+ Lyrics from Metrolyrics kaggle dataset that was created by Gyanendra Mishra: https://www.kaggle.com/gyani95/380000-lyrics-from-metrolyrics, this dataset provided me with features such as song name, year, artist name, genre and lyrics
* Spotify's API for audio features such as mode, acousticness & danceability, please refer to spotify's developer documentation for a full list of features and their descriptions: https://developer.spotify.com/documentation/web-api/reference/tracks/get-audio-features/



### Cleaning and Feature Engineering

There were many rows with NaN values in the lyrics column, these were dropped although in the future I may look into scraping data to find the missing lyrics. However, most songs with missing lyrics seemed to be foreign language songs. I then cleaned what I assume may have been errors in the original web scraping done by Gyanendra Mishra. I mainly used regex to clean lyrics and removed all songs with less than 10 words in a song - usually these were instrumentals or had incorrect information.

I added a total word count, unique word count and unique to total word count ratio as features in my dataset to help me better understand my data. 

The dataset was heavily skewed, most songs had been released in 2006 or 2007 and the majority were rock songs. Although it would have been interesting to do a time series analysis on lyrical data, I decided not to correct this skew as Natural Language Processing was my main focus. I did, however, correct the genre skew to an extent. Rock previously made up 40% of my data set. To correct this, I removed a certain amount of rock songs from my dataset. Rock now makes up 25% and pop makes up another 25%. As this is a classification problem, the genre skew was less of a problem. I also wanted more data on Pop and Rock lyrics as these are two genres that have a lot of overlap with each other and therefore can be difficult to classify correctly. I wanted to have more data on these two genres so that I had a higher chance of finding more distinct features to use for categorisation. I also dropped Indie, R&B and Folk songs as these genres had very few data points and were too similar to other genres. These 3 genres made up under 5% of my dataset.

I also used the spotify api to get additional audio features for each song. This reduced my dataset again by 60,000 songs as many could not be found on spotify's search. This may have been due to differences such as in song names or where featured artists names appear.

I was unable to remove foreign languages that were written using the english alphabet - this is something that I will continue to look into. I believe spacy-langdetect will resolve this problem for me in the future: https://pypi.org/project/spacy-langdetect/



### Exploratory Data Analysis and Natural Language Processing

A few key take aways in this section were:
* Hip-hop had the largest spread of total number of words and total number of unique words, in addition to having the highest average number of words in a song
* Rock appears to have shorter songs but a much larger spread for unique words
* The distribution of total number of words in a song seems to be more similar for all genres except Hip-Hop and Rock
* All genres had very similar average objectivity scores, this may be due to words not correctly being recognised or given the right sentiment score - however more analysis may be needed to check whether this is true or not
* Metal was the only genre with a negative average polarity score, with hip-hop close behind but still positive
* Pop & rock genres may seem similar in many ways but the average polarity score for pop was twice as high as that of rock
* The average polarity score for electronic and pop were more similar
* There was a great deal of correlation between spotify audio features which I have discussed in more detail in my EDA notebook

### Modelling

I chose to use 5 different classification models:
* Logistic Regression
* KNearestNeighbors
* AdaBoosting
* Gradient Boosting
* Random Forest

My baseline accuracy was 0.25, in the end my Random Forest model (score 0.61) performed the best when rounded to 2 decimal places however it's score was very similar to my Gradient Boosting model (score 0.60). I believe with furthur fine tuning that I could increase my scores. Boosting models were however more computationally intensive and therefore I believe the Random Forest model was the best choice. Although logistic regression (score 0.38) gave me a much lower score than other models, it did enable me to extract feature importance which was insightful.



### Final Thoughts and Areas for Further Exploration

Overall I was happy with my final scores based on the dataset that I had. I believe my scores would have improved if I had been able to remove all foreign language songs. I would like to rerun my project with different types of models and forms of feature extraction such as Naive Bayes Classifiers, Support Vector Machines, Word2Vec Feature Extraction and Principal Component Analysis. I think it would also be interesting to directly analyse audio files myself and create my own genre classifications using unsupervised clustering. I believe Laten Dirichlet Allocation (LDS) for topic modelling may have also enhanced my results.





