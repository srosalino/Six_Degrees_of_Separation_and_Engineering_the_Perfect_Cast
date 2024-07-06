# Six Degrees of Kevin Bacon
**Introduction** - Six Degrees of Kevin Bacon is a game based on the "six degrees of separation"
concept, which posits that any two people on Earth are six or fewer acquaintance links apart. Movie
buffs challenge each other to find the shortest path between an arbitrary actor and prolific actor
Kevin Bacon. It rests on the assumption that anyone involved in the film industry can be linked
through their film roles to Bacon within six steps.
The analysis of social networks can be a computationally intensive task, especially when dealing with
large volumes of data. It is also a challenging problem to devise a correct methodology to infer an
informative social network structure. Here, we will analyze a social network of actors and actresses
that co-participated in movies. We will do some simple descriptive analysis, and in the end try to
relate an actor/actress’s position in the social network with the success of the movies in which they
participate.


## Questions
### Data loading and preperation
Review the file descriptions and load the necessary data onto your databricks cluser and into spark dataframes. You will need to use shell commands to download the data, unzip the data, load the data into spark. Note that the data might require parsing and preprocessing to be ready for the questions below.


### Network Inference, Let’s build a network
In the following questions you will look to summarise the data and build a network. We want to examine a network that abstracts how actors and actress are related through their co-participation in movies. To that end perform the following steps:

**Q1** Create a DataFrame that combines **all the information** on each of the titles (i.e., movies, tv-shows, etc …) and **all of the information** the participants in those movies (i.e., actors, directors, etc … ), make sure the actual names of the movies and participants are included. It may be worth reviewing the following questions to see how this dataframe will be used.

How many rows does your dataframe have?


**Q2** Create a new DataFrame based on the previous step, with the following removed:
1. Any participant that is not an actor or actress (as measured by the category column);
1. All adult movies;
1. All dead actors or actresses;
1. All actors or actresses born before 1920 or with no date of birth listed;
1. All titles that are not of the type movie.

How many rows does your dataframe have?


**Q3** Convert the above Dataframe to an RDD. Use map and reduce to create a paired RDD which counts how many movies each actor / actress appears in.

Display names of the top 10 actors/actresses according to the number of movies in which they appeared. Be careful to deal with different actors / actresses with the same name, these could be different people.


**Q4** Start with the dataframe from Q2. Generate a DataFrame that lists all links of your network. Here we shall consider that a link connects a pair of actors/actresses if they participated in at least one movie together (actors / actresses should be represented by their unique ID's). For every link we then need anytime a pair of actors were together in a movie as a link in each direction (A -> B and B -> A). However links should be distinct we do not need duplicates when two actors worked together in several movies. 

Display a DataFrame with the first 10 edges.


**Q5** Compute the page rank of each actor. This can be done using GraphFrames or
by using RDDs and the iterative implementation of the PageRank algorithm. Do not take
more than 5 iterations and use reset probility = 0.1.

List the top 10 actors / actresses by pagerank.


**Q6**: Create an RDD with the number of outDegrees for each actor. Display the top 10 by outdegrees.


### Let’s play Kevin’s own game

**Q7** Start with the graphframe / dataframe you developed in the previous questions. Using Spark GraphFrame and/or Spark Core library perform the following steps:

1. Identify the id of Kevin Bacon, there are two actors named ‘Kevin Bacon’, we will use the one with the highest degree, that is, the one that participated in most titles;
1. Estimate the shortest path between every actor in the database actors and Kevin Bacon, keep a dataframe with this information as you will need it later;
1. Summarise the data, that is, count the number of actors at each number of degress from kevin bacon (you will need to deal with actors unconnected to kevin bacon, if not connected to Kevin Bacon given these actors / actresses a score/degree of 20).


### Exploring the data with RDD's

Using RDDs and (not dataframes) answer the following questions (if you loaded your data into spark in a dataframe you can convert to an RDD of rows easily using `.rdd`):

**Q8** Movies can have multiple genres. Considering only titles of the type 'movie' what is the combination of genres that is the most popluar (as measured by number of reviews). Hint: paired RDD's will be useful.


**Q9** Movies can have multiple genres. Considering only titles of the type 'movie', and movies with more than 400 ratings, what is the combination of genres that has the highest **average movie rating** (you can average the movie rating for each movie in that genre combination). Hint: paired RDD's will be useful.


**Q10** Movies can have multiple genres. What is **the individual genre** which is the most popular as meaured by number of votes. Votes for multiple genres count towards each genre listed. Hint: flatmap and pairedRDD's will be useful here.


## Engineering the perfect cast
We have created a number of potential features for predicting the rating of a movie based on its cast. Use sparkML to build a simple linear model to predict the rating of a movie based on the following features:

1. The total number of movies in which the actors / actresses have acted (based on Q3)
1. The average pagerank of the cast in each movie (based on Q5)
1. The average outDegree of the cast in each movie (based on Q6)
1. The average value for for the cast of degrees of Kevin Bacon (based on Q7).

You will need to create a dataframe with the required features and label. Use a pipeline to create the vectors required by sparkML and apply the model. Remember to split your dataset, leave 30% of the data for testing, when splitting your data use the option seed=0.

**Q11** Provide the coefficients of the regression and the accuracy of your model on that test dataset according to RSME.


**Q12** What score would your model predict for the 1997 movie Titanic.


**Q13** Create dummy variables for each of the top 10 movie genres for Q10. These variable should have a value of 1 if the movie was rated with that genre and 0 otherwise. For example the 1997 movie Titanic should have a 1 in the dummy variable column for Romance, and a 1 in the dummy variable column for Drama, and 0's in all the other dummy variable columns.

Does adding these variable to the regression improve your results? What is the new RMSE and predicted rating for the 1997 movie Titanic.


**Q14 - Open Question**: Improve your model by testing different machine learning algorithms, using hyperparameter tuning on these algorithms, changing the included features. What is the RMSE of you final model and what rating does it predict for the 1997 movie Titanic.
