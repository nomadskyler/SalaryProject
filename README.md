# SalaryProject

DEFINE

If you're a fresher just completing a degree program from college or university you might want to know what salaries the job market has to offer. Let us find what features in the dataset are most correlated to a description's salary to help understand what goals we need to work on in the real world.

DISCOVER

Let's now understand the type of file, types of data, and anything else to help us better describe what we are about to work with. We are working with a .csv file with a million rows of data to start.


The following function returns a concise summary. 7/10 features are categorical while 3/10 are numerical.

train_df.info()

RangeIndex: 1000000 entries, 0 to 999999
Data columns (total 10 columns):
jobId                  1000000 non-null object
companyId              1000000 non-null object
jobType                1000000 non-null object
degree                 1000000 non-null object
major                  1000000 non-null object
industry               1000000 non-null object
yearsExperience        1000000 non-null int64
milesFromMetropolis    1000000 non-null int64
jobId                  1000000 non-null object
salary                 1000000 non-null int64
dtypes: int64(3), object(7)


The following function returns descriptive statistics of a feature. Our target variable is 'Salary.'

train_df.Salary.describe()

count    1000000.000000
mean         116.061818
std           38.717936
min            0.000000
25%           88.000000
50%          114.000000
75%          141.000000
max          301.000000
Name: Salary, dtype: float64


Now let's look for correlation between features and the target. For now we are only interested in the type of job.


The following function returns an array with each 'Type' of job description. Following the function is a dictionary created listing each unique job type's average salary. Finally the target's average is printed for comparison.

np.unique(train_df.Type)

array(['CEO', 'CFO', 'CTO', 'JANITOR', 'JUNIOR', 'MANAGER', 'SENIOR',
       'VICE_PRESIDENT'], dtype=object)

{'JANITOR': '$71,000', 'JUNIOR': '$95,000', 'SENIOR': '$105,000', 'MANAGER': '$115,000', 'VP': '$125,000', 'CTO': '$135,000', 'CFO': '$135,000', 'CEO': '$145,000'}
Average target: '$116,000'


Now we can build some assets to gain insight.


The following function is defined to return two visualizations. The first visualization plots the counts of the unique values or splits the unique values into groups in the dataframe for the selected feature. The second visualization groups the mean salary by the selected feature chosen or uses the wrangled dataframe from the previous visualization to accurately plot a box and whisker plot.

def make_plots( df , col):
    
    plt.figure( figsize = ( 14 , 6 ) )
    plt.subplot( 1 , 2 , 1 )
    
    #fill first plot
    
    if df[ col ].dtype == 'int64':
        
        #find count of all unique values in the index
        #sort dataframe based on index lables
        #plot feature
        df[ col ].value_counts().sort_index().plot()
        
    else:
        
        #split data into group based on input parameter
        #select columns included in new df
        #find mean of each column index
        mean = df.groupby( col )[ 'Salary' ].mean()
        
        #change objects to categorical features
        df[ col ] = df[ col ].astype( 'category' )
        
        #find indeces of sorted values
        sort_mean = mean.sort_values().index.tolist()
        
        #reorder categories per sorted indeces
        df[ col ].cat.reorder_categories( sort_mean , inplace = True )
        
        df[ col ].value_counts().plot()
        
    plt.xticks( rotation = 45 )
    plt.xlabel( col )
    plt.ylabel( 'Counts' )
    
    #fill second plot 
    
    plt.subplot( 1 , 2 , 2 )
    
    if df[ col ].dtype == 'int64':
        
        #split data into group based on input parameter
        #select columns included in new df
        #find mean of each column index
        mean = df.groupby( col )[ 'Salary' ].mean()
        
        mean.plot()
    
    else:
        
        sns.boxplot( x = col , y = 'Salary' , data = df)
        
    plt.xticks( rotation = 45 )
    plt.ylabel( 'Salaries' )


