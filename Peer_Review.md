# Visual Data Exploration with Pandas

Group Review: Divya and Ibrahim

Description: What follows is an in-depth analytical review of the discovery learning process as documented by the above mentioned group. This analysis is meant to identify common errors, pandas uses and/or best practices and ultimately serve as a way to rapidly refamiliarize with pandas in the future.

Project Initiation:

    1. Typical project initiation involves environment setup, python library imports, etc. It is important to understand the task ahead in order to know which python libraries might be most useful to your purpose.

    2. Next, the programmer will need to ensure that the project is set up and running on the appropriate version of python, in the correct operating environment, and that the necessary packages are already installed.

    *If anaconda is installed, a simple/quick way to find out which environment is running is to simply enter "conda env" into a terminal. This command can also be entered inside of a Jupyter Notebook by "!conda env". If, for example, you need to create a custom environment for your project, this can be done by "!conda create {some env name} | conda activate {some env name}"

    3. Once the outer environment is appropriately set up, the first steps are to import those libraries into your python file.

    *The simplest/quickest method for determining if the python libraries you require are already installed is to enter "!echo 'y' | conda install {some lib name}"

    Note: It is likely that many libraries you will want to you use are not inherently included in the standard Anaconda library. In this case, it becomes necessary to use a slight different set of commands.

    For example, for installing Sci Kit Learn: "!echo 'y' | conda install -c conda-forge sklearn-contrib-lightning | conda install -c conda-forge/label/cf201901 sklearn-contrib-lightning"
    
    For most, if not all Anaconda library installation information, refer to https://anaconda.org/.

