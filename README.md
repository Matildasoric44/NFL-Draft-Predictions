# NFL-Draft-Predictions
## Intro

Every year, the NFL invites over 300 prospects to perform at the NFL Combine. The main purpose of the combine is for prospects to display their raw talents to teams before the NFL Draft. Prospects perform in events like the 40 Yard Dash, Bench Press, Vertical Jump, and many more. Teams then decide who they are going to draft based upon combine measurements, college performance. etc.

In this project, our goal is to create a model that can predict the round or pick each prospect will be taken at.
We'll start by loading in several useful libraries and reading our .csv files into dataframes. Our draft dataframe contains the round and pick that each player was drafted at; our combine dataframe contains general information and combine results concerning each player.
Each of our dataframes have several columns that don't serve as any use to us. So, we'll drop these columns in order to focus on what we care about. 
## Data Cleaning and Exploration
Our data also includes a column called `playerID`, which we'll use as the point to combine our draft and combine dataframes so we can have all the information we need in one place.
There are a few small changes that we're going to make before we start creating models. First, we're going to remove the data from the 2019 NFL Draft because it contains no information about the draft rounds. Then, we will make very minor changes to ceratin columns while editing information about the positions in the data we'll keep. We're also going to remove the rows that have a `Null` value in the `position` column.
In order to create models, we can't have any null values in our data. We can't remove all rows with null values because it would take too much out of our data set. Since every remaining column with a null value is a combine result, we'll fill the null values with 0.

We've only included the measurements that are taken and the events that occur in the modern NFL combines.
The modern day draft only has 7 rounds, but has had more than that in the past. Because of this, the model would predict certain prospects to be drafted in a round that no longer exists. So we'll consider any prospect with a prediction past round 7 to be undrafted, which will be respresented by the digit "8".
During data exploration, we'll primarily be looking for anything we can use to our advantage when making models, but we'll also include any interesting trends or findings in our data.

We found that the defensive line is the most commonly selected position during the first round of the draft. This gives us a better understanding as to the strategy and needs of teams in the NFL. Something interesting we can take away from this is that QB is the 7th most drafted position in the first round, but it is the most commonly drafted position with the first pick.
We also found that the college a prospect played for does somewhat encourage whether or not they get drafted. Intuitively, this makes sense as the general assumption would be that the higher skill level a prospect plays at, the more likely they are to play professionally.
Florida State has an impressive number of selections overall with 157. A large majority of these selections took place in the first and second rounds, which supports the claim made previously about the correlation between skill level and whether or not a prospect plays professionally.

Now that we've manually explored some possible correlations in our data, let's use Python's built-in methods to look at correlation between our variables.
We examined teh correlation coefficiens with `pick` and `round` and found that no variable has a particularly strong correlation with Round or Overall Pick. This can be for a number of reasons; let's revisit this after constructing and analyzing our model.
## Model for Overall Pick
For our model, we're going to use a Decision Tree Regressor to attempt to predict the pick a prospect will be selected at. We'll start by splitting our data into training and testing sets and then plotting what our model predicts for each prospect against the overall pick that they were actually selected at.
As the plot shows us, our model waa way off on some predictions and spot on for others. This is most likely because of the role that technical ability plays during the draft process. In other words, teams don't always just look for the prospect with the best raw talent, but rather ones that possess technical abilities as well. The NFL Combine does have technical drills in which the measure a prospect's football abilities, but those results were not included in our data. If our data did have access to this kind of information, it would most likely be a lot more accurate in terms of predicting where a prospect will be selected.
## Model for Round Predictions
We started off by splitting our data into train and test dataframes. We used quarterbacks to look at the predictions of each model. First model was K Nearest Neighbors Regressor with 3 nearest neighbors.Then we fitted a Random Forest Regressor, Decision Tree Regressor and XGBOOST Regressor. We didn't find much linearity between predictions and actual values so we performed hyperparemter tunning for each of the models. No progress was seen after hyperparemeter tunning. We tried the same concept just with Classifiers and got a slightly better output but still not good enough. We then decided to enseble those models and took avergae predictions from regressors' predictions and mode predictions from the classifiers'prediction. 
That resulted in a slighlty imporved model but still without much linearlity.
## Conculsion
After running all of our model we conclude that Comine results are best used in conjunction with other information about a prospect. A model that has access to measurements of technical skill would most likely perform much better. There is that human part of scouting a player that cannot be measured and it plays a big role in the Draft.
