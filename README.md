# pedestrian-bike-data

Data exploration over St. Paul publicly available data on pedestrian and bike crashes using R packages tidyverse and ggplot2.
It is a data set with 35 features. The purpose of data exploration in workflow is to identify key features how their relationships with other features within the data set to discover ways to construct (predictive) modeling and make inference. In other words, it helps inform us about how to create models when we are not yet familiar with how variables relate to each other -- EDA allows us to pick apart the data set and informs us about what it can tell us and its limitations. 

The 35 columns are listed below -- unfortunately there were no definitions provided in the database. Furthermore, there are instances where the data had not been recorded very well, so some aggregation and filtering of entries within the data set needed to occur to produce sparse (using few features) visualizations.

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

## Questions Posed and Answered
Some questions that I posed over the data set and attempted to answer were

# How many of each crash type occurred?

The data set partitions the crash types into bike or pedestrian crashes, and a natural question arises about how many of each type occurred. In fact, this question remains relevant for the following questions asked, so this question/answer will be embedded for the remaining sections.

![Rplot-crash-types](https://user-images.githubusercontent.com/35606112/60136698-80846a80-976a-11e9-8205-619906ee3764.png)

We observe approximately two times more pedestrian crashes than bike crashes within the observational period of January 2016 - April 2019. In hindsight, that should have been a subtitle in the graph.

# How many crash reports did each district respond to?

The data collected is an aggregation of crash reports answered by the police departments in Minnesota. The police departments are identified by districts. A natural question is what type of crashes and how many of these crashes did each police department investigate?


![Rplot-district-crashes](https://user-images.githubusercontent.com/35606112/60136865-fdafdf80-976a-11e9-8d03-54bf97d75d6c.png)


![Rplot-district-crash-types](https://user-images.githubusercontent.com/35606112/60136970-3f408a80-976b-11e9-8fa7-bd8bff214984.png)

# How do crash reports change over time?

The data collected contains time data of substantial granularity. We have data in the format of mm/dd/yyyy and hh:mm:ss.
This question is often a relevant in the context of time series analysis -- the choice of periodicity to examine can matter depending on how much information we want to see (e.g. whether there is cyclical patterns).

I give my own interpretation to the questions in the following visualizations -- looking over the time periods of years, months, hours of the day, and even month-day combinations.

![Rplot-years](https://user-images.githubusercontent.com/35606112/60137074-8890da00-976b-11e9-8b81-6aed8b6e9ebe.png)

![Rplot-month](https://user-images.githubusercontent.com/35606112/60137121-a100f480-976b-11e9-85aa-7112a4ccb40e.png)

![Rplot-hours](https://user-images.githubusercontent.com/35606112/60137184-d1489300-976b-11e9-8709-894936c65218.png)

![Rplot-month-days](https://user-images.githubusercontent.com/35606112/60137234-eb827100-976b-11e9-884b-a5f863d528f5.png)

# How do crash types vary of speed limits?

This would have been an interesting question to ask of any data set that has count data for crashes across different speed limits. Unfortunately, most of the data has been recorded for speed limits of 30 mph -- with a few 10mph data points, so the plot is largely uninteresting. However, we can easily imagine an alternate world where there are more varied speed limits (e.g. if we looked at vehicle crash data of cars, trucks, buses, etc. on free-ways and high-ways). The beauty in tidyverse and ggplot is that the code chunk that produces these plots would largely be invariant -- it is just the data set that needs to change for us to see finer features.

![Rplot-speed](https://user-images.githubusercontent.com/35606112/60137292-0b199980-976c-11e9-81ba-84e8fd13fd6a.png)

# How does age correlate with crash incidences and crash type?

The data collected also contained ages associated with the people involved in these crashes. An interesting distinction here (and in the following visualizations) is that bike crashes do not contain driver crashes, but driver crashes may contain bike crashes. 

Unfortunately, as I previously mentioned, there is no data definitions so I cannot identify the exact reason why this is true -- but I can speculate. I believe that the data has been collected for vehicle collisions with bikers and pedestrians, therefore the reports do not document instances of bikers colliding with pedestrians, but it *does* contain age for drivers (for presumably vehicle drivers).


![Rplot-bikes](https://user-images.githubusercontent.com/35606112/60137311-1c62a600-976c-11e9-971d-837ccb2a5d1b.png)

![Rplot-drivers](https://user-images.githubusercontent.com/35606112/60137337-33a19380-976c-11e9-865d-e5c74038a45a.png)

The distributions appear bimodal, with most of the points aggregating around more youthful ages (around ~age 25).

# How does gender correlate with crash incidences and crash type?

The data contains information about the gender of the people involved in the crashes -- for the same reason I investigated age, I would like to investigate gender. To be honest, it's just a lot of fun investigating these multi-variate distributions -- as you can tell, I've plotted many of them!

![Rplot-gender](https://user-images.githubusercontent.com/35606112/60137370-4c11ae00-976c-11e9-9d9d-e71a94e38de5.png)

![Rplot-gender2](https://user-images.githubusercontent.com/35606112/60137407-68ade600-976c-11e9-91f3-12464e4a41f3.png)

Interestingly enough, we see that males are often times more invovled in crashes than females. However, I would argue that there is a latent variable, i.e. there is a limitation to the data set that might inadvertantly lead us to this proposed hypothesis that males are more at risk than females.

The limitation here is the number of miles driven by each gender. A preliminary google search suggests that males drive many more miles than females. It would be very important to investigate a model where we have genders (males, females) with the number of miles driven for each gender nested under each gender. In this hierarchical model framework, we can see what truly carries the potentially (statisitcally and practically) significant effects on crash rates -- is it the gender or is it the miles driven?!

At any rate, it is always good to pose the question of whether or not there is an omitted variable in the data set -- and thus a limitation to the answers posed to questions you may want to ask.

# How does a signal being present or omitted reflect on incidences and crash type?

This question is particularly interesting because it allows us to pose the question of whether or not a signal being present has an effect on crash rates and crash types. Of course, that is more of a modelling question -- but you can easily see how EDA can help us pose great hypotheses and gives us insight into what type of modelling we would like to do to answer these hypotheses.

![Rplot-signal](https://user-images.githubusercontent.com/35606112/60137488-ab6fbe00-976c-11e9-9e88-2cebfdbc6b91.png)

# What does the distribution of levels of injuries look like?

This question is also interesting from a modelling perspective -- once we have data that bins the types of injuries into categories and we have count data for it, we can formulate questions such as "if a police officer were investigating a crash report, what is the likelihood that the injury sustained by the invovled parties is non-serious, serious, fatal, etc.?

![Rplot-biker-inj](https://user-images.githubusercontent.com/35606112/60137540-d9ed9900-976c-11e9-93d4-f41178b41975.png)

![Rplot-driverinj](https://user-images.githubusercontent.com/35606112/60137560-e96ce200-976c-11e9-8419-ddc0295a6fab.png)

# Summary of EDA

From EDA, I can tentatively say the following:

1. More pedestrian crashes occur than bike crashes.

2. Most crashes occur under jurisdictions of the Western, Central, and Eastern Districts.

3. By year, crashes have been trending downward.

4. By month, crashes tend to occur more frequently in the summer season.

5. By hour, the 2:00pm - 7:00pm time slot seems to have the most frequent incidents of crashes.

6. Younger bikers and drivers tend to get more involved in crashes.

7. Males are associated with higher crash incidents.

8. Signals do not have an obvious effect on crash incidents.

These EDA insights are worth studying more in-depth using modelling and predictive techniques, but the purpose here was to work with some EDA techniques using ggplot2 and tidyverse. 

For insights into how these plots were created, check out the repository! :)
