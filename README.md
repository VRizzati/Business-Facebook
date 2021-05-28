# HATE CRIME MAPS BY FACEBOOK DATA FOR GOOD
Valentina Rizzati <br/>
May 28, 2021 <br/>
Metis: Business Fundamentals <br/>

## ABSTRACT
The year 2020, amongst orther things, was also a year of general awakening to the deeply problematic issues impairing the social fabric of the United States. One of the most prominent of these issues is hate - hate against different races, sexual orientations, genders, religions or other grounds.

Hate crimes in the United States are characterized by major underreporting both by victims and witnesses and by a significant lack of tracking, and therefore data, at the governmental level. Also, as we noticed in the past year, individuals now tend to share and report instances of hate crime on social media - representing a huge behavioral shift with respect to the past. This presents a compelling opportunity for a big tech firm like Facebook which - even in an unstructured way - collects way more data than the police on hate crimes. 

In the wake of the passing of the AAPI Bill and mindful of the greatly positive impact already created by Facebook's Disaster Maps, I have decided to put forward a new product idea: the creation of Hate Crime Maps. 

My impact hypothesis is that by identifying insights and trends in hate crimes, Facebook will collaborate with government and NGOs to support first responders in the appropriate resource allocation to fight hate crimes. 

## DATA

I have collected data on hate crime in NYC:
- Jan 2019 - Mar 2021: [City of New York](https://data.cityofnewyork.us/Public-Safety/NYPD-Hate-Crimes/bqiq-cu78)
- Jan 2017 - Dec 2019: [NYC Gov](https://www1.nyc.gov/site/nypd/stats/reports-analysis/hate-crimes-archive-2017.page)

Additionally, I have collected data on precinct addresses on [NYC Gov](https://www1.nyc.gov/site/nypd/bureaus/patrol/precincts-landing.page).

The Jan 2019 - Mar 2021 dataset consists of 832 rows (hate crime complaints in NYC) and several columns as elements characterizing the complaint (e.g. Arrest ID).

The Jan 2017 - Dec 2019 data consists of three main tables:
- table of 231 rows (unique by year and precinct number) presenting the count of complaints by bias motive per precinct per year
- table of 231 rows (unique by year and precinct number) presenting the count of murder and felony assaults per precinct per year
- table of 418 rows (hate crime arrestees in NYC) presenting attributes (e.g. gender) of the individuals arrested for a hate crime

The precinct address dataset reports the address for every NYPD precinct.

## DESIGN

As a first step, I have cleaned and explored the data on Google Sheets. See my work [here](https://docs.google.com/spreadsheets/d/1xgUaUFrYza1ZxL4bKAzrVbhHiHSxZJBO2TWrZAxdAAo/edit?usp=sharing). <br/>
During this phase I have used the Google API (geopy) to collect latitude and longitude for the precincts' addresses. Then, I have pivoted the Jan 2019 - Mar 2021 table and created a new table called *NYC_precinct_crimes* that served as the source for the hate crime maps.

In parallel, I have consolidated the yearly hate crime tables for the period 2017-2019, which served as the source for the *Precinct Profile | Hate Crime Arrests (2017-2019)* dashboard.

## ALGORITHM

As part of the data manipulation step, I have applied some feature engineering and created four new metrics:
- Time to Arrest: difference between the arrest date and the complaint date.
- Crime Level: classified as "Needs Addressing" (i.e. High) if the count of offences is greater than the 50th percentile for a specific offence type and precinct.
- Arrest ROI: number of arrests divided by the number of complaints. This ratio is between 0 and 1 with 1 being the optimal value. 
- Arrest Effectiveness: number of arrests minus the number of complaints. This metric is generally lower than 0 because for many hate crime complaints no suspect is arrested. The optimal value for this metric is 0 (i.e. for a specific precinct and bias motive, all the complaints have been addressed with an arrest).

I have used these four metrics and others to visualize the hate crime profile by area in NYC through both the *Precinct Profile* and the *Hate Crime Maps*.

## TOOLS

- Google Sheets for data cleaning and exploratory data analysis
- Pandas for data manipulation
- Geopy for locating the coordinates of the NYPD Precinct Addresses 
- Tableau for data visualization

## DATA SCIENCE SOLUTION PATH

As a first step, we need to be able to identify hate crime-related content on Facebook and Instagram. This will involve a combination of text/image recognition and NLP techniques and possibly the implementation of a hate crime-specific hashtag (first iteration) or a more salient form of CTA (second iteration) that will allow the user to classify the content as hate crime-related while sharing it.

It's useful to mention that this will be a classification model that will determine if the event related to a post is a hate crime.

By characterizing and differentiating hate crimes by neighbourhoods, these maps will allow first responders to allocate the appropriate resources to each neighbourhood. Finally, since the information will be shared by users in real time, my hypothesis is that Hate Crime Maps will shorten the first responders’ reaction time.

## FINAL DELIVERABLES
1. [Google Sheet](https://docs.google.com/spreadsheets/d/1xgUaUFrYza1ZxL4bKAzrVbhHiHSxZJBO2TWrZAxdAAo/edit?usp=sharing)
2. Tableau Dashboards
- [Hate Crime Maps - Main Components (2019-2021)](https://public.tableau.com/views/HateCrimeMaps-MainComponents/Hate_Crime_Maps_Components?:language=en-US&:display_count=n&:origin=viz_share_link)
- [Hate Crime Maps - Offence Type (2019-2021)](https://public.tableau.com/views/HateCrimeMaps-OffenceType/Hate_Crime_Maps_Offence?:language=en-US&:display_count=n&:origin=viz_share_link)
- [Precinct Profile - Hate Crime Complaints vs Arrests (2019-2021)](https://public.tableau.com/views/HateCrimePrecinctProfile-ComplaintsvsArrests/PP_complaints_arrests?:language=en-US&:display_count=n&:origin=viz_share_link)
- [Precinct Profile - Hate Crime  Arrests (2017-2019)](https://public.tableau.com/views/HateCrimePrecinctProfile-Arrests/PP_arrests?:language=en-US&:retry=yes&:display_count=n&:origin=viz_share_link)

## COMMUNICATION

A slide deck is included in this repo. 

In addition, see below the four Tableau dashboards I have created as part of this project.

### 1. Hate Crime Maps | Offence Type (2019-2021)
![image](https://user-images.githubusercontent.com/68084582/119904308-25d88800-bf18-11eb-8b55-d4b534d5a9ed.png)

### 2. Hate Crime Maps | Main Components (2019-2021)
![image](https://user-images.githubusercontent.com/68084582/119911218-da79a600-bf26-11eb-9d52-67429355e005.png)

### 3. Precinct Profile | Hate Crime Complaints vs Arrests (2019-2021)
![image](https://user-images.githubusercontent.com/68084582/119904164-e447dd00-bf17-11eb-8ee7-490dd22c58fc.png)

### 4. Precinct Profile | Hate Crime Arrests (2017-2019)
![image](https://user-images.githubusercontent.com/68084582/119904228-017cab80-bf18-11eb-9c37-a698ae856761.png)
