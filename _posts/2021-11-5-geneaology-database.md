---
layout: post
title:  "Genealogy Database"
date:   2021-4-14 09:47:27 -0700
categories: jekyll update
type: other
permalink: "/blog/geneaology-database"
blurb: "I created a SQL database to keep track of relatives"
---

Here's simple database project I completed in PostgreSQL to store and query members of my family. It works by storing each individual in a table, then establishes either a spousal or parent/child relationship in a separate table. While I have a field for gender in the individual table, I wanted to make sure it also worked when specifying a third gender, or no gender.

![Family database schema](/assets/img/family_db_schema.png){:class="img-responsive"}

The schema includes the two main tables and three tables to store special codes for gender, relationship types, and the role of each individual in the relationship. It also sets up views that I used to query other types of relationships. For example, here's the code to create the aunt/uncle view:

{% highlight sql %}
create view aunt_uncle as
--Select biological aunts/uncle
select distinct i.individual_id as aunt_uncle, i.name_first, i.name_last, i2.individual_id as niece_nephew, i2.name_first, i2.name_last
from individual i, individual i2, sibling s, parent p
where i2.individual_id = p.child     --the niece/nephew is a child
    and p.parent = s.sibling2        --the parent of the niece/nephew has a sibling
    and s.sibling1 = i.individual_id --aunt/uncle is a sibling of the parent of the niece/nephew

union --select nonbiological aunts/uncles(spouses) listed in relationships as r.individual_2_id

select distinct i.individual_id as aunt_uncle, i.name_first, i.name_last, i2.individual_id as niece_nephew, i2.name_first, i2.name_last
from individual i, individual i2, relationship r, aunt_uncle a
where a.aunt_uncle = r.individual_1_id      --individual 1 is a boilogical aunt or uncle
    and r.individual_2_id = i.individual_id --relationship.individual2 joined with individual
    and i2.individual_id = a.niece_nephew   --i2 is a niece or a nephew
    and r.relationship_code = 20            --only select mirriages

union --select nonbiological aunts/uncles(spouses) listed in relationships as r.individual_1_id

select distinct i.individual_id as aunt_uncle, i.name_first, i.name_last, i2.individual_id as niece_nephew, i2.name_first, i2.name_last
from individual i, individual i2, relationship r, aunt_uncle a
where a.aunt_uncle = r.individual_2_id
    and r.individual_1_id = i.individual_id
    and i2.individual_id = a.niece_nephew
    and r.relationship_code = 20
            
{% endhighlight %}

The first block selects biological aunts/uncles. This uses the sibling view. In short, it selects an individual as a niece/nephew if that individual (a) is a child in the database, (b) the individual's parents have siblings, and (c) the aunt/uncle is a sibling of the individual's parent. The subsequent unions select the spouses of the biological aunts/uncles.

Here's another example of querying for cousin relationships:

{% highlight sql %}
--Select cousins
select distinct i.individual_id as cousin1, i.name_first, i.name_last, i2.individual_id as cousin2, i2.name_first, i2.name_last
from individual i, individual i2, parent p, parent p2, sibling s
where i.individual_id = p.child     -- cousin 1 is a child in the database
	and p.parent = s.sibling1       -- the parent of cousin 1 has a sibling
	and i2.individual_id = p2.child -- cousin 2 is a child in the database
	and p2.parent = s.sibling2      -- the sibling of the parent of cousin 1 is the same as the parent of cousin 2
	--This works because the sibling view has two records for each relationship
		--(person a is a sibling of person b and person b is a sibling of person a)
            
{% endhighlight %}