---
layout: post
title: Analyzing Crime Trends and Enhancing Safety in Urban Areas
description: This project analyzes crime rates at Washington D.C. bus stops to enhance rider safety
---

### Introduction ###

With the rise in violent crimes, there's a need to analyze current preventative measures and resource allocation, particularly at bus stops in urban areas like the DMV. This project aims to identify wards with the highest crime rates and assess trends in resource allocation, focusing on bus stops.

`The Analyzed Characteristics of Each Dataset`
1. Crime Incidents 2022

      Dataset Used: [Crime Incident Reported (DC)](https://opendata.dc.gov/datasets/DCGIS::crime-incidents-in-2022/about){:target="_blank"}

* Ward
* Shift (time of day)
* Offense types include auto theft, motor vehicle theft, robbery, assault with a dangerous weapon, burglary, homicide, sex abuse, and arson

2. Metro Bus Stops
   
      Dataset Used: [Metro Bus Stops (DC)](https://opendata.dc.gov/datasets/DCGIS::metro-bus-stops/explore){:target="_blank"}
   
* Service effective dates for each ward
* Presence of street lights within 30 feet
* Street locations

`Outcome:` Identify wards with high crime rates, and provide recommendations for resource reallocation to improve bus stop safety.

### Method ###

The datasets were merged to find correlations between bus stop locations and crime rates. Visualizations were created to identify wards with high crime rates and inadequate resource allocation. Based on these findings, suggestions were provided for reallocating preventative services to enhance bus stop safety.

Python Libraries Used:
* Pandas
* Matplotlib
* Folium


~~~
offenses_day = crime_bus_df.groupby(['WARD', 'TIME'])['OFFENSE'].size().reset_index()
offenses_day.pivot(index = 'WARD', columns = 'TIME', values = 'OFFENSE').plot(kind='bar')
plt.xlabel('WARD')
plt.ylabel('Number of Offenses')
plt.title('Number of Offenses by Time of Day')
plt.show()
~~~
![Chart_1](https://github.com/jchan125/gradfolio/blob/master/assets/images/Image1_CrimeIncident.png?raw=true)

The graph above depicts the number of offenses by the time of the day in each ward. Ward 2 has a high amount of offenses and it seems that crimes happen more towards the day and evening, rather than midnight.

~~~
street_day.pivot(index='STREET', columns='TIME', values='OFFENSE').plot(kind='bar')
plt.xlabel('Street Name')
plt.ylabel('Number of Offenses')
plt.title('Number of Offenses by Time of Day in Ward 2')
plt.show()
~~~
![Chart_2](https://github.com/jchan125/gradfolio/blob/master/assets/images/Image2_CrimeIncident.png?raw=true)

The graph above focuses in on Ward 2, as they have the highest number of offenses. 9th ST NW's bus stop has a lot of crimes happening during the day and evening while comparing that to midnight.

~~~
street_light.pivot(index='WARD', columns='LIGHT', values='OFFENSE').plot(kind='bar', stacked=True)
plt.xlabel('WARD')
plt.ylabel('Number of Offenses')
plt.title('Street Lights in Relation to Number of Offenses')
plt.show()
~~~
![Chart_3](https://github.com/jchan125/gradfolio/blob/master/assets/images/Image3_CrimeIncident.png?raw=true)

The graph above shows that overall streetlights are being implemented, but they're not affecting the number of offenses per ward.

### Summary ###

The discussion analyzes the frequency, distribution, and timing of offenses, the impact of bus stop characteristics on crime rates, and the limitations of the data used.

`Frequency of Offenses:`

* Theft-related offenses are the most common, with "THEFT/OTHER" being the highest
* D.C Metro Police should focus on preventing theft incidents

`Timing of Offenses:`
* Offenses frequently occur during the day and evening
* Most wards experience more offenses during the day, while Ward 2 sees a higher rate during the evening
* Suggest increased security presence in Ward 2 during the evening

`Bus Stop Characteristics and Crime:`
* No correlation found between street lights and reduced offenses
* Offenses are higher within 30 feet of a street light in Ward 2, indicating a need for more robust prevention measures

`Limitations:`
* Data is limited to Washington, D.C., and the year 2022
* The "THEFT/OTHER" category is too broad, limiting deeper analysis
* Lack of data on the number and distribution of police officers
* Absence of precise timestamps, relying only on broad time categories (day, evening, midnight)
* High number of unknown values in the Metro Bus Stops dataset, especially in the street light column

### Conclusion ###

The analysis highlights the need for better security measures at bus stops, with a focus on theft prevention. Ward 2, particularly 9th St NW, requires more security during the evening. Effective crime prevention must extend beyond street lights to include features like emergency call boxes.
