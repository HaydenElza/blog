---
date: 2022-11-28
layout: post
slug: 
title: "ArcGIS Online: Update Service to Allow HTML Links in Fields"
categories:
- ArcGIS Online
tag:
- arcgis 
- agol
- esri
- python
---

If you are editing a feature layer hosted in ArcGIS Online and trying to edit a field to add an HTML link you may run into this error:

~~~bash
Exception: 
Field some_field_name has invalid html content.
(Error Code: 400)
~~~

This is because by default feature layers hosted on ArcGIS Online do not allow you to insert links into fields because it could be "harmful". There are two solutions based on your specific scenario. If you just have a link in a field, you can try replacing certain characters with [HTML entities](https://developer.mozilla.org/en-US/docs/Glossary/Entity) that are considered invalid such as `=` or `&`, but if you have HTML content that includes a link, then you will need to update your feature layer's service definition to disable XSS prevention. 

## Option 1: replace invalid characters

So for the first scenario, simply santize your links to remove any charcters that ESRI deems invalid:

~~~python
def sanitize_link(link):
    return link.replace("=","&equals;").replace("&","&amp;")
~~~

You might need to replace additional characters such as `<` or `>`.

## Option 2: update service definition to disable XSS prevention

In the second scenario the solution to this error is updating the service definition of your feature layer by chainging the `"xssPreventionEnabled"` value to `False`.

[This blog post](https://community.esri.com/t5/arcgis-data-interoperability-blog/writing-html-and-other-amp-lt-and-amp-gt-tagged/ba-p/1116925) was helpful in outlining the solution using the ArcGIS REST API. However, if you'd rather do it using ArcGIS API for Python, say in a notebook, here is a code snippet you can adapt to your feature layer:

~~~python
# Allow html links in fields
from arcgis.features import FeatureLayerCollection
item = gis.content.get("c65363c5bfe54557b1985e69a8a3052e")  # Enter your feature layer's id here
flc = FeatureLayerCollection.fromitem(item)

updated_properties = {"xssPreventionInfo": {
    "xssPreventionEnabled": False
}}

flc.manager.update_definition(updated_properties)
flc.properties
~~~

This code snippet allows you to edit the service definition of a feature layer to allow HTML links to be added to field value. You can learn more about working with service definitions using ArcGIS API for Python [here](https://developers.arcgis.com/python/guide/updating-feature-layer-properties/).

Enjoy!