Visual Data Exploration

    CLEANING:

    1. An important piece of information to understand is how your data is organized, if it is labeled or unlabeled, if there are eroneous or duplicate items, etc. With this in mind, the Pandas python library can be very useful in gathering this understanding and then implementing the appropriate algorithms to first clean, then organize, and finally conduct initial analysis to determine how to proceed further in the data analysis process.

    2. Divya and Ibrahim begain by first reading in their data sample from a file provided for the exercise. The data could just as easily from from a URL instead.

    Note: Data files/samples can come in many different formats. Often, they are compressed or "zipped" which makes it difficult to see what exactly is in your data file. An option for doing this is to first unzip/decompress the data file in place and then open it in some text editor to understand if your data is in a tabular format, or delimited by some char or space or tab, etc.

    A way to do this from Jupyter Notebook is to find where the data file is located and then call the appropriate bash commands. For example: let's say that the file I want is zipped and located in a different folder from my project on my machine, the command would be "!unzip /path/to/file/file_name | gedit /path/to/file/file_name". This would unzip the file in place and then open it in a text editor for viewing.

    3. Next, Divya and Ibrahim began by re-labeling their data so as to have better semantic meaning for their purposes. This step can be accomplished simulataneously as the data is read in or as an additional step later. Divya and Ibrahim chose to execute this step separately. For more information on Pandas ".read_ " methods, visit: https://pandas.pydata.org/pandas-docs/stable/reference/io.html.

    Note: The importance of first visually exploring the raw data is so that one can reasonably understand the steps they will need to take in order to have a dataframe which is organized properly and provides the correct semantic meaning for the dat set they are exploring. It can be necessary to separate out the visual exploration step from the Datafram creation step. This will aide in knowing which parameters need to be adjusted during the Datafram initialization process.

    4. The next logical step is to remove any rows where any of the data in the row is either missing or erroneous i.e. when a number is expected but no number is currently occupying the data space within a given column of a given row. Thankfully Pandas provides a neat command       "{Dataframe Name}.dropna()". You can read more about this method here: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dropna.html.

    Note: For most Pandas Library methods, if you want the action to take place in the Dataframe's original space and not create a copy of the Dataframe, the arg "inplace" must be set to True. So,in the case of .dropna() the command would be "{some dataframe name}.dropna(inplace=True)".

    Ibrahim and Divya called the command dropna() without specifying inplace=True and also did not assign the returned dataframe to a new dataframe name, therefore this operation was not retained going forward.

    5. The next operation was to convert the duration series which stored to duration of each movie in minutes to seconds. This can be accomplished in several ways. One of the ways it can be accomplished succinctly is to use a lambda expression on a particular series within a dataframe. This method executes neatly in the original data space while only travering the data set once and it is not necessary for multiple copy operations. Essentially, this takes the time complexity from O(n**(# of copy/math operations)) to O(n). For some example implementations, refer to: https://stackoverflow.com/questions/45593792/can-lambda-expressions-be-used-within-pandas-apply-method or https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html for the official documentation.

    Ibrahim and Divya chose to first split each entry in the duration series and assign that to a new dataframe. Next, they assigned the result of converting each number in the 0th index of the new series within the new dataframe to an int multiplied each by 60s. While this worked well on a relatively small data sample, this will experience slow/poor performance on larger data sets.

    CONCATENATING:

    1. The last phase of this process is to visually see trends in the data sample. To that end, it is necessary to merge various dataframes with simlar contextual meaning so that analyses run on these data don't exclude important facts.

    2. Pandas provides a wealth of options for merging data. One of them is the ".merge" method which you can read about here: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html. Again, programmer preferences matter; I am of the opinion of "why do something in multiple steps at the cost of efficiency/performance; time is money?".

    3. In this exercise Ibrahim and Divya read in two more data sample into two additional dataframes (refer to information above on ".read_ " method(s/ology)).

    4. The meat of this exercise is how to efficiently, and without data compromise, merge multiple dataframes. Ibrahim and Divya effectively executed .merge operations which eliminated eroneous/duplicate data.

    Note: When merging data, pay particular attention to the "how= " parameter in the merge method args. i.e. outer vs inner merge/join operations etc.

    5. Next, data samples where multiple directors were credited with a given movie entry were dropped. Ibrahim and Divya first created a new series where the entries were longer than 9 chars. This separated out the entries where more than one director were credited with a movie's creation. Next they called the pandas ".drop({names > 9}, inplace=True)" method to remove the duplicated information. This process requires 2n memory and time to process vs n.

    6. Lastly in this process, individual persons information were merged into the main dataframe, series names were changed, and unnecessary series were removed now that director names were directly associated with a given movie entry.

    EXPLORATION:

    1. The first instructions were to find the 10 longest duration movies in our dataframe. Ibrahim and Divya chose to first sort their dataframe in place based on the duration series and then display this information in it's entirety. This implementation unnecessarily sorts the dataframe and displays the entire dataframe rather than the top 10.

        Another options for accomplishing this would be to first find the 10 largest duration factors, then use the indeces of those rows to display the top 10 and not sort the entire dataframe. A way to do this is to use a pandas method "{dataframe name}.nlargest()" which you can read about here: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.nlargest.html. This method returns the 10 largest rows based on the series passed as an argument from a given dataframe. Thus, no sorting, copying etc.

    2. The next task was to find the best rated movies ordered by rating DESC and title ASC. At first glance, this may seem like it can be accomplished exactly as the step before, and, for the most part it can with one caveat; the returned results need to be sorted in this fashion: First, the overall list is displayed in descending rating numerical order, when two entries have the same rating, they will be displayed in alphabetical ascending order. Ibrahim and Divya sorted the dataframe according to the instructions using the pandas ".sort_values()" method which you can read more about here: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_values.html. Ultimately, this may not be very useful information for data extrapolation but it is good to have experience with as many Pandas tools as possible.

    3. The next task was to find the average duration (in minutes) of a movie. This doesn't make sense as a given movie would only have one duration. However, Ibrahim and Divya made an assumption that the exercise author meant the average duration of all movies. This task can be quickly accomplished with "{dataframe name}['series name'].mean()/60 (since movie durations had been converted to seconds). Ibrahim and Divya implemented this method and assigned it to a variable, then called that variable to display the value. The assignment portion, in this case is unnecessary.

    4. The next task was to find the top ten most productive directors. This can be easily accomplished using "{dataframe name}['series name'].value_counts()[:10]" since we only need the top 10.

    5. The next task was to count how many movies were made in the 2000's. For this step, the instructions are a bit vague. As I understood these instructions, we wanted to count the numer of movies created in the range 2000 - 2010. This task can be easily accomplished by again using the "value_counts()" method and applying some pandas filters. However, Ibrahim and Divya approached this problem in a slightly different way. First, they used the .apply method to place boolean values in place of the numerical values based on the numerical value being == 2000. This means that only the rows with the year series element == 2000 will have True inside those cells. This means that later the other year counts for 2001 - 2009 will be excluded. Next they assigned the number of "True" entries to a variable and then displayed that value. While this works, again, on large data samples, this may experience poor performance given the additional steps.

    6. The final task in this exercise was to display all of the movies directed by Akira Kurosawa displayed in descending order by year. This task can be accomplished by "{dataframe name}['director'].sort(by='year', ascending=False)". Howevery Ibrahim and Divya chose to break this process up into two steps where they assigned only the rows with the correct director to a new dataframe, they then sorted that datafram appropriately.
