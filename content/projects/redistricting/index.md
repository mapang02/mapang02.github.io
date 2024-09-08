+++
title = 'CSE 416 - Redistricting Simulation'
date = 2023-12-20
draft = false
+++
[[GitHub link](https://github.com/hshaf/redistricting-project)]

As different parts of the country grow and shrink in population, it becomes necessary to draw new electoral districts for state and federal elections so that political power is distributed proportionally. However, the manipulation of electoral districts to provide disproportional power to a party or group--known as gerrymandering--has been a problem throughout the history of the United States. In this class project for CSE 416, I worked in a team to generate electoral districts using computational techniques, yielding results which may help to create fairer election maps.

## The Recombination Technique
States are divided into large numbers of precincts, each of which is defined by the section of land serviced by a single polling station (meaning that all citizens of a precinct go to that station to vote). Electoral districts are usually created by combining precincts; since precincts are so small it is usually possible to create electoral maps with an almost equal population for each district without breaking up any precincts. As such, precincts can be considered the minimum unit of land for constructing districts. We used data from the [Redistricting Data Hub](https://redistrictingdatahub.org/), which provides the geographical boundaries of the precincts of each state as well as the census and election data for each precinct.

The recombination technique (or ReCom) works by repeatedly selecting two adjacent districts from the map, merging them, and re-partitioning their respective precincts into two new districts. There are various ways to perform the re-partitioning step; all methods must ensure that both resulting districts are contiguous and have around the same population. After a large enough number of steps, the resulting district map is effectively unrelated the starting map (which might be the current electoral map), meaning that they can be considered effectively random. 

{{<figure src="images/recom.png" caption="An example of a single iteration of the recombination process. Source: DeFord, Daryl, et al. Recombination: A Family of Markov Chains for Redistricting, mggg.org/uploads/ReCom.pdf">}}

Generating a large number of potential maps with this technique and analyzing the likely outcomes of elections held with those maps gives a sense of the range of likely outcomes from an electoral map created in a truly fair manner, and human-created maps which are extreme outliers relative to the random maps can be examined for bias. For example, if the randomly generated maps generally result in one party winning between 50% and 60% of the seats, then it indicates that a map which let that party win 80% of seats is likely gerrymandered.

The ReCom technique was created by the MGGG Redistricting Lab at Tufts University. You can find their site [here](https://mggg.org/) and you can read the research paper describing this technique in further detail [here](https://mggg.org/uploads/ReCom.pdf).

## Analyzing Generated Maps
Using data for the 2020 Presidential Election, we can predict the winners of state or federal Congressional elections using a given generated map (under the assumption that votes for a party in the Presidential election correspond to votes for a party in other elections). These results vary from map to map, but they provide a range of results that can be expected to occur from creating maps in an unbiased manner.

We accomplished this using the [GeoPandas](https://geopandas.org/) library, which expands on Pandas by providing tools for working with geographical boundary data. Using GeoPandas, we were able to aggregate precinct-level data into the districts we generated and also create map boundaries for the district plans.

## Visualizing Results
We created a web application that allows for several important properties of the generated maps, such as the number of Democratic/Republican districts and the number of majority-minority districts[^1] to be visualized. This is useful for establishing the expected range of values for maps generated in an unbiased manner (which can be compared to the currently existing maps to detect potential bias or gerrymandering), and can also be used to find correlations between these different properties.

{{<figure src="images/cluster_analysis.png" caption="The chart shows the number of majority-minority districts versus the party split for each of the generated district plans within the cluster. Other properties of the generated districts can be graphed as well.">}}

We also displayed the generated maps using [Leaflet](https://leafletjs.com/). This could be potentially be used to evaluate the maps to see if they are suitable for use or to compare them to the currently existing maps. 
{{<figure src="images/district_plan.png" caption="One of the plans we generated for the Virginia State Assembly.">}}

## Personal Thoughts
This was a unique and interesting project; I hadn't seen this kind of computerized analysis in politics before. I learned a lot about data analysis throughout this project; GeoPandas in particular felt like a powerful tool that made working with geographical data feel simple and I'd definitely consider it for future projects of this nature. 

[^1]: Majority-minority districts are districts where the majority of the population belongs to a certain racial or ethnic minority group.