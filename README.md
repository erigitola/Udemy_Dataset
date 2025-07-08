# Udemy Online Education Courses - Exploratory Data Analysis

# Project Objectives:
# - Understand trends in Udemy's online course offerings.
# - Analyze relationships between reviews, subscribers, price, and levels.
# - Visualize data to support insights.

# Importing Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

#Set plot style
sns.set(style='whitegrid')
plt.rcParams['figure.figsize'] = (10,6)

# Loading the Dataset
df = pd.read_csv('udemy_courses.csv')

# Initial Exploration
df.head()

# Check data types and missing values
df.info()

# Check statistics summary
df.describe()

# Check missing values
df.isna().sum()

# Count uniques values
df.uniques()

#Count duplicates rows
df.duplicated().sum()

# Shows first 5 rows
df.head(5)

# Rows and columns count
df.shape

# Columns names
df.columns


import pandas as pd
df = pd.read_csv('/kaggle/input/udemy-online-education-courses/udemy_online_education_courses_dataset.csv')
import matplotlib.pyplot as plt
import seaborn as sns

import warnings
warnings.filterwarnings('ignore')


f['subject'].value_counts()

business_finance_counts = df[df['subject'] == 'Business Finance'].shape[0]
graphic_design_counts = df[df['subject'] == 'Graphic Design']['course_id'].shape[0]
musical_instruments_counts = df[df['subject'] == 'Musical Instruments']['course_id'].shape[0]
web_development_counts = df[df['subject'] == 'Web Development']['course_id'].shape[0]
from matplotlib.cm import get_cmap
cmap = get_cmap("Blues")
colors = cmap([0.4, 0.5, 0.6, 0.7])
explode = [0.1,0,0,0.1]

plt.figure(figsize=(10,6))

index_values = [business_finance_counts, graphic_design_counts, musical_instruments_counts, web_development_counts]
index_labels = ['Business Finance', 'Graphic Design','Musical Instruments','Web Development']

plt.pie(index_values, labels = index_labels, autopct='%2.2f%%', explode=explode, shadow=True)

plt.title('Overall Subject Distribution of Courses', fontsize=16)


# find total subscribers for each subject 
subscribers_by_subject = df.groupby('subject')['num_subscribers'].sum().reset_index()
subscribers_by_subject

plt.figure(figsize=(10,6))

plt.xlabel("Subject", fontsize=20)
plt.ylabel("Subscribers", fontsize=20)

sns.barplot(data=subscribers_by_subject, x="subject", y="num_subscribers", palette='pastel', edgecolor='black')

plt.title("Number of Subscribers per Subject", fontsize=16)
plt.xlabel("Subject", fontsize=12)
plt.ylabel("Subscribers", fontsize=12)


business_finance_counts = df[df['subject']=='Business Finance']['num_subscribers'].sum()
graphic_design_counts = df[df['subject']=='Graphic Design']['num_subscribers'].sum()
musical_instruments_counts = df[df['subject']=='Musical Instruments']['num_subscribers'].sum()
web_development_counts = df[df['subject']=='Web Development']['num_subscribers'].sum()

explode = [0.05,0.05,0.05,0.1]

plt.figure(figsize=(10,6))

index_values = [business_finance_counts, graphic_design_counts, musical_instruments_counts, web_development_counts]
index_labels = ['Business Finance', 'Graphic Design','Musical Instruments','Web Development']

plt.pie(index_values, labels = index_labels, autopct='%2.2f%%', explode=explode, wedgeprops={'width':0.8}, 


# boxplot for course distribution
plt.figure(figsize=(16,10))
sns.boxplot(x=df['num_subscribers'], color='goldenrod')
plt.title('Boxplot Course Subscribers', fontsize=16)
plt.xlabel('Subscribers', fontsize=12)
plt.show()


from datetime import datetime
df['published_timestamp'] = pd.to_datetime(df['published_timestamp'])
df['date_published'] = df['published_timestamp'].dt.date
df['month'] = df['published_timestamp'].dt.month
df['year_month'] = df['published_timestamp'].dt.strftime('%Y-%m')
year_month = df.groupby('year_month').size()
df.head(1)
plt.figure(figsize=(16,10))
year_month.plot(linewidth=2, color='blue')
plt.title('Number of New Courses per Month', fontsize=16)
plt.xlabel('Year-Month', fontsize=12)





price_grouped = df.groupby('price')['course_title'].count().reset_index()
price_grouped.columns = ['price', 'num_of_courses']
sorted = price_grouped.sort_values(by='num_of_courses',ascending=False)

plt.figure(figsize=(16, 10))


sns.barplot(data=sorted, x='num_of_courses', y='price', palette='plasma', orient='h')  # Swap x and y
plt.title("Distribution of Prices", fontsize=16)
plt.xlabel("Number of Courses", fontsize=12)
plt.ylabel("Price", fontsize=12)
plt.show()

# verifying free courses
free_courses = df[df['is_paid'] == False]
free_course_count = free_courses['course_title'].count()
print(free_course_count)


level_count = df['level'].value_counts().reset_index()
plt.figure(figsize=(10,6))
sns.barplot(level_count, x='level',y='count', palette='pastel')
plt.xlabel('Level', fontsize=12)
plt.ylabel('Number of Courses', fontsize=12)
plt.title('Distribution of Course Difficulty', fontsize=16)


# content duration
grouped_duration = df.groupby('content_duration').size()
grouped_duration_sorted = grouped_duration.sort_values(ascending=False)
grouped_duration_sorted.head(5)



# Scatterplot of content duration and subscribers 
plt.figure(figsize=(16,10))
custom_markers = {True: 'o', False: 'X'}
sns.relplot(data=df, y='num_subscribers',x='content_duration',hue='is_paid', style='is_paid', markers=custom_markers)
plt.xlabel('Content Duration', fontsize=12)
plt.ylabel('Number of Subscribers', fontsize=12)
plt.title('Scatterpllot of Content Duration and Subscribers')



plt.figure(figsize=(10,6))
sns.regplot(data=df, x='num_reviews', y='num_subscribers', scatter_kws={'alpha':0.5}, line_kws = {'color':'red'})
plt.xlabel('Number of Reviews', fontsize=12)
plt.ylabel('Number of Subscribers', fontsize=12)
plt.title('Regression Plot of Reviews and Subscribers', fontsize=16)



# correlation map between quantitative variables and number of subscribers
# converted ordinal categorized data into a scale
# removed outliers using IQR method 


quantitiave_data = ['price', 'num_reviews','num_lectures','num_subscribers', 'content_duration','published_timestamp', 'level']
corr_matrix = df1[quantitiave_data].corr()
plt.figure(figsize=(10,6))
sns.heatmap(corr_matrix, annot=True, cmap = 'Blues',fmt='.2f')
plt.show()






