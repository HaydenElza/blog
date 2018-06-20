---
date: 2015-11-30
layout: post
slug: 
title: "ArcGIS Model Builder - Select by Location: Using an Output as an Input "
categories:
- GIS
tag:
- ArcGIS
- Select by Location
---

While building a model in ArcGIS Model Builder today I was baffled by the fact that I could not use a previous output as the input for the [Select by Location]( https://resources.arcgis.com/EN/HELP/MAIN/10.1/index.html#//001700000072000000) tool. I later realized that I must use the [**Make Feature Layer**](https://pro.arcgis.com/en/pro-app/tool-reference/data-management/make-feature-layer.htm) tool on the output before it can be used as the input for Select by Location. Make Feature Layer creates a layer from a spatial dataset to that it may be used with any tool requiring a feature layer (such as Select by Location).
[![](https://imgur.com/xTHTM1n.png)]( https://imgur.com/xTHTM1n.png)
