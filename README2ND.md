# Google Data Analytics Capstone The Population of Malaysia
## Introduction
For my Google Data Analytics Capstone project, I choose Case Study 3: Follow your own case study path. For this option, I will perform numerous real-world tasks of a junior data analyst by following the steps of the data analysis process: ask, prepare, process, analyze, share, and act. I will answer the key tasks and the deliverables for each process given in the Case Study 3 packet.

## Data Analysis Process: Ask :question:
The business statement for this capstone is to analyze population trends of Malaysia’s younger population (ages 0–24) from 2014 to 2024 to assess growth and potential demand for child and adolescent healthcare services. This analysis aims to support healthcare planners, private hospitals, and public health stakeholders in developing age-appropriate care models, educational programs, and preventive health strategies.

There are few questions that I would like to focus and explore:
1. How has the population of the 0–24 age group changed between 2014 and 2024?
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
In order to answer the question, I need to summarize the young age group population from the year 2014 to 2024. 
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
In order to calculate any changes in the young age group population between 2014 to 2024, I will perform a simple calculation to determine the changes in percentage. To do so, I used the following steps.

I set the values for the population in 2014 and 2024.
```
population_2014 <- question_one$total_young_population[question_one$year == 2014]
population_2024 <- question_one$total_young_population[question_one$year == 2024]
```
Heres is the result.
![image](https://github.com/user-attachments/assets/fb0bec89-3b6b-4487-ae23-d61cdc627649)

Next, I need to perform a simple calculation to identify the difference in percentage.
```
percent_change <- (population_2024 - population_2014) / population_2014 * 100
```

Here is the result.
![image](https://github.com/user-attachments/assets/f19dd08c-77de-410c-8b56-41d775cae381)

From the result it shows that the young age group population declined 2.70% after rounding.


#### 2. Are any specific age brackets (e.g., 0–4 or 15–19) growing or shrinking?
To answer this questions, I need to calculate the total population based on year and age group.
First, I summarize the total for each age group by year.
```
age_trends <-young_data %>%
  mutate(year = lubridate::year(date)) %>%
  group_by(year,age) %>%
  summarise(total_population = sum(population, na.rm = TRUE), .groups = "drop")
```
By using the View command, this is the result.
![image](https://github.com/user-attachments/assets/176da131-d325-4535-8eaf-273c4ad403d4)

Next, I need to compare the young age group population from the year 2014 to 2024. First, I extract the required data from the year 2014 and 2024.
```
age_2014 <- age_trends %>% filter(year == 2014)
age_2024 <- age_trends %>% filter(year == 2024)
```
Then, I use the table join function and calculate the difference in percentage.
```
question_two <- age_2014 %>%
  inner_join(age_2024,by = "age", suffix = c("_2014", "_2024")) %>%
  mutate(
    percent_change = (total_population_2024 - total_population_2014) / total_population_2014 * 100
  )
```
I used the View command to show the result.
![image](https://github.com/user-attachments/assets/deef45c9-bfe0-4e22-a331-6471095bfc6c)

From the result, it shows that the young age group population of 0-4, 10-14,15-19,20-24 are shrinking. While the young age group population of 5-9 is growing.


#### 3. What proportion of Malaysia’s total population does this group make up now vs. 10 years ago?
In order to answer this question, there are several steps that I need to complete.

First, I need to find out the total population of Malaysia for the year of 2014 and 2024. In order to do that, I add a year column for easier observation using the following method.
```
population_by_year <- data %>%
  mutate(date = as.Date(date),
         year = lubridate::year(date))
```
Here is the result.
![image](https://github.com/user-attachments/assets/6c3540a8-8905-4268-aa26-d71cf52f9db3)

Next, I sum the total population for each year by filtering the sex, age and ethnicity.
```
total_pop <- population_by_year %>%
  filter(sex == "both", age == "overall", ethnicity == "overall") %>%
  group_by(year) %>%
  summarise(total_population = sum(population, na.rm = TRUE), .groups = "drop")
```
Here is the result.
![image](https://github.com/user-attachments/assets/656ecb85-9030-4d49-993c-4095a142753e)

Now, I need to find the total of young population for each year. The step is similar to the answer for question #1. 

Defining the young population.
```
young_ages <- c("0-4","5-9", "10-14", "15-19", "20-24")
```
Then, filter the target range for the young population only.
```
young_pop <- population_by_year %>%
  filter(sex == "both", ethnicity == "overall", age %in% young_ages) %>%
  group_by(year) %>%
  summarise(young_population = sum(population, na.rm = TRUE), .groups = "drop")
```
Here is the result.
![image](https://github.com/user-attachments/assets/1680d7f4-fb94-4d1e-bb25-df0642af30c5)

Next, I need to join the tables and compute the proportion for each year.
```
proportion_df <- young_pop %>%
  inner_join(total_pop, by = "year") %>%
  mutate(proportion = round((young_population / total_population) *100,2))
```
Here is the result.
![image](https://github.com/user-attachments/assets/1dd814ad-a07a-4a19-a309-c87e60531969)

The final step, I extract the proportion for the year 2014 and 2024 to answer the question.
```
proportion_df %>%
  filter(year %in% c(2014,2024))
```

Here is the answer.
```
# A tibble: 2 × 4
   year young_population total_population proportion
  <dbl>            <dbl>            <dbl>      <dbl>
1  2014           13809.           30708.       45.0
2  2024           13436.           34059.       39.4
```
Based on the result, the proportion of the young population of Malaysia in Malaysia in 2024 is 39.4%. While in 2014, the proportion of young population was 45.0%.

4. What are the implications for pediatric and adolescent healthcare services?
5. Are there visible effects or trends around COVID-19 (2020) on this age group’s population reporting?
   


#### Summary of analysis
1. The total of population for young age group (0-24) population in Malaysia has declined 2.70% between the year 2014 to 2024.
2. The young age group of 0-4 population shows the highest decline of 8.2%. Meanwhile, the young age group of 5-9 populations shows small inclination of 1.45%.
3. The proportion of young population in Malaysia has decreased by 5.6% between the year 2014 to 2024.

## Data Analysis Process: Share :bar_chart:
For this analysis process, I used the ggplot function available in the Tidyverse package. 

#### Question 1
To generate the visualization for the first question. I use the following command.
```
ggplot(question_one, aes(x = year, y = total_young_population)) +
  geom_line(color = "seagreen", size = 1.2) +
  geom_point(color = "darkgreen", size = 2) +
  scale_y_continuous(limits = c(0, 30000), expand = c(0, 0)) +
  labs(
    title = "Population Trend of Age Group 0–24 in Malaysia (2014–2024)",
    x = "Year",
    y = "Total Population (Ages 0–24) '000"
  ) +
    annotate(
      "text",
      x = 2019,
      y = 20000,
      label = percent_change_label,
      size = 4.5,
      color = "black",
      hjust = 0
    ) +
  theme_minimal()
```
Here is the result.
![image](https://github.com/user-attachments/assets/494a0de6-3141-4718-9eeb-0513f48711f8)

#### Question 2
To generate the visualization for this question, I used the following command.
```
ggplot(question_two, aes(x = age, y = percent_change, fill = percent_change)) +
  geom_col() +
  labs(
    title = "Percent Change in Population by Age Group (2014-2024)",
    x = "Age Group",
    y = "Percent Change (%)"
  ) +
theme_minimal()
```
Here is the result.
![image](https://github.com/user-attachments/assets/94e2c477-3517-48f8-b27a-0ddb31fcf151)

### Question 3

## Data Analysis Process: Act :rocket:
### Insights
1. 

### Recommendation
1. 

## Thank you :pray:
