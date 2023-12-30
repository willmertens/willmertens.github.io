---
layout: post
title:  "Master's Thesis: Facilities Management"
date:   2021-12-2 09:47:27 -0700
categories: blog gis
type: GIS
permalink: "/blog/masters-thesis-facilities-management"
blurb: "Creating an indoor GIS for Montessori in Redlands"
---

## A Facilities Management Solution for Montessori in Redlands
Herein is the progress I've made so far on my master's thesis. Or, as we call it at the University of Redlands, my major individual project (MIP). As of October 2021, it's still a work in progress. However, with the digitizing phase mostly complete, I can showcase some of what I've done so far.

The goal of this project is to build an integrated facilities management platform for Montessori in Redlands (MIR), which is a small non-profit school serving students from pre-k to 6th grade. MIR wanted the system to serve three main functions:
- Track inventory of classroom materials
- Manage the maintenance and replacement of permanent assets
- Provide a basemap to first responders, which they can access in the event of an emergency

The solution I've developed will create a basemap of campus utilizing the ArcGIS Indoors spatial hierarchy.

### Digitizing
MIR has six buildings, none of which have had CAD floorplans that were accessible to the project. It was, therefore, my job to manually digitize each building from their original, paper, floorplans. I began by scanning and georeferencing each of the floorplans, then digitized them into the Details feature class. The most difficult building to complete was the main building, which had three separate floorplans from various renovation projects. These floorplans also did not accurately reflect every change that has been made to the building since it was built in 1990. There were also direct contradictions among some measurements. Fortunately, I was able to elicit some help from a team member at ESRI. I thank this person immensely. An example of one of the digitized buildings is below, along with the attributes for the selected polygon.

![One of the digitized buildings](/assets/img/stu_serv_activity_room_attrib.png){:class="img-responsive"}
![Attributes from the selected polygon](/assets/img/stu_serv_pro.png){:class="img-responsive"}

Most of these attributes are there to support the ArcGIS Indoors data model. The feature I show in the attribute table above is from the units feature class, which is for representing individual spaces such as rooms or hallways. In most applications of the Indoors data model, the name of the unit would follow the room numbering scheme of the building. MIR, however, does not use room numbers in any of their buildings, so I've given each space a unique name. The Level ID is the main attribute used to enable floor aware features that will be present in the deployment.

### What's Next
All the facilities management features will be represented as point data. Each item will have a point located in its approximate location in the classroom. The item's attributes will contain data about its location, use, and quantity. Assets will also be points at their approximate location and have information derived from a previous reserve study that had been conducted on the campus. The points for first responders will clearly show door numbers and room names.

The system will be managed in WebMaps and through the FieldMaps mobile app. It's important that the system is able to preform everyday functions without running ArcGIS Pro since it will be used by staff members without significant GIS skills.

### Update: It's finished!
I've finished the project. I'm working on getting a more detailed update on here. In the meantime, check out my final report and poster on the [University of Redlands Repository](https://inspire.redlands.edu/work/ns/633a0310-b42c-474d-bbb2-3e4947aaf06c).