

```


When going through the program we came across various issues, some were easy and some proves to be challenging. The modules given for the exercise were Basic info, Cleaning, Concatenating, Exploration. Following is the review of each module.

1.) The file df, crew_data, movie_data and name_data are in format of tab seperated files. So there are two ways to read these
    files. The read_csv and read_table both provide output. Thus it depends on user to how to read file.
    
2.) The renaming of the column can be done in various ways. You can use the different cell to remane the column or the same cell       in which you define the name of data frame using '&' symbol. Advantage of this is the less memory usage and more speed.

3.) In the cleaning section the conversion of the duration from minutes into seconds will provide you with some challenges. The 
    used way is to slice off the 'mins.' element from the value of the element of column and then multiply the number by 60.
    
4.) Merging the dataframe can be done with two dataframe having the same or different name of columns. If the dataframes to be         merged have same column name then simply use the merge command with that column. However if you face the data frame with           different column names then specify the right and left column of the dataframe.

5.) The nlargest function prove to be challenging to figure out. However it is really easy to find the output using it.

6.) The sort_values is another intresting function which can be used in various sorting problems. It helped to sort the table of 
    dataframe according to the requirements.
    
    
After going through the exercise we were able to know various new functions and their uses as well. We were also able to compare the commands used by us to see what can be the better way.




```
