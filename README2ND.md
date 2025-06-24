# Google Data Analytics Capstone The Population of Malaysia
## Introduction
For my Google Data Analytics Capstone project, I choose Case Study 3: Follow your own case study path. For this option, I will perform numerous real-world tasks of a junior data analyst by following the steps of the data analysis process: ask, prepare, process, analyze, share, and act. I will answer the key tasks and the deliverables for each process given in the Case Study 3 packet.

## Data Analysis Process: Ask :question:
The business statement for this capstone is to analyze population trends of Malaysia’s younger population (ages 0–24) from 2014 to 2024 to assess growth and potential demand for child and adolescent healthcare services. This analysis aims to support healthcare planners, private hospitals, and public health stakeholders in developing age-appropriate care models, educational programs, and preventive health strategies.

There are few questions that I would like to focus and explore:
1. How has the population of the 0–24 age group changed between 2010 and 2020?
2. Are any specific age brackets (e.g., 0–4 or 15–19) growing or shrinking?
3. What proportion of Malaysia’s total population does this group make up now vs. 10 years ago?
4. What are the implications for pediatric and adolescent healthcare services?
5. Are there visible effects or trends around COVID-19 (2020) on this age group’s population reporting?

## Data Analysis Process: Prepare :construction_worker:
For this analysis, I will be using the public data available from government agency, the Department of Statistics Malaysia. The link can be found [here](https://open.dosm.gov.my/data-catalogue/population_malaysia). The credibility of this data is high because it was released directly by a government agency. The data contains the population of Malaysia by sex, age group and ethnicity recorded from 1970 to 2024. Once I downloaded the data from the website I move to the next data analysis process.

**Disclaimer:** The format of the data from the original source for population is formatted as **Population('000)**. The format applies for this analysis.

Additionally, I will be using R with the following packages for this analysis.
1. Tidyverse

## Data Analysis Process: Process :factory:

Based on my business statement, this analysis will focused on the younger (0-24) age group from 2014 to 2024. Therefore, I would need to process my data to match the requirement.

#### 1. My first step is to extract the requirement.
First, I need to mutate the date to ensure that the date section is accurately formatted. I'm using the mutate function.
```
data <- data %>%
  mutate(date = as.Date(date)
```
Next, I need to define the specific age group for easy reference. For this analysis, the age group is between 0-24. In order to do so, I'm using the following syntax to define my desired values.
```
young_ages <- c("0-4","5-9", "10-14", "15-19", "20-24")
```
Now, I'm ready to extract the required data for this analysis. I'm using the filter function.
```
young_data <- data%>%
  filter(
    year(date) >= 2014 & year(date) <= 2024,
    sex == "both",
    age %in% young_ages,
    ethnicity == "overall"
  )
```

## Data Analysis Process: Analyze :mag:

In this process, I will be analyzing the data based on the earlier given questions.

#### 1. How has the population of the 0–24 age group changed between 2014 and 2024?
In order to answer the question, I need to summarize the population from the year 2014 to 2024. 
```
question_one <- young_data %>%
  mutate(year = year(date)) %>%
  group_by(year) %>%
  summarise(total_young_population = sum(population, na.rm = TRUE), .groups = "drop")
```
This is the result.
```
# A tibble: 11 × 2
    year total_young_population
   <dbl>                  <dbl>
 1  2014                 13809.
 2  2015                 13848 
 3  2016                 13867.
 4  2017                 13844.
 5  2018                 13810.
 6  2019                 13691.
 7  2020                 13478.
 8  2021                 13379.
 9  2022                 13275.
10  2023                 13385.
11  2024                 13436.
```
In order to calculate any changes in the group age population between 2014 to 2024, I will perform a simple calculation to determine the changes in percentage. To do so, I used the following steps.

I set the values for the population in 2014 and 2024.
```
population_2014 <- question_one$total_young_population[question_one$year == 2014]
population_2024 <- question_one$total_young_population[question_one$year == 2024]
```
Next, I perform a simple calculation and this is the result.
![image](https://github.com/user-attachments/assets/fb0bec89-3b6b-4487-ae23-d61cdc627649)


2. Are any specific age brackets (e.g., 0–4 or 15–19) growing or shrinking?
3. What proportion of Malaysia’s total population does this group make up now vs. 10 years ago?
4. What are the implications for pediatric and adolescent healthcare services?
5. Are there visible effects or trends around COVID-19 (2020) on this age group’s population reporting?
   


#### Summary of analysis
1. The total of population for older adults (aged 60 and above) in Malaysia is steadily increasing.
2. Based on the differences of the older adults total population from year to year, the average growth is around 3.9%.
3. The age group 60-64 is the highest and the age group 85+ is the lowest.
4. A steady increase of population on all age group since 2014.
5. A decline in 2020 on all age group most likely due to the Covid-19 pandemic.

## Data Analysis Process: Share :bar_chart:
For this analysis process, I used Tableau to visualize my findings.

Here is the dashboard for this analysis.
![Dashboard 1](https://github.com/user-attachments/assets/ee32b661-3d13-47f3-b9b9-ea30d1130e72)


For more details and interactive experience using the dashboard, please access it [here](https://public.tableau.com/shared/D27SZSJHY?:display_count=n&:origin=viz_share_link).

## Data Analysis Process: Act :rocket:
### Insights
1. The population of Malaysia is growing and if the trend continues, the group age 60 and above will be a big population in Malaysia.
2. Potentially higher demand on healthcare services especially for older people products and services.
3. Likely to impact workforce for those who struggle financially after retirement.

### Recommendation
1. Government should consider few factors moving forward like healthcare capacity, workforce, budget, and policy around the growth of older generation.
2. Private healthcare should consider scaling up their services.
3. Business should take advantage in providing product and services catering to the older population.

## Thank you :pray:
