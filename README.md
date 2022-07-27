# IMDB Movie Prodject

## Introduction
You have been hired to produce a MySQL database on Movies from a subset of IMDB's publicly available dataset. Ultimately, you will use this database to analyze what makes a movie successful and will provide recommendations to the stakeholder on how to make a successful movie.  There are FOUR parts to this exercise for you to complete in sequential order.


Based on your customers' previous research, they realized they want to focus on the following files, which can be downloaded from [Link to IMDB](https://datasets.imdbws.com/) :

**title.basics.tsv.gz**

**title.ratings.tsv.gz**

**title.akas.tsv.gz**

Overview/Data Dictionary: [Link to IMDB Data Dictionary](https://www.imdb.com/interfaces/)

## Problem Description

* Part 1 of the project, you will create your project repository using GitHub Desktop, load the official Internet Movide Database(IMDB) data based on customer requirements, filter out unnecessary data, and save the **filtered** data as gzip-compressed csv files (".csv.gz") in your repository for further analysis. 

* Part 2 of the project, your stakeholder realized that there is no financial information included in the IMDB data (e.g. budget or revenue). This will be a major roadblock when attempting to analyze which movies are successful.  So, please extract the budget, revenue, and MPAA Rating (G/PG/PG-13/R), which is also called "Certification" from the database.  **Note: this process can take a long time and may need to run overnight.**

* Part 3 of the project, you will be practicing applying an E.T.L. process on your previously saved movie data. Specifically, you will create a new MySQL database after preparing the data for a relational database.  You will export your database to a .sql file in your repository using MySQL Workbench.

* Part 4 of the project, you will be using your MySQL database from Part 3 to answer meaningful questions for you.  hey want you to use your hypothesis testing and statistics knowledge to answer 3 questions about what makes a successful movie.



## Solution Description
IMDB provides several files with varied information for Movies, TV Shows, Made for TV Movies, etc.

### Specifications

**Part 1**

Your stakeholder only wants you to include information for movies based on the following specifications:

+ Exclude any movie with missing values for genre or runtime

+ Include only full-length movies (titleType = "movie")

+ Include only fictional movies (not from documentary genre)

+ Include only movies that were released 2000 - 2021 (include 2000 and 2021)

+ Include only movies that were released in the United States

**Part 2**

+ Your stakeholder wants you to take the data you have been cleaning and collecting in Parts 1 & 2 of the project, and create a MySQL database for them.  

+ Create a separate repository for EDA.

**Part 3**

+ Normalize/Transform the tables as best you can before adding them to your new database:

- Convert the single string of genres from title basics into 2 new tables.
> "title_genres"  with columns:
- tconst
- genre_id

> "genres" with columns:
- genre_id
- genre_name

- Discard/Drop all unnecessary information:

> For the title basics table, drop the following columns:
- "original_title" (we will use the primary title column instead)
- "isAdult" ("Adult" will show up in the genres so this is redundant information).
- "titleType" (every row will be a movie).
- "genres" and other variants of genre (genre is now represented in the 2 new tables described above.

- Do not include the title_akas table in your SQL database.
- Any nulls

+ Keep all of the data from the TMDB API in 1 table together (even though it will not be perfectly normalized). 

+ You only need to keep the imdb_id, revenue, budget, and certification columns.



**Part 4**

+ Use the TMDB API again and extract data for additional years.

+ To prevent taking >24hr or more extracting TMDB data for all movies from 2000-2022, **EITHER:** 

- Define a smaller (but logical) period of time to use for your analyses (e.g. last 10 years, 2010-2019 (pre-pandemic, etc) 

**OR**

- Coordinate with cohort-mates and divide the API calls so that you can all download the data for a smaller number of years and then share your downloaded JSON data.


### Deliverable

**Part 1**

After filtering out movies that do not meet the stakeholder's specifications:

+ Before saving, run a final .info() for each of the dataframes to show a summary of how many movies remain and the datatypes of each feature

+ Concatenate the TMDB API data results into **one** dataframe, then do some light Exploratory Data Analysis (EDA):

1. How many movies had at least some valid financial information (values > 0 for budget OR revenue)?
(Please exclude any movies with 0's for budget AND revenue from the remaining visualizations)

2. How many movies are there in each of the certification categories (G/PG/PG-13/R)?

3. What is the average revenue per certification category?

4. What is the average budget per certification category?

+ Remember to save your combined TMDB API data results as a .csv.gz file

**Part 2**

After you have joined the tmdb results into 1 dataframe in the EDA Notebook, 

+ Save a final merged .csv.gz of all of the tmdb api data in "tmdb_results_combined.csv.gz"

+ Make sure this is pushed to your github repository along with all of your code:

- One code file for API calls
- One code file for EDA

**Part 3**

+ Use sqlalchemy library with pandas to execute your SQL queries inside your notebook.

+ Create a new database on your MySQL server and call it "movies".

+ Make sure to have the following tables in your "movies" database:

- title_basics
- title_ratings
- title_genres
- genres
- tmdb_data

+ Make sure to set a Primary Key for each table that isn't a joiner table (e.g. title_genres is a joiner table).

+ After creating each table, show the first 5 rows of that table using a SQL query.

+ Make sure to run the "SHOW TABLES" SQL query at the end of your notebook to show that all required tables have been created.

**Part 4**

1. The stakeholder's first question is: Does the MPAA rating of a movie (G/PG/PG-13/R) affect how much revenue the movie generates?

- Perform a statistical test to get a mathematically-supported answer.
- Report if you found a significant difference between ratings. 
- If so, what was the p-value of you analysis? AND which rating earns the most revenue?
- Prepare a visualization that supports your finding.

2. Now, think of 2 additional hypotheses to test that your stakeholder may want to know.  Some example hypotheses you could test:

- Do movies that are over 2.5 hours long earn more revenue than movies that are 1.5 hours long (or less)?
- Do movies released in 2020 earn less revenue than movies released in 2018?
- How do the years compare for movie ratings?
- Do some movie genres earn more revenue than others?
- Are some genres higher rated than others? etc.
