# table_R
code to make a function that turn model results into table for microsoft word

I adapted most of these codes from Simon Ejdemyr (https://sejdemyr.github.io/r-tutorials/basics/tables-in-r/). 

Why: 
I want to find a way to automate and standardise reporting results (betas, std error, F statsitic, P-value) in a table. Our research group consistently report those statistics from lme() manually into Word. 

Problem:
When we find an error, we have to run the whole analysis again and change the values manually. 

Solution (hopefully):
Have the function gather the statistic of interest and then bind them in R before inserting the txt file in Word. We can then convert the txt file to table in Word.
