# Pedestrian And Bike Crash Data - Dataset (Public Safety)

# Data Source and Description
This data was provided by the St. Paul Police Department and contains all available information relating to bike and pedestrian crashes in St. Paul. As part of its commitment to improving pedestrian and bike safety, the city of St. Paul began aggressively tracking bike and pedestrian crashes in 2016. Data comes from traditional sources such as the State of MN Police Crash Report System and police reports. It also comes from social media, community conversations, police calls (911 and non-emergency) where no report was made, and other non-traditional ways to verify that a crash occurred. By collecting this level of detail for every pedestrian and bike crash in St. Paul, we are hoping to find patterns and answers to help us reach our goal of reducing the number of crashes and improving safety for all residents and visitors of St. Paul.

*  For more information, please visit the city of Saint Paul's website: https://www.stpaul.gov/departments/police/pedestrian-and-bike-crash-data-city-st-paul

* Last Update to Data Set: April 3, 2019 

* Data Provided by: Saint Paul Police Department

# Data Exploration and Data Visualization using Shiny

Data exploration over St. Paul publicly available data on pedestrian and bike crashes using R packages leaflet and shiny.
Leaflet is a package in R that is comparable to arcGIS. 

* The data contains crash type, longitude, and latitude data. Using these features, I created an interactive dashboard, which can be viewed here:

#  https://benjnguyen.shinyapps.io/ped-bike-shiny/

The following data visualization and explorations in tidyverse may also be framed within an R shiny web application to allow the audience to plot features against each other, which may be a feature I implement later on.

# Data Exploration and Data Visualization using Tidyverse

Data exploration over St. Paul publicly available data on pedestrian and bike crashes using R packages tidyverse and ggplot2.
The data is .csv format and exported into R for analysis.

It is a data set with 35 features; the names of the columns are listed below -- unfortunately there were no feature definitions provided in the database description. Furthermore, there are instances where the data had not been recorded very well, so some aggregation and filtering of entries within the data set needed to occur to produce easy to understand, sparse (using few features) visualizations.

## Column Names
 [1] "Crash.Type"                   
 [2] "Report.Made."                 
 [3] "Date...Time"                  
 [4] "Case.Number"                  
 [5] "District"                     
 [6] "Crash.Location"               
 [7] "Lanes.Of.Traffic"             
 [8] "Signal.Present."              
 [9] "Speed.Limit.Of.Road..MPH."    
[10] "Road.Type"                    
[11] "Synopsis"                     
[12] "Ticket.Arrest."               
[13] "Citation.To"                  
[14] "Pedestrian.Age"               
[15] "Pedestrian.Gender"            
[16] "Pedestrian.City.Of.Residence" 
[17] "Pedestrian.Zip.Code"          
[18] "Biker.Age"                    
[19] "Biker.Gender"                 
[20] "Biker.City.of.Residence"      
[21] "Biker.Zip.Code"               
[22] "Driver.Age"                   
[23] "Driver.Gender"                
[24] "Driver.City.Of.Residence"     
[25] "Driver.Zip.Code"              
[26] "Injury.to.Pedestrian."        
[27] "Level.of.Injury.to.Pedestrian"
[28] "Pedestrian.to.Hospital."      
[29] "Injury.to.Biker."             
[30] "Level.of.Injury.to.Biker"     
[31] "Biker.to.Hospital."           
[32] "Crash.Lat.Long.Location"      
[33] "Count"                        
[34] "District.Council...Map"       
[35] "Council.Ward"  

# Questions Posed and Answered
## How many of each crash type occurred?

The data set partitions the crash types into bike or pedestrian crashes, and a natural question arises about how many of each type occurred. In fact, this question remains relevant for the following questions asked, so this question/answer will be embedded for the remaining sections.

