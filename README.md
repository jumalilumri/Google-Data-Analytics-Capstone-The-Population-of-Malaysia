# Google Data Analytics Capstone The Population of Malaysia
## Introduction
For my Google Data Analytics Capstone project, I choose Case Study 3: Follow your own case study path. For this option, I will perform numerous real-world tasks of a junior data analyst by following the steps of the data analysis process: ask, prepare, process, analyze, share, and act. I will answer the key tasks and the deliverables for each process given in the Case Study 3 packet.

## Data Analysis Process: Ask :question:
The business statement for this capstone is to analyze population trends of older adults (aged 60 and above) in Malaysia from 2014 to 2024 to assess the growth of the aging segment and evaluate potential healthcare demands. The insights aim to support public and private healthcare providers in planning for geriatric care services, chronic disease management, and senior-focused health policies.

## Data Analysis Process: Prepare :construction_worker:
For this analysis, I will be using the public data available from government agency, the Department of Statistics Malaysia. The link can be found [here](https://open.dosm.gov.my/data-catalogue/population_malaysia). The credibility of this data is high because it was released directly by a government agency. The data contains the population of Malaysia by sex, age group and ethnicity recorded from 1970 to 2024. Once I downloaded the data from the website I move to the next data analysis process.

**Disclaimer:** The format of the data from the original source for population is formatted as **Population('000)**. The format applies for this analysis.

## Data Analysis Process: Process :factory:

Based on my business statement, this analysis will focused on the older adults (aged 60 and above) age group from 2014 to 2024. Therefore, I would need to process my data to match the requirement.

#### 1. My first step is to extract the requirement.
![sql_data_preparation](https://github.com/user-attachments/assets/68aba32b-bada-4a03-b12e-537086289abb)

In this step, I extract the required year which is from 2014 to 2024. I also populate only require both for sex and overall for ethnicity because my focus is on the age group.

After running the query, this is how it looks like.
![data_data_preparation](https://github.com/user-attachments/assets/c12e8fae-801d-49ff-ba5a-d22a6a3c2048)

#### 2. Next, I need the data for the specific age group. For this analysis, I need the older adult (aged 60 and above). Therefore, I filtered only the necessary age group which are 60-64, 65-69, 70-74, 75-79, 80-84, 80+.
![sql_data_preparation_02](https://github.com/user-attachments/assets/5c4ff01e-a790-4724-a6c0-2f13e6a2a94f)

After filtering, this is the data that I will be working with.
![data_data_preparation_02](https://github.com/user-attachments/assets/3140aa0c-7ad3-4168-84dc-6a35c96555f0)

Let's move on to the next analysis process so the data can be more useful and meaningful.

## Data Analysis Process: Analyze :mag:

In order to analyze the population trend on the older adults (aged 60 and above) in Malaysia, I have to perform several calculations to make sense of the data.

#### 1. The total population on the older adults (aged 60 and above) from 2014-2024
By using the following query, I am able to calculate the total population of the older adults (aged 60 and above) of each year.
![sql_data_analysis_01](https://github.com/user-attachments/assets/395dcb0e-079a-472a-bb17-2fa55825bd6a)

The result.
![data_data_analysis_01](https://github.com/user-attachments/assets/35dc6d53-1559-4b0b-8b4b-a2c5c15c4bb4)

#### 2. The differences of the older adults (aged 60 and above) total population from year to year
I want to see if there are any trends or changes on the total population of each year. To analyze this I first need to calculate the differences and the percentages for each year. The query is as follow:
![sql_data_analysis_02](https://github.com/user-attachments/assets/ec2cf789-b4f1-42b8-acd7-a74652dd8576)

The result.
![data_data_analysis_02](https://github.com/user-attachments/assets/18dbcfa9-981b-4601-a20e-5820d9a65c2b)

#### 3. The population of the older adults (aged 60 and above) by groups for each year
I also want to see if there are any trends or patterns on the population by age groups for each year. I use the following query to find out:
![sql_data_analysis_03](https://github.com/user-attachments/assets/be0823ce-d344-498e-994a-24594eeb3d5d)

The result.
![data_data_analysis_03](https://github.com/user-attachments/assets/f6e195cf-e384-46ec-b711-e36b14c1984e)


#### Summary of analysis


### Deliverables
A summary of your analysis

## Data Analysis Process: Share :bar_chart:
### Key Tasks
* Determine the best way to share your findings.
* Create effective data visualizations.
* Present your findings.
* Ensure your work is accessible.

### Deliverables
Supporting visualizations and key findings

## Data Analysis Process: Act :rocket:
### Key Tasks
* Create your portfolio.
* Add your case study.
* Practice presenting your case study to a friend or family member.

### Deliverables
Your top high-level insights based on your analysis
Based on what you discover, a list of additional deliverables you think would be helpful to include for further exploration

## Thank you :pray:
