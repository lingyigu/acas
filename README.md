# ACAS Progress Report

Team: [Haoyu(Jerry) Wu](https://github.com/wuhaoyujerry), [Wei Wei](https://github.com/wei0496), [Lingyi Gu](https://github.com/lingyigu)
### Project Description
The overall goal of this project is to gain more insights on the main reasons for midair collisions.  As the project owner request, we focus on analyzing the narratives of each incident and aim to find the main reason that causes the near midair collision. After initial data analysis, we find that the human error is the most prominent factor of collisions. 

Furthermore, we would like to see how the relative position of the aircraft (relative distance to the airport) and altitude of the aircraft relate to these human errors. For example, a air collision happened near the aircraft may because of a wrong decision made by the traffic alert and collision avoidance crew, while a collision happened far from the aircraft may because of pilot’s operation error. We will cluster based on these human errors and quantified distances to give an intuitive explanation of the human causes of mid air collisions. 

### Data Retrieval (Close to be completed)
As we work more on retrieving data, we decide to use the air collision data published by NASA (https://akama.arc.nasa.gov/ASRSDBOnline/QueryWizard_Filter.aspx). We first select all the airborne collision data in Massachusetts for test. We plan to expand the data collection to other states, or to the entire United State. Then we specify different parameters regarding the environment, aircraft type, etc. After we get the data, we generate corresponding CSV files from this website. 

### Data Cleaning & Analysis
We first clean the data by removing all the prefixes, suffixes, and empty entries to get the useful information. 
As the client request, we choose to primarily analyze the report of each incident, which is the short narratives from the pilots that explain the details of the incidents.  We first parse each report and remove some insignificant words like “in”, “one”, etc. Then we change all the words to the root forms by stemming them, so even if the same word is in different term, the algorithm will still categorize them together.

We also have performed the Principle Component Analysis on the narrative of each event to get the most important terms and phrases that mentioned across all the descriptions. Here are the example of some terms we found:

```

[['acr', 'error', 'standard', 'system', 'separ', 'between', 'ltss', 'sy'],
 ['ctlr', 'zbw', 'experienc', 'operror', 'at', 'separ', 'standard', 'ft'],
 ['tcasii', 'to', 'alt', 'acr', 'ra', 'ltss', 'assign', 'dscnt'],
 ['rwi', 'on', 'acr', 'apch', 'experienc', 'ltss', 'operror', 'error'],
 ['rwi', 'on', 'acft', 'of', 'apch', 'to', 'separ', 'standard'],
 ['class', 'in', 'airspac', 'tcasii', 'separ', 'ra', 'at', 'system'],
 ['plt', 'at', 'pa28', 'pattern', 'conflict', 'same', 'ltss', 'bed'],
 ['ft', 'crew', 'alt', 'at', 'conflict', 'dep', 'through', 'rwi'],
 ['acft', 'close', 'prox', 'at', 'ha', 'sma', 'tcasii', 'ft'],
 ['acft', 'alt', 'anoth', 'same', 'crew', 'at', 'class', 'airspac']]
```
Full forms of the above abbreviations:<br>
aircaft, error, standard, system, separation, between, Less Than Standard Separation<br>
control, boston air route traffic control center, experience, operator, at, separation, standard, feet<br>
Traffic Alert and Collision Avoidance, to, alert, aircaft, Resolution Advisory, Less Than Standard Separation, assign, descdent<br>
runways, on, aircraft, approach, experience, Less Than Standard Separation, operator, error<br>
Resolution Advisory, Traffic Alert and Collision Avoidance, report, crew, aircraft, approach runway, control<br>

### Methodology
We will cluster each report based on the quantified values, relative distance and altitude, to find similar reports in each cluster and analyze based on the size and the assigned human error in each cluster to reach our conclusion.

In order to visualize the cluster results, we will represent each report as a data point in a 2D graph, and extract the human errors causing the collision of each cluster, which will not only give an intuition of the interrelation of the human factor and quantified distances, but also show how these factors combined together may lead to frequent air collisions. 

### Timeline
* **11/17** Initial report complete & Utilize PCA to extract the descriptions of incident report
* **11/27** Use multiple distance functions  to measure the similarity between different parameters extracted by PCA from the narratives or data fields already existed in the report (environment conditions, aircraft type, etc). After that, cluster based on the relative distance and altitude to find similar reports in each cluster.
* **12/04** Visualize the data into a 2D graph and interpret the graph and reach our final conclusions.
* **12/13** Poster Ready and all code & reports submitted.
