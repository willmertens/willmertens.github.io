---
layout: post
title:  "Effigy Mound Walkways"
date:   2020-9-14 09:47:27 -0700
categories: jekyll update
type: GIS
permalink: "/blog/effigy-mound-walkways"
blurb: "Beloit College has 22 Native American effigy mounds. What's the most efficient path to avoid walking on them?"
---

This was a special project was completed for Beloit College in Spring 2019 using analysis tools in ArcMap. Beloit College is home to 22 Native American mounds, some of which contain human remains. My project used the guidelines for mound preservation provided by the state of Wisconsin to systematically draw new walkways that would provide easy access to buildings while insuring the integrity of the mounds. I was thrilled to take on this project because I was able to combine skills from my focus in cultural anthropology with my interest in GIS to create a useful map for future walkways at Beloit College.

![Beloit College mounds. View from the West. Source: Beloit College Archives](/assets/img/mounds.jpg){:class="img-responsive"}

Analysis tools used were Cost Distance, Cost Back Link, and Least Cost Path. Priority was assigned to each class in the cover-type based on where paths could be safely constructed. Three origin and three destination points were then selected. The cover-type was used to generate Cost Distance and Cost Back Link rasters for each of the three origin points. These rasters were then passed into the Least Cost Path tool, which was used to generate recommend paths between each of the points.

![Effigy mounds map](/assets/img/effigy_mounds_map.jpg){:class="img-responsive"}
