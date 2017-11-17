# ACAS Progress Report
### Project Description
The overall goal of this project is to gain more insights on the main reasons for midair collisions. After discussion with the project owner, we are planning to come up with our own hypothesis and assumptions to investigate any possible correlations between different features such as weather condition, pilot operation, radio usage, etc. After we experiment more with the dataset, we may come up with a more specific, interesting hypothesis. The motivation for choosing this project is that it is really open-ended and contains a lot of information and parameters per report, which is quite challenging but rewarding. In addition, it also allows us to freely test our own hypothesis to find attracting or possibly counterintuitive results. Therefore, by participating in this project, we are able to get a better understanding of the data science techniques as well as contribute to reducing the aircraft incidents.

### Data Retrieval (Close to be completed)
As we work more on retrieving data, we decide to use the air collision data published by NASA (https://akama.arc.nasa.gov/ASRSDBOnline/QueryWizard_Filter.aspx). We first select all the airborne collision data in Massachusetts for test. We plan to expand the data collection to other states, or to the entire United State. Then we specify different parameters regarding the environment, aircraft type, etc. After we get the data, we generate corresponding CSV files from this website. 

### Data Cleaning & Analysis
We first clean the data by removing all the prefixes, suffixes, and empty entries to get the useful information. 
As the client request, we choose to primarily analyze the report of each incident, which is the short narratives from the pilots that explain the details of the incidents.  We first parse each report and remove some insignificant words like “in”, “one”, etc. Then we change all the words to the root forms by stemming them, so even if the same word is in different term, the algorithm will still categorize them together.
We also have performed the Principle Component Analysis on the narrative of each event to get the most important terms and phrases that mentioned across all the descriptions. Here are the example of some terms we found:

![](Screen%20Shot%202017-11-17%20at%203.03.44%20PM.png)

### Methodology
One of the simple results we can show, giving that all reports are aircraft collisions which actually happened, is to create a bar graph of the frequency of each parameter which leads to the collision. This gives a simple intuition but does not explain the interrelations. So to explore further, we will construct a distance matrix and decide between distance metrics (Euclidean Distance, Manhattan Distance, etc), to find the similarity between our different parameters in each report. After that, we will utilize clustering to find similar reports in each cluster and analysis based the size and combination of terms in each cluster to reach our conclusion. In order to visualize the cluster results, we will represent every report as a data point in a 2d graph, and extract the frequent combination of features of each cluster, which will give an intuition of each factor combined together may likely to lead to frequent air collisions. 

### Timeline
* **11/17** Initial Report Complete & Utilize PCA to extract the descriptions of incident report SV
* **11/27** Use multiple distance functions  to measure the similarity between different parameters extracted by PCA from the narratives or data fields already existed in the report (environment conditions, aircraft type, etc). After that, cluster based on the similarity and extract the frequent combinations of factors which lead to “similar” aircraft collisions.
* **12/04** Visualize the graph (more detail in the Results section), interpret the graph and reach our final conclusions.
* **12/13** Poster Ready and all code & reports submitted.
