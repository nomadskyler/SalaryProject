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


The following function returns descriptive statistics of the initial dataframe. Our target variable is 'Salary.'

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

