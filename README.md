# Aircraft Collision Avoidance System (ACAS)
Research the main reasons for near midair collisions to improve the existing Aircraft Collision Avoidance Systems.

Team: [Haoyu(Jerry) Wu](https://github.com/wuhaoyujerry), [Wei Wei](https://github.com/wei0496), [Lingyi Gu](https://github.com/lingyigu)

## Objective
In the US, the VFR(Visual Flight Rules) allows pilots almost unlimited freedom to fly anywhere without filing a flight plan. In 2016, there were 179 reported near midair collisions, which led to critical consequences. Our main objectives are to generate insight from the narratives of collision reports that help researchers reinforce their collision avoidance strategy to alleviate the situation.

The overall goal of this project is to gain more insights on the main reasons for midair collisions.  As the project owner request, we focus on analyzing the narratives of each incident and aim to find the main reason that causes the near midair collision. After initial data analysis, we find that the human error is the most prominent factor of collisions. 

Furthermore, we would like to see how the relative position of the aircraft (relative distance to the airport) and altitude of the aircraft relate to these human errors. For example, an air collision happened near the aircraft may due to a wrong decision made by the traffic alert and collision avoidance crew, while a collision happened far from the aircraft may because of pilot’s operation error. We will cluster based on these human errors and quantified distances to give an intuitive explanation of the human causes of mid air collisions. 

## Data Retrieval
As we work more on retrieving data, we decide to use the air collision data published by NASA (https://akama.arc.nasa.gov/ASRSDBOnline/QueryWizard_Filter.aspx). We first select all the airborne collision data in Massachusetts for test. We plan to expand the data collection to other states, or to the entire United State. Then we specify different parameters regarding the environment, aircraft type, etc. After we get the data, we generate corresponding CSV files from this website. The dataset we currently used for data cleaning & analysis is included in the src folder.

[NASA’s Aviation Safety Reporting System](https://asrs.arc.nasa.gov/): We downloaded the collision data from the system and mainly utilized the narratives and summaries of each report, along with the altitude and the relevant distance between aircrafts. 

[The U.S. National Transportation Safety Board](https://www.ntsb.gov/investigations/AccidentReports/Pages/aviation.aspx): We also scraped informative reports on aviation incidents, which serve as a useful aid to supplement our understanding of the data sourced from the ASRS database.

## Preprocessing
1. **Stemming**: Eliminate noises in the text.
2. **Stop words**: remove common English words. (E.g. We, are)
3. **Preliminary analysis**: Before analyzing the narratives, we want to learn what factors contribute to collisions the most. From the graph on the right, we can see that human error is the most prominent reason for midair collisions. However, we still need to analyze the narratives to see if the finding corresponds to this heat map.


## Dimensionality Reduction & Latent Semantic Analysis(LSA)
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

We can observe that the cause of the collision is most likely to be caused by human (pilot, crew, traffic control center, resolution advisory) and later we will analyze further into how different parameters may affect their decisions and cause the collision. 

## Clustering
After performing latent semantic analysis and singular value decomposition, we clustered the incidents by three metrics. We confirmed that human error is the most common reason for collision. Since K-means ++ has the highest Silhouette Score, we chose it for further analysis. 

## Heap map of clustering results
Clustering gave us an intuition of how different combination of factors at each different altitude, which may lead to a collision. By plotting a heat map for each cluster, we can observe the number of occurrence of these words and determining the important ones.  

## Conclusion
- The lower the altitude, collision is more likely to happen because aircrafts are taking off or landing.
- Among low altitude collision (<20,000) during climbing and descending, the parameters which may cause a collision are: downwind, tower, true airspeed, aircraft turning, heading mode, traffic control, visual and collision frequently happens among single engine piston.
- Among high latitude collision (20,000 ~ 50,000), collisions likely happen during sector (a portion of an itinerary) or climb, and associates more with the arrangement of the traffic control center and airport. Visual and radar may also play an important role here.

## Limitation & Future Work
1. Outlier detection improvement.
2. Text vectorization improvement. (E.g. remove numbers)
3. Analyze based on phase rather than single word

## Methodology
We will cluster each report based on the quantified values, relative distance and altitude, to find similar reports in each cluster and analyze based on the size and the assigned human error in each cluster to reach our conclusion.

In order to visualize the cluster results, we will represent each report as a data point in a 2D graph and let relative distance & altitude being the x,y value of the axis. We will extract the person(pilot, crew, resolution advisory, etc) and his errors causing the collision of each cluster, which will not only give an intuition of the interrelation of the human factor and quantified distances, but also show how these factors combined together may lead to frequent air collisions. 

## Timeline
* **11/17** Initial report complete & Utilize PCA to extract the descriptions of incident report
* **11/27** Use multiple distance functions  to measure the similarity between different parameters extracted by PCA from the narratives or data fields already existed in the report (environment conditions, aircraft type, etc). After that, cluster based on the relative distance and altitude to find similar reports in each cluster.
* **12/04** Visualize the data into a 2D graph and interpret the graph and reach our final conclusions.
* **12/13** Poster Ready and all code & reports submitted.

## Reference