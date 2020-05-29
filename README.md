# This project is part of Udacity's Nanodegree program "Data Engineering"

# Purpose

In this project we are going to receive details about board games from two sources. The first source contains meta information about almost 100.000 board games (number of players, genre, ..). The second source contains the ratings of the board games on a daily basis (+2 mio. rows). Our goal is to link these two sources and transform the data into an easier digestible data model to enable Data Analysts to see trends by genre or other game parameters.

# Scope
We are transforming the two data sources about board games and their ratings into a data model with five tables. We gather the daily ratings of the board games, aswell as category, game family, game mechanics, number of players, minimum age and some more.

 Since we talk about daily ratings, we can then use this data to find trending game types in the board gaming industry.

The amount of data is still easily managable on a local machine, so we decided to run this locally while (thinking about possible future scenarios) using mainly Spark for reading the data and transforming it. In the end we will persist the tables with parquet.

# Data sources
First dataset (Daily rankings; given as git repository with csv files):
https://github.com/beefsack/bgg-ranking-historicals

Second dataset (Meta Data; given as kaggle download as sqlite file):
https://www.kaggle.com/mshepherd/board-games?select=bga_GameItem.csv

# Schema after transformation

## rankings (fact table)
|   Column    |                    description                     |
| ----------- | -------------------------------------------------- |
| id          | auto incrementing key                              |
| rank        | rank of the game on the particular date            |
| average     | average rating                                     |
| bayes_avg   | bayes average rating                               |
| users_rated | number of users who rated                          |
| date        | time when the other values were calculated / taken |
| game_id     | foreign key: linking to game_details               |


## game_details (dimension table)

|   Column    |                           description                         |
| ----------- | ------------------------------------------------------------- |
| game_id     | auto incrementing key                                         |
| game_type   | which type of game; e.g. board game, board game expansion, .. |
| maxplayers  | maximum number of players                                     |
| maxplaytime | maximum playtime for one game                                 |
| minage      | recommended minimum age of players                            |
| minplayers  | minimum number of players                                     |
| minplaytime | minimum playtime for one game                                 |
| playingtime | average playing time for one game                             |
| year        | year in which the game was published                          |
| artist      | game artist                                                   |
| designer    | game designer                                                 |


## game_categories (dimension table)

|   Column   |                 description                 |
| ---------- | ------------------------------------------- |
| id         | auto incrementing key                       |
| category   | game category (e.g. Political, Fantasy, ..) |
| game_id    | foreign key: linking to game_details        |


## game_mechanics (dimension table)

|   Column   |                      description                       |
| ---------- | ------------------------------------------------------ |
| id         | auto incrementing key                                  |
| mechanic   | game mechanic (e.g. Auction/Bidding, Dice Rolling, ..) |
| game_id    | foreign key: linking to game_details                   |


## game_family (dimension table)

|   Column   |               description                  |
| ---------- | ------------------------------------------ |
| id         | auto incrementing key                      |
| family     | game family (e.g. Asian Theme, Dragon, ..) |
| game_id    | foreign key: linking to game_details       |


# Files in repository
capstone_project.ipynb
README.md             