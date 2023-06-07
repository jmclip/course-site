---
title: "HW09: Geospatial visualization"
date: 2022-11-09T13:30:00-06:00  # Schedule page publish date
publishdate: 2019-04-01

draft: false
type: post
aliases: ["/hw07-geospatial.html"]

summary: "Build a map."
---



# Overview

Due by 11:59pm on November 15th.

# Accessing the `hw09` repository

Go [here](https://github.coecis.cornell.edu/cis-fa22) and find your copy of the `hw09` repository. It follows the naming convention `hw09-<USERNAME>`. Clone the repository to your computer.

# Generate a geospatial visualization

Your objective: use geopspatial visualizations to communicate a story.

## Is that really all the help I get?

Yes.

## Arrrrrrrrgh but that is so vague

I know. But at this point you should be able to rise to the occasion.

## But where do I start?

Think of data you've seen in the past that you think would make for a good geospatial visualization. Which means it needs to include both a geographic component plus some additional data to overlay on top of the geography.

As for drawing the geographic boundaries, that depends on what you want to map. Find a relevant shapefile or GeoJSON which contains the boundaries for the region you wish to visualize. [Google is a great starting point](https://www.google.com/search?q=where+to+get+shapefiles). If you need help finding a relevant shapefile, feel free to post on the discussion board to get help from the instructional staff/peers.



Some suggested sources compiled by Deblina Mukherjee, a previous TA for the course:

* City Open Data Portals - Check [here](http://us-cities.survey.okfn.org/) to see what any city has available.
* [The government more generally.](https://catalog.data.gov/dataset?metadata_type=geospatial) Geospatial data is kind of hard to generate individually. Also consider [the `tidycensus` package](/notes/vector-maps-practice/) for any data related to the United States and demographics. Remember you can use `tidycensus` purely for the spatial features, then merge it with outside datasets that contain the substantive variables of interest.
* The [Array of Things](https://arrayofthings.github.io/) - it contains lots of different data from independent street-level sensors, all based in Chicago. 



Once you have your geographic boundaries data (either from an R package or imported from an external file), combine this with your substantive data you wish to visualize. Be sure to make the graph presentable - that is, make it look like a nice map. Things to consider include (but are not limited to):

* A map projection system
* Appropriate legends, titles, labels, etc.
* Color palette

**Along with the maps, write a brief description (250-500 words).** Summarize the information being depicted and explain any major visual design choices (e.g. why this color palette, why split the continuous variable into XYZ intervals rather than ABC intervals).

## How many maps do I need to make?

As many as it takes to tell your story. The more ambitious your analysis, the more you can be rewarded in your evaluation. Create a single map with all the default labels/settings? Your effort will be reflected in your evaluation.



Remember to make your assignment reproducible. If you get a shapefile from the internet, either include it in your repo or make sure your Quarto document/R script includes a function to download it from the internet.



# Submit the assignment

Your assignment should be submitted an Quarto document using the `gfm` (GitHub Flavored Markdown) format. Follow instructions on [homework workflow](/faq/homework-guidelines/#homework-workflow).

# Rubric

Needs improvement: Cannot get code to run or is poorly documented. No documentation in the `README` file. Severe misinterpretations of the results. Overall a shoddy or incomplete assignment. Maps look amateurish or hard to interpret.

Satisfactory: Solid effort. Hits all the elements. No clear mistakes. Easy to follow (both the code and the output). Nothing spectacular, either bad or good.

Excellent: Interpretation is clear and in-depth. Accurately interprets the results, with appropriate caveats for what the technique can and cannot do. Code is reproducible. Writes a user-friendly `README` file. Graphs look crisp, easy-to-read, and communicates information honestly and accurately.
