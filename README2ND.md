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

#### 2. Next, I need the data for the specific age group. For this analysis, I need the older adult (aged 60 and above). Therefore, I filtered only the necessary age group which are 60-64, 65-69, 70-74, 75-79, 80-84, 85+.


## Data Analysis Process: Analyze :mag:

In order to analyze the population trend on the older adults (aged 60 and above) in Malaysia, I have to perform several calculations to make sense of the data.

#### 1. The total population on the older adults (aged 60 and above) from 2014-2024
By using the following query, I am able to calculate the total population of the older adults (aged 60 and above) of each year.
![sql_data_analysis_01](https://github.com/user-attachments/assets/395dcb0e-079a-472a-bb17-2fa55825bd6a)

The result.
![data_data_analysis_01](https://github.com/user-attachments/assets/2c0e3713-8455-4508-9ca8-3b0f3bb3f1c9)

#### 2. The differences of the older adults (aged 60 and above) total population from year to year
I want to see if there are any trends or changes on the total population of each year. To analyze this I first need to calculate the differences and the percentages for each year. The query is as follow:
![sql_data_analysis_02](https://github.com/user-attachments/assets/ec2cf789-b4f1-42b8-acd7-a74652dd8576)

The result.
![data_data_analysis_02](https://github.com/user-attachments/assets/98564e34-6a28-497c-bcf5-122a9a11e3f4)

#### 3. The population of the older adults (aged 60 and above) by groups for each year
I also want to see if there are any trends or patterns on the population by age groups for each year. I use the following query to find out:
![sql_data_analysis_03](https://github.com/user-attachments/assets/be0823ce-d344-498e-994a-24594eeb3d5d)

The result.
![data_data_analysis_03](https://github.com/user-attachments/assets/c1345677-0db9-4ce0-82a7-00ee28422593)

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
