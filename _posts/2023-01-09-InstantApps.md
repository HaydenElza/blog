---
date: 2023-01-09
layout: post
slug: 
title: "ArcGIS Online Instant Apps Set Initial View/Extent"
categories:
- GIS
tag:
- ArcGIS
- ArcGIS Online
- Instant Apps
- GIS
---

## The Problem

If you've used ArcGIS [Instant Apps](https://www.esri.com/en-us/arcgis/products/arcgis-instant-apps/overview) before, you know that your underlying web map defines the initial view in the instant app. That is to say, if you set the initial view on your web map, the instant app will inherit that initial view.

However, if you use [navigation boundaries](https://www.esri.com/arcgis-blog/products/configurable-apps/mapping/refine-the-configurable-app-experience-using-navigation-boundary/) the initial view will no longer be inherited from the underlying web map but instead will be at the center of your navigation boundary. This is fine if your navigation boundary happens to align with what you want your inital view to be like illustrated below. 

<svg viewBox="23.535 17.733 386.076 237" width="100%" height="222">
  <rect x="23.535" y="33.936" width="386.076" height="204.081" style="stroke: rgb(0, 0, 0); fill: rgb(240, 240, 240);"></rect>
  <text style="fill: rgb(51, 51, 51); font-family: Arial, sans-serif; font-size: 14px; white-space: pre;" x="24.367" y="30.502">Navigation Boundary</text>
  <rect x="132.443" y="57.141" width="177.597" height="150.911" style="fill: none; fill-rule: nonzero; stroke: rgb(34, 0, 255);"></rect>
  <text style="fill: rgb(34, 0, 255); font-family: Arial, sans-serif; font-size: 14px; white-space: pre;" x="132.971" y="54.305">Initial View</text>
</svg>

But if your desired intial view is offset from the center of the navigation boundary like below, you're going to have an issue.

<svg viewBox="23.535 17.733 386.076 237" width="100%" height="222">
  <rect x="23.535" y="33.936" width="386.076" height="204.081" style="stroke: rgb(0, 0, 0); fill: rgb(240, 240, 240);"></rect>
  <text style="fill: rgb(51, 51, 51); font-family: Arial, sans-serif; font-size: 14px; white-space: pre;" x="24.367" y="30.502">Navigation Boundary</text>
  <rect x="37.443" y="56.141" width="127.315" height="133.062" style="fill: none; fill-rule: nonzero; stroke: rgb(34, 0, 255);"></rect>
  <text style="fill: rgb(34, 0, 255); font-family: Arial, sans-serif; font-size: 14px; white-space: pre;" x="37.971" y="53.305">Initial View</text>
</svg>

An example of this can be seen below. The navigation boundary is set to the entire Great Lakes region, so the initial view is set to the center of that extent. However, in this example I would like to center the inital view on the state of Wisconsin.

[![Instant App with initial view centered on navigation boundary.](/blog/assets/img/posts/2023-01-09_1.png)](https://uw-mad.maps.arcgis.com/apps/instant/sidebar/index.html?appid=96b80d1eb5174d3f9abd3b3c1301283c){:target="_blank"}

## The Solution

The solution is to add the center and zoom level paramters such as `&center=-89.9283;44.8694&level=7` to the URL. When those parameters are specified in the URL, the result is an intial extent in the desired area, in this example Wisconsin, as seen below.

[![Instant App with initial view centered on navigation boundary.](/blog/assets/img/posts/2023-01-09_2.png)](https://uw-mad.maps.arcgis.com/apps/instant/sidebar/index.html?appid=96b80d1eb5174d3f9abd3b3c1301283c&center=-89.9283;44.8694&level=7){:target="_blank"}

There are far more URL parameters than just center and level, so if you want to learn more check out the [URL parameter documentation](https://doc.arcgis.com/en/arcgis-online/reference/use-url-parameters.htm). There is also an extent parameter which I though would be even better than the center and level option, but unfortunately it seems like it doesn't work on instant apps where the navigation boundaries are set.



