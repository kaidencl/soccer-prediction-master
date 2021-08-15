# soccer-prediction-master
Several models for predicting the outcome of European league soccer matches.

### Problem Statement
---
The goal is to predict the outcome of a game based on pre-game odds and some other information.

### Table of Contents
---
- [Data Collection](#Data_Collection)
- [EDA](#EDA)
- [Modeling](#Modeling)
- [Conclusions and Recommendations](#Conclusion_and_Recommendations)
- [Soruces](#Sources)

### Data_Collection
---
After some exploration, I chose the data from football-data.co.uk. (https://www.football-data.co.uk/) It provides information about the odds of each of the six bookmakers on each game. Some companies, like Interwetten, don’t allow individuals to scrape data, and their odds are critical to analyzing the results. The football-data.co.uk site plays the role of a good database.  <br/>
You can find the notes for each column of data here: https://www.football-data.co.uk/notes.txt

### EDA
---
At first I tried to split up the data, using home team stats and home team odds to predict home team results, but unfortunately that didn’t work. I think it’s because the three odds per game have an effect on the number of goals scored by both sides, which is the result of the game. So I took the simplest approach: I combined the data from all five leagues, removed the team names, and used that data to predict the full time result. <br/>
Since we know that if there is a significant difference in the odds of a match between different bookmakers, there is a higher probability that the game will have an abnormal result, I calculated the variance between the odds. There are only two columns of Asian Handicap, so I didn’t calculate that part of the variance. <br/>
I used principal component analysis and fitted its results into different models. Remarkably, I got a worse result on the neural network, and when I put all the data into the neural network, it worked again.

### Modeling
---
I used all the data to divide the training set and the test set. <br/>
Logistic regression + principal component analysis is my first choice, The results are: <br/>
75.5% accuracy in the training set and 74.3% accuracy in the test set. <br/>
I also tried running random forests and support vector machine, and the results weren’t as good as logistic regression. All kinds of decision trees don’t work in almost all the models I make, they’re all over-fitting. <br/>
The neural network based classification model, which is considered as the best model in the world of soccer betting, performs well, achieving an accuracy of 75% in both test and training sets. I think this result is the culmination of my dataset performance.

#### How to predict a new game
In addition to scraping all the odds on the game, we need game stats (that haven't taken place yet). The approach I use is to take the average of the first five away (or home) games. It’s not my idea, but it makes sense.

### Conclusion_and_Recommendations
---
As I said, this dataset has its limits. It includes the odds a few hours before the start of the game, as well as the odds just before the start of the game, however: <br/>
Most bookmakers change the odds dozens of times before the game starts, and unless we get all of these numbers, we can’t tell what they’re really trying to do. <br/>
Inaccurate game stats can also affect accuracy. Maybe I’m using the data of the future to predict the future, but as you all know, I have a better way of predicting the fortunes of the two teams. However, some people feel that this is not a proper way, so I don't think I have to share my essence of knowledge to such people.

### Sources:
---
* Data sets for the Premier League and other leagues: https://www.football-data.co.uk/englandm.php
