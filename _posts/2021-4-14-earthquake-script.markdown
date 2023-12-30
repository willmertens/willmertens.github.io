---
layout: post
title:  "Buffer Earthquakes"
date:   2021-4-14 09:47:27 -0700
categories: jekyll update
type: GIS
permalink: "/blog/earthquake-script"
---
This script generates a polygon feature class of earthquake "felt areas" and a summary table with the count and average magnitude of earthquake classes. It produces output buffers of earthquake epicenter points based on the magnitude of the quake and the average kilometers felt. It also produces a table of statistics that display the count and average magnitude by descriptive class. Parameters are passed in with a Script Tool in ArcGIS Pro.

{% highlight python %}
import arcpy

# function to determine the descriptive class of a earthquake based on magnitude
def desc_class(mag):
    if mag < 3.0:
        return "Micro"
    elif 3.0 <= mag <= 3.99:
        return "Minor"
    elif 4.0 <= mag <= 4.99:
        return "Light"
    elif 5.0 <= mag <= 5.99:
        return "Moderate"
    elif 6.0 <= mag <= 6.99:
        return "Strong"
    elif 7.0 <= mag <= 7.99:
        return "Major"
    else:
        return "Great"


# function to determine the distance felt of an earthquake in kilometers based on magnitude
def km_felt(mag):
    if mag < 3.0:
        return 5
    elif 3.0 <= mag <= 3.99:
        return 25
    elif 4.0 <= mag <= 4.99:
        return 75
    elif 5.0 <= mag <= 5.99:
        return 125
    elif 6.0 <= mag <= 6.99:
        return 250
    elif 7.0 <= mag <= 7.99:
        return 400
    else:
        return 750


input_fc = arcpy.GetParameterAsText(0)  # Input feature class
distance_field = arcpy.GetParameterAsText(1)  # magnitude field used to find felt distance and descriptive class
output_buffer = arcpy.GetParameterAsText(2)  # location of output buffer
output_table = arcpy.GetParameterAsText(3)  # location of summary table
temp_copy = r"in_memory\tempOutput"  # variable for in-memory workspace
fields = ["Magnitude", "buff_dist", "descriptive_class", "OID@"]  # field names, used as needed

# copy input feature class to in-memory workspace to calculate felt distance and descriptive class
arcpy.CopyFeatures_management(input_fc, temp_copy)
arcpy.AddMessage(f"Copied features to {temp_copy}")

# add fields to temporary feature class
arcpy.AddFields_management(temp_copy, [[fields[1], "TEXT"], [fields[2], "TEXT"]])
arcpy.AddMessage(f"Added fields for buffer distance and descriptive class to {temp_copy}")

# update new fields using the functions
arcpy.AddMessage(f"Starting to update new fields in {temp_copy}")
with arcpy.da.UpdateCursor(temp_copy, fields) as cursor:
    for row in cursor:
        if row[0] is None:  # skip rows with null magnitude values
            arcpy.AddMessage(f"Skipped point with null magnitude value at OID {row[3]}")
            continue
        row[1] = str(km_felt(row[0])) + " kilometers"
        row[2] = desc_class(row[0])
        cursor.updateRow(row)
arcpy.AddMessage(f"Finished updating new fields in {temp_copy}")

# create the buffer feature class
arcpy.Buffer_analysis(temp_copy, output_buffer, fields[1])
arcpy.AddMessage(f"Created buffer feature class in {output_buffer}")

# create table using summary statistics
arcpy.Statistics_analysis(output_buffer, output_table, [[fields[0], "COUNT"], [fields[0], "MEAN"]], fields[2])
arcpy.AddMessage(f"Created summary statistics table in {output_table}")
arcpy.AddMessage("Done!")
{% endhighlight %}