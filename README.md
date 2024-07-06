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

#### Rules & Notes - Please take your time to read the following points:

1. The submission deadline shall be set for the 10th of June at 23:59.
2. It is acceptable that you **discuss** with your colleagues different approaches to solve each step of the problem set. You are responsible for writing your own code, and analysing the results. Clear cases of cheating will be penalized with 0 points in this assignment;
3. After review of your submission files, and before a mark is attributed, you might be called to orally defend your submission;
4. You will be scored first and foremost by the number of correct answers, secondly by the logic used in the trying to approach each step of the problem set;
5. Consider skipping questions that you are stuck in, and get back to them later;
6. Expect computations to take a few minutes to finish in some of the steps.
7. **IMPORTANT** It is expected you have developed skills beyond writting SQL queries. Any question where you directly write a SQL query (then for example create a temporary table and use spark.sql to pass the query) will receive a 25% penalty. Using the Spark syntax (for example dataframe.select("\*").where("conditions")) is acceptable and does not incur this penalty. Comment your code in a reasonable fashion.
8. **Questions** – Any questions about this assignment should be posted in the Forum@Moodle. The last class will be an open office session for anyone with questions concerning the assignment. 
9. **Delivery** - To fulfil this activity you will have to upload the following materials to Moodle:
    1. An exported IPython notebook. The notebook should be solved (have results displayed), but should contain all neccesary code so that when the notebook is run in databricks it should also replicate these results. This means the all data downloading and processing should be done in this notebook. It is also important you clearly indicate where your final answer to each question is when you are using multiple cells (for example you print "my final anwser is" before your answer or use cell comments). Please make sure to name your file in the following way: *[student_number1]_[student_number2]_submission.ipynb*. As an example: *19740001_197400010_submission.ipynb*
    2. **Delivery** - You will also need to provide a signed statement of authorship, which is present in the last page;
    3. It is recommended you read the whole assignment before starting.
    4. You can add as many cells as you like to answer the questions.
    5. You can make use of caching or persisting your RDDs or Dataframes, this may speed up performance.
    6. If you have trouble with graphframes in databricks (specifically the import statement) you need to make sure the graphframes package is installed on the cluster you are running. If you click home on the left, then click on the graphframes library, from where you can install the package on your cluster (check the graphframes checkbox and click install). Another installation option is using the JAR available on Moodle with the graphframes library.
10. **Note**: By including the name and student number of each group member  in the submission notebook, this will be considered as a declaration of authorship.

#### Data Sources and Description
We will use data from IMDB. You can download raw datafiles
from https://datasets.imdbws.com. Note that the files are tab delimited (.tsv) You can find a
description of the each datafile in https://www.imdb.com/interfaces/


## Questions
### Data loading and preperation
Review the file descriptions and load the necessary data onto your databricks cluser and into spark dataframes. You will need to use shell commands to download the data, unzip the data, load the data into spark. Note that the data might require parsing and preprocessing to be ready for the questions below.