![Rplot-crash-types](https://user-images.githubusercontent.com/35606112/60136698-80846a80-976a-11e9-8205-619906ee3764.png)

We observe approximately two times more pedestrian crashes than bike crashes within the observational period of January 2016 - April 2019. In hindsight, that should have been a subtitle in the graph.

## How many crash reports did each district respond to?

The data collected is an aggregation of crash reports answered by the police departments in Minnesota. The police departments are identified by districts. A natural question is what type of crashes and how many of these crashes did each police department investigate?


![Rplot-district-crashes](https://user-images.githubusercontent.com/35606112/60136865-fdafdf80-976a-11e9-8d03-54bf97d75d6c.png)


![Rplot-district-crash-types](https://user-images.githubusercontent.com/35606112/60136970-3f408a80-976b-11e9-8fa7-bd8bff214984.png)

Here, we see that Western, Central, and Eastern districts take most of the bulk of crash reports, with most reports being pedestrian-type crashes.

## How do crash reports change over time?

The data collected contains time data of substantial granularity. We have data in the format of mm/dd/yyyy and hh:mm:ss.
This question is often a relevant in the context of time series analysis -- the choice of periodicity to examine can matter depending on how much information we want to see (e.g. whether there is cyclical patterns).

I give my own interpretation to the questions in the following visualizations -- looking over the time periods of years, months, hours of the day, and even month-day combinations.

![Rplot-years](https://user-images.githubusercontent.com/35606112/60137074-8890da00-976b-11e9-8b81-6aed8b6e9ebe.png)

Here, we can see that crash incidences have been trending downward -- although a limitation here is that the 2019 observation period is currently incomplete.

![Rplot-month](https://user-images.githubusercontent.com/35606112/60137121-a100f480-976b-11e9-85aa-7112a4ccb40e.png)

Here, we can see that the bulk of crash incidences occur during the summer months. However, it's worth noting that there is an increase in pedestrian crashes during the winter season, which I would conjecture is due to iced-over roads and snow.

![Rplot-hours](https://user-images.githubusercontent.com/35606112/60137184-d1489300-976b-11e9-8709-894936c65218.png)

Here, we can see that the bulk of crashes occur in the 2:00pm - 7:00pm periods.

![Rplot-month-days](https://user-images.githubusercontent.com/35606112/60137234-eb827100-976b-11e9-884b-a5f863d528f5.png)

Here, we can see some peaks for certain mm/dd combinations. These dates are likely worth investigating (I looked at them, which can be seen in the .pdf files with code chunks -- I didn't notice anything special about these dates so I attribute these peaks to being random occurrences.)

## How do crash types vary of speed limits?

This would have been an interesting question to ask of any data set that has count data for crashes across different speed limits. Unfortunately, most of the data has been recorded for speed limits of 30 mph -- with a few 10mph data points, so the plot is largely uninteresting. However, we can easily imagine an alternate world where there are more varied speed limits (e.g. if we looked at vehicle crash data of cars, trucks, buses, etc. on free-ways and high-ways). The beauty in tidyverse and ggplot is that the code chunk that produces these plots would largely be invariant -- it is just the data set that needs to change for us to see finer features.

![Rplot-speed](https://user-images.githubusercontent.com/35606112/60137292-0b199980-976c-11e9-81ba-84e8fd13fd6a.png)

## How does age correlate with crash incidences and crash type?

The data collected also contained ages associated with the people involved in these crashes. An interesting distinction here (and in the following visualizations) is that bike crashes do not contain driver crashes, but driver crashes may contain bike crashes. 

Unfortunately, as I previously mentioned, there is no data definitions so I cannot identify the exact reason why this is true -- but I can speculate. I believe that the data has been collected for vehicle collisions with bikers and pedestrians, therefore the reports do not document instances of bikers colliding with pedestrians, but it *does* contain age for drivers, which are presumably for vehicle drivers which imply that there are vehicle collisions with both bikers and pedestrians.


![Rplot-bikes](https://user-images.githubusercontent.com/35606112/60137311-1c62a600-976c-11e9-971d-837ccb2a5d1b.png)

![Rplot-drivers](https://user-images.githubusercontent.com/35606112/60137337-33a19380-976c-11e9-865d-e5c74038a45a.png)

The distributions appear bimodal, with most of the points aggregating around more youthful ages (around ~age 25).

## How does gender correlate with crash incidences and crash type?

The data contains information about the gender of the people involved in the crashes -- for the same reason I investigated age, I would like to investigate gender. To be honest, it's just a lot of fun investigating these multi-variate distributions -- as you can tell, I've plotted many of them!

![Rplot-gender](https://user-images.githubusercontent.com/35606112/60137370-4c11ae00-976c-11e9-9d9d-e71a94e38de5.png)

![Rplot-gender2](https://user-images.githubusercontent.com/35606112/60137407-68ade600-976c-11e9-91f3-12464e4a41f3.png)

Interestingly enough, we see that males are often times more invovled in crashes than females. However, I would argue that there is a latent variable, i.e. there is a limitation to the data set that might inadvertantly lead us to this proposed hypothesis that males are more at risk than females.

The limitation here is the number of miles driven by each gender. A preliminary google search suggests that males drive many more miles than females. It would be very important to investigate a model where we have genders (males, females) with the number of miles driven for each gender nested under each gender. In this hierarchical model framework, we can see what truly carries the potentially (statisitcally and practically) significant effects on crash rates -- is it the gender or is it the miles driven?!

At any rate, it is always good to pose the question of whether or not there is an omitted variable in the data set -- and thus a limitation to the answers posed to questions you may want to ask.

## How does a signal being present or omitted reflect on incidences and crash type?

This question is particularly interesting because it allows us to pose the question of whether or not a signal being present has an effect on crash rates and crash types. Of course, that is more of a modelling question -- but you can easily see how EDA can help us pose great hypotheses and gives us insight into what type of modelling we would like to do to answer these hypotheses.

![Rplot-signal](https://user-images.githubusercontent.com/35606112/60137488-ab6fbe00-976c-11e9-9e88-2cebfdbc6b91.png)

As we can see, it's hard to see whether there is a significant difference -- a preliminary gesture would be to test the hypothesis that the presence of a signal has no effect. A limitation in this data set is that some most of the entries were (Yes -- present signal) or (No -- no signal). Some entries recorded the type of signal, which I think would have been the best way to take the measurement (as opposed to a binary response). In particular, having both the binary response and the indetifying response would have been wonderful here, but I make do with what I received.

## What does the distribution of levels of injuries look like?

This question is also interesting from a modelling perspective -- once we have data that bins the types of injuries into categories and we have count data for it, we can formulate questions such as "if a police officer were investigating a crash report, what is the likelihood that the injury sustained by the invovled parties is non-serious, serious, fatal, etc.?

![Rplot-biker-inj](https://user-images.githubusercontent.com/35606112/60137540-d9ed9900-976c-11e9-93d4-f41178b41975.png)

![Rplot-driverinj](https://user-images.githubusercontent.com/35606112/60137560-e96ce200-976c-11e9-8419-ddc0295a6fab.png)

# Summary of EDA

From EDA, I can tentatively (i.e.. *not definitively*) say the following:

1. More pedestrian crashes occur than bike crashes.

2. Most crashes occur under jurisdictions of the Western, Central, and Eastern Districts.

3. By year, crashes have been trending downward.

4. By month, crashes tend to occur more frequently in the summer season.

5. By hour, the 2:00pm - 7:00pm time slot seems to have the most frequent incidents of crashes.

6. Younger bikers and drivers tend to get more involved in crashes.

7. Males are associated with higher crash incidents.

8. Signals do not have an obvious effect on crash incidents.

These EDA insights are worth studying more in-depth using modelling and predictive techniques, but the purpose here was to work with some EDA techniques using ggplot2 and tidyverse. 

For the purposes of public safety, it is interesing to unravel important features. Often times, many features are out of the department of public safety's control -- there are few to no design variables that they can change to help them reduce crash rates. However, they may produce targetted messages to help reduce accidents. For example, they can broadcast to pedestrians in the winter months to be extra careful; they can broadcast in the summer months for people to take extra precaution on the roads; they can encourage safer travels in the 2:00pm-7:00pm brackets via social media; they can encourage younger and more inexperienced drivers to be extra careful and mindful of their surroundings, etc...

Since many of these features are outside of the design variable paradigm, it is helpful to give a gentle reminder and bring to attention about potential dangers to at-risk people during opportune times.

* For insights into how these plots were created, check out the repository! :)
