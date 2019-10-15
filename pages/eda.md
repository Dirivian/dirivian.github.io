---
layout: default
permalink: /pages/eda/
---



Exploratory data analysis - Taking a look at earthquakes.

 
I got interested in the earthquakes dataset from CORGIS. Since I had previously worked on tsunamis, this seemed like
a nice field to explore and find some patterns. My vague question right now is to see how the impact and timing of earthquakes depends on previous earthquakes 
spacially.

After extracting the dataset, I plotted it.

![Incorrect](incorrect.png)

After looking at the specific data of a few points, I realized I made a mistake because California seemed to be near Austrialia (I had switched latitude and longitude.)
The corrected version is below.

![Correct](correct1.png)

Not all earthquakes are the same. So, I added the 'significance' of the earthquake as the radius in the scatterplot. However, the visualization is less effective.

![sig2big](sig2big.png)

So, I turned to see if earthquakes triggered other earthquakes in nearby locations. I first checked the last 3 instances and found them very close to each other.

![Last3](last3.png)

 The last 10 instances seemed to agree and the last 50 seem to show some clustering.

![Last10](last10.png)

![Last50](last50.png)



