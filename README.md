# You and U.S. Research Program: Optimizing Recruitment 

## Overview:
[Google Slides](https://docs.google.com/presentation/d/1137s3_O7ktF4cMPk-cHCNadZev04o0CW/edit?usp=sharing&ouid=103298195738654763321&rtpof=true&sd=true)
This dataset is modeled after recruitment data for an National Institutes of Health (NIH) research program called You and U.S.(de-identified name). You and U.S. is an ambitious research program asking one million or more people from across the country to participate. Participating includes enrolling online and completing an in-person visit at a local site. Participants share a wealth of personal data in an attempt to capture information about the whole person. Data comes from a range of sources including medical records, biosamples, self-reported surveys, and in-person assessments. 

You and U.S. will ultimately be the largest research data and biorepository in U.S. history and will be leveraged to answer future research questions related to personalized medicine. 

As an enrollment location, the ultimate goal is to 'complete' in-person research visits as funding is directly tied to this metric. However, the most efficient approach to achieving this end goal is less clear. The typical process to recruit someone starts with an email invitation. The email is followed up by up to 5 contacts in an attempt to schedule the prospective participant for a research visit. Generally, 10% of those contacted to participate schedule a research visit. Of those that schedule a visit, only 50% go on to complete the in-person visit. 

### Objective of this Analysis:
The goal of this analysis is to determine if there is an identifiable pattern that leads to completion of the research visit. There are a number of questions that we aim to explore in this analysis:
 1. What are the predictors for a completed visit? Age, location, number of follow-up contacts, method of contact?
 2. For phone outreach, is there an ideal time of day to call (when do people answer the phone)?
 3. For completed visits, is there a rank order to days of the week and does this vary by location?

### Data Source:
This data is sourced from the research endeavor at UC Davis Health and has been completely de-identified. No locations or personal information (for staff or particpants) is included in the csv file. Each row has been assigned a random alphanumeric code that is not traceable to any actual data; all physical locations have been coded with numbers. Information regarding the variables is included in an additional csv file located in the Resources folder on github.  
![image](Resources/missing.jpg)

### Dataset From AWS(Cleaned Database):
![image](Resources/coded.jpg)

### Tableau Dashboard:
The project overview will be shown and explained through Google Slides [here.](https://docs.google.com/presentation/d/1137s3_O7ktF4cMPk-cHCNadZev04o0CW/edit#slide=id.p101)
Technical charts and graphs will be created and shared through Tableau.
The first Tableau graph shows you how many people of each age have completed a survey, and you can filter for a specific age range. This graph is now grouped in bins of ten years.

![Age_by_outcome_bins](https://user-images.githubusercontent.com/35434608/201314169-ed785eae-0e89-45cb-b090-049d8fff6194.png)

The second graph shows number of participants by year. You can see a sensible drop off in the year 2020.

![participants_by_year](https://user-images.githubusercontent.com/35434608/201314229-18637b69-5bc2-4227-a4ac-983d5b1fe6ac.png)

The third graph shows number of participants broken down by sex.

![sex_of_participants](https://user-images.githubusercontent.com/35434608/201314265-7125158d-dd89-4216-aa41-cb9af448cb7a.png)

The fourth graph shows the visit outcome broken down by days of the week.

![days_of_the_week](https://user-images.githubusercontent.com/35434608/201314320-f5ff236b-dc2d-437b-9004-567a01a2560b.png)

The fifth graph shows the success and failure rates of different contact methods.

![contact_methods](https://user-images.githubusercontent.com/35434608/201314363-de3e0c81-140f-4ac3-91df-a6a54cfb8086.png)


## Please refer to running_with_ml_code.ipynb for the current working file. 

### Machine Learning Model:
Given that we have an outcome, we expect to use a supervised machine learning model. Further, the outcome is discrete (complete vs. incomplete) and as such, we will use a classification model. Logistic regression is used to solve classification problems. We will start with a Random Forest Classifier model. 

### A summary of our process:
- 1. We started with a significant amount of preprocessing. Mulitple rows existed for the same individual. As such, we aggregated multiple entries for the same individual into a single row containing all relevant information. 
- 2. Next, we used existing column data to calculate new columns in an analyzeable format. This includes calculating the following: a person's age, how far into the future a visit was scheduled, how many times a visit was scheduled, and how many times a person was contacted. This allowed us to investigate who completed a visit and to look at whether mode or frequency impacts show-rate for a visit. 
- 3. Sklearn train test split was used to stratify our data. 
- 4. The Random Forest Model was selected because we had a defined outcome that was discrete. Additionally, Random Forest Classifer models are resilient to being overfit. 
- 5. We tested using an adaboost model but found that the random forest model preformed sligtly better by comparison.
- 6. Ultimately our model had a confidence score of 68%, a precision score of 77% and a recall of 79% which for our uses was sufficient. Our ability to predict successful visits was much higher than our ability to predict for failures. Improving our ability to predict successfully completed visits is the objective of our analysis.
          
### Imbalanced calssification report
![image](Resources/imbalanced_classification_report.PNG)

### Future Analyses: Look at more data and use a Neural Network!
The complete dataset includes more comprehensive demographics: zip code, race/ethnicity, concurrent clinical appointment
#### Ask more questions:
- Look at trends for visits scheduled vs. completed by time of day for visit
- Did the scheduled individual have a concurrent clinical appointment? And how does this influence show-rate?
- Was there a recruitment communication pattern that worked better than another?
- How many contacts are worthwhile? When does the payoff (scheduled visit) diminish (i.e., is it worth making a 4th contact?

### What could we have done differently?
If we had met earlier and taken more time, it would have been worthwhile to choose a project that everyone was curious to learn more and dive into. This project was specific to one individual's profession and thus, perhaps, not as inspiring or motivating for the full group. Our team would have benefited from meeting earlier on in class so we could get to know one another and each other's working style.
