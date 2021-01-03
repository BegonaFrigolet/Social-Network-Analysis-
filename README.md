# Social-Network-Analysis

## Introduction

With the high increase in bicycle sharing systems in most large cities around the world, we found it interesting to analyze and compare some of the best established ones. We here use a different approach that would ususally be applied on such data. Indeed, we use a Network Analysis to try finding insights

In our project, we focus on turning bike trips into networks that we can analyze. Thus throughout the study, we established networks in which the nodes are the bike stations throughout the city, and the edges are the flows pf the trips in each direction between the stations. And the edges are weighted by the number of trips carried out by the bikes on that edge.

The goal of this research would be to try finding similarities and differences in the networks of these cities’ systems as well as finding interesting patterns within each city.

The different cities analyzed here are Montreal, New York, and Madrid which respectively started operating those bicycle sharing systems in 2009, 2013, and 2014.


## About the tools used
For our analysis, we combined outputs from various tools. Namely:

- R for the analysis and the report in a Markdown format;
- Python for data transformation;
- Gephi for the visualizations of our networks;
- FlowingBlue for maping the networks on mapped backgrounds.

## To review the Final Materials:
- [R Markdown](https://github.com/BegonaFrigolet/Social-Network-Analysis-/blob/main/SNAproject.Rmd)
- [HTML](https://github.com/BegonaFrigolet/Social-Network-Analysis-/blob/main/A%20look%20at%20Madrid%E2%80%99s%20Bike%20Sharing%20System%20with%20Comparaisons%20to%20New%20York%20and%20Montreal%E2%80%99s%20systems%20HTML.html)

## About the main ressources consulted
Throughout this analysis, we consulted many ressources and accumulated some inspiration from here and there. The main ones are the following:

For the preliminary analysis, we mainly used the course scripts and a great course from DataCamp from which we use many functions and approaches: https://learn.datacamp.com/courses/case-studies-network-analysis-in-r

For the visualization in Gephi, we mainly used: http://gephi.michalnovak.eu/Mastering%20Gephi%20Network%20Visualization.pdf

For the community detection, we combined the knowledge from: https://www.sciencedirect.com/science/article/pii/S2405896317325284

https://arxiv.org/pdf/1804.05584.pdf

https://www.kernix.com/article/community-detection-in-social-networks/


## About the data used
As mentionned above, we used the data for 3 cities, each city provided the information in different ways and thus the preparation for the data was different in each cases. Most of the data preparation has been done in Python before using R for the analysis. We here provide the steps followed for each city’s data. The Python code is available in the submitted documents with the intermmediary and final datasets as well.

Note that we used data for the month of June 2019 for the 3 cities to make sure our comparison is the least biased possible.

The data can be found here: https://we.tl/t-pEYMo5DTZ3

4.1 Madrid Data

Data for the stations:
The EMT Madrid open data provides information on trips and stations. The stations information are timestamp data on the activities of the station at each time interval. From this file we extracted the stations and made sure all the stations present in the trips were present in the stations file as well. This data can be found here:https://opendata.emtmadrid.es/Datos-estaticos/Datos-generales-(1) We then used this interactive map to get insights on the stations themselves which helped us better understand the data on hand: https://data-crtm.opendata.arcgis.com/datasets/bases-bicimad


Data for the trips:
We used the same source as the one mentionned above, and did the transformations in the Python file. The transformations we did were mainly to get a Source and Target station with weights that represented the trips between the stations. We provide both these processed files in the data folder.


Montreal Data
Data for the stations:
We downloaded the data from Kaggle, made available by the user JackyWang (available at: https://www.kaggle.com/jackywang529/bixi-montreal-bikeshare-data). He concatinated the data from the source open data website: https://montreal.bixi.com/en/open-data. The station files were already provided and thus we used the file for the stations in 2019.

Data for the trips:
In the same datasets provided from Kaggle, we took the data for June 2019 and did the transformations in the Python file. The transformations we did were mainly to get a Source and Target stations with weights that represented the trips between the stations. We provide both these processed files in the data folder.


New York Data
Data for the stations:
We downloaded the data from https://www.citibikenyc.com/system-data, which provides data on trips since 2013. Here, the files for the stations and for the trips were not separated. The stations data was combined with the trips one. From the June 2019 data, we thus extracted the stations names, geolocalisation data, and id. We looked for the distinct ones in starting and ending stations to make sure we captured all the available stations. The transformations can be found in the Python file.

Data for the trips:
In the same way as Madrid and Montreal, the transformations we did were mainly to get a Source and Target stations with weights that represented the trips between the stations. We provide both these processed files in the data folder.

## Starting with some graphs to get an intuition
After testing various plots in R, Gephi, and Flowmap, we concluded that the best way to visualize the networks would be to map the in, out, and overall the degrees on the same graph using Flowmap. These were the graph giving us the best insights and availability for comparison. We later on in the next section show the computations of these and other central measures.

To be able to compare the graphs and reduce bias, we used the month of June 2019 for each city.

The maps of the degrees for the 3 cities
The datasets used were built in Python and we uploaded them to Flowmap.

The links to the interactive maps are:

Madrid:https://flowmap.blue/1ICXKvFfMd3jDKvJTbpprm1JW3w2lOP_bMoIdpgMwWtE?v=40.423190,-3.694299,12.13,0,0&a=0&b=1&bo=75&c=0&d=0&lt=1&lfm=ALL&col=DarkMint&f=50

New York:https://flowmap.blue/1NKYn1fEw0qe7biOgdMlzXXGDjhpeSpLd51J8DhXFeQY?v=0.000000,0.000000,1.71,0,0&a=0&b=1&bo=75&c=0&d=0&lt=1&lfm=ALL&col=DarkMint&f=50

Montreal:https://flowmap.blue/1APu7yHTPZg6j0c8ggbj09ViGseqnvN-TDUEO31WVIqA?v=45.509453,-73.602573,11.02,0,0&a=0&b=1&bo=75&c=0&d=0&lt=1&lfm=ALL&col=DarkMint&f=50 

![Map of three cities](https://github.com/BegonaFrigolet/Social-Network-Analysis-/blob/main/1.%20Graphs/Captura%20de%20Pantalla%202021-01-02%20a%20la(s)%2019.20.11.png)

The first insight, we believe, from the graph is the obvious central focus point for Montreal and New York while Madrid’s important nodes are more widespread with no clear center. These attributes will be further highlighted in the upcoming analysis.

### Madrid over the years
How has Madrid’s network evolved over the years? We here plotted the data of the 3 networks over the years to see the evolution of the network and maybe get an insight from it.

![Madrid over the years](https://github.com/BegonaFrigolet/Social-Network-Analysis-/blob/main/1.%20Graphs/Captura%20de%20Pantalla%202021-01-02%20a%20la(s)%2019.20.27.png)

Already from the data, we noticed a decrease in the edges for Madrid. And this is clearly evident from the graphs of the network. We have a reduced amount of weight from year to year (again here we are using for each year the data for the months of June 2017).

### A comparison to Montreal over the years

To see if this pattern is similar or different in other already established systems, we also looked at the change of the network for Montreal from June 2016 to June 2019.

![Montreal over the years](https://github.com/BegonaFrigolet/Social-Network-Analysis-/blob/main/1.%20Graphs/Captura%20de%20Pantalla%202021-01-02%20a%20la(s)%2019.20.34.png)

We can clearly see an opposite trend here with increasing weights in the edges of the graph. And another interesting trend is the expansion of the network to further locations.

### Concluding remarks

Through this Social Network Analysis, we were able to clearly highlight the differences between the bike sharing systems of more established cities like New York and Montreal as compared to Madrid. The insights here could be beneficial for Madrid to improve its system and tackle the decline in use we’ve highlighted over the years.
