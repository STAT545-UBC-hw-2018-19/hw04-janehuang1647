This is Zhenyi Huang's repository for Stat 545 Assignment 4 Tidy Data and Joins
===

For simple reshaping, the following functions from **tidyr** are the following:

tidyr Function | Definition
----------------|------------------
   `gather`      | takes multiple columns and collapses into key values pairs
   `spread`       |  Spread a key-value pair across multiple columns

for better domenstration of these two functions, please check:
[**Data Reshaping**](https://github.com/STAT545-UBC-students/hw04-janehuang1647/blob/master/assignment_4.md#exploring-gather-and-spread-for-data-reshaping) 
The prompt that I have attempted in this part is activity 2. In this activity, I have again explored the gapminder database and the required tables and plots are generated.

To join database together, the following function could be used.

join function  | filter join function
---------------|----------------------
 `left_join`  |     `semi_join`
 `right_join`  |   `anti_join`
 `anti_join`  |
   `inner_join`  |
   `full_join`|
   
For the join functions, the prompt that I have attempted is activity 1. A new data frame with extra column on spoken language is created and then this joined with the gapminder data frame using different join functions. The results and its explanation are presented here: [**Join Function**](https://github.com/STAT545-UBC-students/hw04-janehuang1647/blob/master/assignment_4.md#join-prompts-join-merge-look-up) 
