# Demographic_Analysis using python

## Table Of Content
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaning/preparation)
- [Data Analysis](#data-analysis)




  
### Project Overview

This data analysis project aims to provide demographic insight on a particular region. By analyzing various aspect of demographic data we seek to identify race, education, salary of 
particular groups in certain region.

### Data Sources
Demographic data: The primary dataset used for this analysis is "freecodedata.txt" file, containing detailed information about the demograph of certain region.

### Tools
-  Excel - Data cleaning  [download_here]()
-  Python - Data analysis and visualization
-  Jupyter notebook - Used to code 

### Data Cleaning/Preparation
In the intial data preparation phase, we did the following task;
1. Data loading and inspection
2. Handling missing values
3. Data cleaning and formatting

### Exploratory Data Analysis
EDA involved exploring the demographic datato answer key questions, such as;

- How many people of each race are represented in this dataset?

- What is the average age of men?

- What is the percentage of people who have a Bachelor's degree?

- What percentage of people with advanced education (Bachelors, Masters, or Doctorate) make more than 50K?

- What percentage of people without advanced education make more than 50K?

- What is the minimum number of hours a person works per week?

- What percentage of the people who work the minimum number of hours per week have a salary of more than 50K?

- What country has the highest percentage of people that earn more than 50K and what is that percentage?

- Identify the most popular occupation for those who earn more than 50K in India.

### Data Analysis
Include some code

```python
import pandas as pd
import matplotlib.pyplot as plt

def demographic_analyzer():
    url = "freecodedata.txt"
    df = pd.read_csv(url)
    df.columns = ['age','workclass', 'fnglwgt','education', 'education_num', 
                 'marital-status', 'occupation', 'relationship', 'race', 'sex',
                'capital-gain', 'capital-loss', 'hours-per-week', 'native-country', 'salary' ]
    
    race = df['race'].value_counts()
    
    population_men = df[df['sex']== df['sex'][0]]
    average_men_age = round(population_men['age'].mean(),1)
    
    
    people_bachelors = df[df['education'] == df['education'][0]]
    percentage_bachelors = round((len(people_bachelors)/len(df)) * 100,1)
    
    advance_education = df[(df['education'] == df['education'][0]) |
                          (df['education'] == df['education'][7]) |
                          (df['education'] == df['education'][19])]                      
    advance_rich = df[(df['salary'] == df['salary'][8]) &
                           ((df['education'] == df['education'][0]) |
                          (df['education'] == df['education'][7]) |
                          (df['education'] == df['education'][19]))]
    percentage_advance_rich = round((len(advance_rich) / len(advance_education)) * 100,1)
    
    non_advance_education = df[(df['education'] != df['education'][0]) &
                          (df['education'] != df['education'][7]) &
                          (df['education'] != df['education'][19])]
    non_advance_rich = df[(df['salary'] == df['salary'][8])&
                          ((df['education'] != df['education'][0]) &
                          (df['education'] != df['education'][7]) &
                          (df['education'] != df['education'][19]))]
    percentage_non_advance_rich = round((len(non_advance_rich) / len(non_advance_education)) * 100,1)
  
    minimum_hour_per_week = df['hours-per-week'].min()
    
    min_hour = df[df['hours-per-week'] == minimum_hour_per_week]
    min_hour_rich = min_hour[min_hour['salary'] == min_hour['salary'][188]]
    percentage_min_hour_rich = round((len(min_hour_rich) / len(min_hour)) * 100,1)
    
    rich_country = df[df['salary'] == df['salary'][8]]
    richest_country = (rich_country['native-country'].value_counts()) / (df['native-country'].value_counts()) * 100
    richest_country = richest_country.sort_values(ascending = False )
    richest_earning_country = richest_country.index[0]
    percentage_richest_country = richest_country[0]
    data = race, average_men_age, percentage_bachelors, percentage_advance_rich, percentage_non_advance_rich, minimum_hour_per_week, percentage_min_hour_rich, richest_earning_country ,percentage_richest_country.round(1) 
  
    top_IN_occupation = df[df['native-country'] == df['native-country'][10]]
    top_IN_occupation = top_IN_occupation['occupation'].value_counts()
    top_IN_occupation = top_IN_occupation.index[0]
    return top_IN_occupation

demographic_analyzer()

```

### Result / findings





### Recommendation





### Limitation
