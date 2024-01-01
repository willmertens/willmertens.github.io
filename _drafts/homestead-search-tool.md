---
layout: post
title:  "GIS features from Public Land Survey System Land Descriptions"
date:   2022-4-5 09:47:27 -0700
categories: jekyll update
type: GIS
permalink: "/blog/gis-features-from-PLSS"
blurb: ""
---

The [General Land Office (GLO)](https://en.wikipedia.org/wiki/General_Land_Office) was the federal government organization responsible for administering public lands in the United States. It existed from 1812 until 1849, when it was placed under the Department of the Interior and later merged with the United States Grazing Service to become the Bureau of Land Management (BLM) in 1946.

Among other things, the GLO took over responsibility for finishing the [Public Land Survey System](https://en.wikipedia.org/wiki/Public_Land_Survey_System) (PLSS) from the Department of the Treasury. Another responsibility of the GLO was administering the homestead acts, with land allocation being facilitated by the PLSS.

## History of the Public Land Survey System
The PLSS was created by the Land Ordinance of 1785 to better-systematize the United States occupation of first peoples' lands. At first under the purview of the Department of the Treasury, surveying of the Northwest Territory commenced in 1786 from an origin point at its Eastern border. The first survey created the [Seven Ranges](https://en.wikipedia.org/wiki/Seven_Ranges) in present-day East-Central Ohio, comprising an area with a northern border of 42 miles, western border of 91 miles, and roughly split diagonally by the Ohio river. That took almost two years to complete. As the PLSS had not yet been fully developed, they were reportedly littered with inaccuracies.

![State of Ohio. Arrow points to the Seven Ranges.](/assets/img/Seven_in_Ohio.png)
##### State of Ohio. Arrow points to the Seven Ranges. [Image Source](https://books.google.com/books?id=r-jSAAAAMAAJ&pg=RA1-PA93&source=gbs_selected_pages&cad=2#v=onepage&q&f=false)
{: .img-caption}

The name "Seven Ranges" refers to the seven North-South "range" lines established every six miles along the established baseline, thus creating a northern border of 42 miles. At each of these six-mile increments surveyors began to travel South, again placing markers every six miles, creating East-West "township" lines. The resulting six-mile-square plats of land are referred to as townships. After the Seven Ranges was completed, several more surveys were completed in Ohio as surveying methods were perfected. 

Ohio, being sort of a test-bed for the PLSS, has several surveyed tracts each with its own origin point, baseline (the line extending East-West from the origin), and meridian (the line extending North-South from the origin). It seems like the last of Ohio was surveyed in 1819, but I couldn't find a solid answer on that. Mississippi is another state to be surveyed early on, resulting in more (smaller) tracts.

Expanding westward, subsequent meridians and baselines covered far greater land area, with some encompassing many current U.S. states. The final results can be seen in the map below below. Notable exceptions include the land controlled by the thirteen original colonies at the time of U.S. independence and Texas, which was under the control of the Spanish and later adopted its own system that it still uses today.

![Meridians and baselines in the United States created under the PLSS](/assets/img/Meridians-baselines.png)
##### Meridians and baselines in the United States created under the PLSS. [Image Source](https://www.researchgate.net/figure/The-Rectangular-Survey-System-in-the-United-States_fig2_238093708)
{: .img-caption}

## How the PLSS works
If you have made it this far into my coverage of U.S. westward expansion at the beginning of a blog post largely about a Python script, thank you. You will now be rewarded with a detailed explanation of how the PLSS actually subdivides the U.S. 

### Townships

As I already mentioned, the basic building block of the PLSS are the six-mile squares known as townships. Each of the 85,316 -- according to the [Living Atlas](https://fedmaps.maps.arcgis.com/home/item.html?id=90289fe691db470195f6511454ede315) layer I was looking at -- townships in the PLSS area originate from one of the 38 origin points.

Townships are numbered sequentially based on how far away they are from their principal meridian. Directions indicate which quadrant of the principal meridian they are in. In this example we're describing township 27 South range 34 West, abbreviated to T27S R34W. It's origin is the Sixth Principle Meridian. Remember that the township is the number of six mile increments North or South of the meridian and the range is the number of six mile increments east or west of the meridian. 

You may, at this point, find the use of the word "township" to describe a particularly sized plot of land to be confusing as it likely conjures up images of small towns in Pennsylvania coal country. More confusingly, as it relates to the PLSS, a township is both the term for this particular geographic reference and part of the descriptor. This would mean that the sentence "that township is on township 27 South" makes sense. 

Anyway, since this origin point is toward the east side of the Kansas-Nebraska border, we can see that T27S R34W is in, appropriately, Southwestern Kansas. The Southwest corner of this township would be (in theory) 204 miles West and 162 miles south of the origin.

<!-- TODO insert image here -->

I say in theory because townships boundaries -- and their further subdivisions -- remain defined by how they were originally surveyed. This means that the technology of the time, hastiness of the crew, and more besides led to a grid that is...less that perfect but also remarkably uniform given the monumental task of the surveyors. 

You can look at the map above to see the mess that was created in Ohio while the surveyors were still learning how to walk in a straight line. But while they<sup>*</sup> became demonstrably better as westward expanded, there are still any number of abnormalities to be found in the 

To be clear, we still use the PLSS today. It's still the was that land is allocated in the western United states.

<sup>**By they I mean the hundreds or thousands of surveyors that took part in surveying the U.S. using the PLSS between 1785 and the early 1900s.*</sup>
