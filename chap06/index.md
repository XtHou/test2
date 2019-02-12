---
title: "Module 6 Interactive data exploration & visualisation"
author: "Kimbal Marriott"
date: "25/01/2019"
description: ""
output: bookdown::gitbook
site: bookdown::bookdown_site
toc depth: 1
documentclass: book
---



# Interactive data visualisation

As a data scientist you are comfortable using R and Python to interactively explore data. However, often it’s better to use a less powerful but easier to use interactive visualisation tool. This is because programming is slow and error prone, and many analysts are not experienced programmers. Most data analysts find exploring data with Tableau a lot easier than using R.

In this topic we look at how to design such visual analytics tools. While it is unlikely that you will ever be involved in the design or implementation of a really generic tool like Tableau it is quite possible that you may be a part of a team developing a more specialised analytics tool. [Scaffold Hunter](http://scaffoldhunter.sourceforge.net) is an example of such a visual analytics tool. It was originally developed for drug design. To find out more about Scaffold Hunter please take a look at the video below.  Another good reason for learning about the design space is that it informs more critical evaluation of existing visual analytics tools.

<video width="320" height="240" controls>
  <source src="diagrams_datasets/section1/ScaffoldHunter_Video.mp4" type="video/mp4">
</video>

## Analytics tasks

The first part of any design process is to understand the user tasks: _what_ do they want to be able to do with the tool. Once we know this, then we can decide _how_ best to achieve this. There have been many different ways of classifying the user tasks in data exploration.

Ben Schneiderman introduced the very influential data visualisation mantra: _Overview first, zoom and filter, details on demand_ as a summary of the key steps in data visualisation.  An initial overview provides the user with a summary of the entire data set and a context in which to drill down.

Providing an initial overview makes sense for applications in which the relevant context is well defined and the data set is moderately sized.  In many applications however providing an overview may not be beneficial. For instance, when using Google Maps it isn’t that useful to always start with the whole Earth.  For cases like this van Ham and Perer introduced an alternative mantra: _search, show context, expand on demand_. This is precisely how Google Maps works.

Other data visualisation researchers have attempted to provide a more fine-grained and multi-level analysis of the visual analytics tasks:

_Discovery_: The fundamental task that the analyst wants to achieve is to derive insight or knowledge from the data. The desired outcome might be to formulate a hypothesis (“discover the unexpected”) or to test a hypothesis (“confirm the expected”). The hypotheses may take the form of cause-and-effect relationships, trends, correlations or clusters.

_Presentation_: This goal refers to presenting insight or knowledge that has already been found to some intended audience.

We shall focus on the discovery task. This relies on performing a series of _analytical tasks_:

* *Search* for elements that satisfy certain properties, if they exist. This might be locating a known data point, filtering the data, or finding outliers.
* *Identify* the properties of a single data item
* *Compare* or *rank* elements
* *Visually* identify patterns in some subset of elements. Examples include trends, correlations, clusters or categories.
* Calculate *derived* properties not originally in the data. These may be data transformations, data aggregations or may be statistical properties such as regression lines or clusters

Analytical tasks rely on _presentation_ tasks:

* *Visualise* by mapping elements and their attributes to visual variables to create a view
* *Manipulate (or configure)* a view by navigating and selecting subsets of elements

There are other user tasks that support analytical tasks

* *Annotate* visual elements with text or graphical elements
* *Record* visualisation elements so that they can be preserved and accessed outside the analytics tool. For example, Tableau records a graphical history, with snapshots showing how the current visualisation was reached
* *Revisit* an earlier visualisation or relocate an element or pattern that was previously found by the analyst

We now look at various ways to support the analytical and presentation tasks.

## Manipulate a view

One of the defining characteristics of a visual analytics tool is that it supports direct manipulation of views by the user. This is unlike say using **R** and **ggplot2** in which views are static and any modification (apart from zooming and panning) requires generating a new view from the command line. Please take a look at the [Line Up](https://www.youtube.com/watch?v=4WfwDQC73o0) system for a good example of view manipulation.

Common reasons for manipulating the view are to

* *Control a dynamic visualisation*. It is natural to visually encode data that changes over time as an animation. Effective understanding requires that the viewer can control the speed, pause and move backwards and forwards in time. If possible the changes should be staged and use animated transitions so that the viewer’s attention is focused on salient changes and they preserve their mental map of the visualisation. Also remember that animation is not the only way, and often not the best, of showing dynamic data: small multiples are very effective and can be used to show differences as well as the actual values.
* *Modify the visual encoding*. It is common to allow the viewer to change the choice of colour palette (improving accessibility), or provide the ability to reorder or sort elements and to align elements.
* *Filter items*. A major reason for interaction is to reduce data complexity. Filtering data items is a widely used technique for reducing complexity. Typically the viewer can use slider bars, search terms etc, to filter data based on restricting attribute values.
* *Control the level of detail (LoD)*. Interaction can be used to control whether sub-hierarchies or clusters are expanded/collapsed or the level of detail shown in the data items.
* *Filter attributes*. Attributes can also be filtered to reduce complexity. The most common approach is slicing which eliminates an attribute by only showing the items with the chosen value in that attribute. Slicing is widely used to show axis-aligned 2D slices or sections through 3D images. Closely related is the *cut*, which shows the data on one side of a cutting plane.
* *Navigate*. But undoubtedly the main use of interaction is to allow the user to navigate through the view, to change the viewpoint.

The most common navigation technique is to provide zooming and panning, exactly as in Google Maps. In _geometric zooming_ the objects do not change their spatial appearance, they simply get larger or smaller. In _semantic zooming_ the appearance changes at different scales. Typically , as the object becomes larger, the level of detail increases. For instance in maps, towns are shown as dots on large scale maps but when the viewer zooms in they reveal their spatial shape and then the buildings and streets that form the town.

It is useful to distinguish between _unconstrained navigation_ in which the viewer can zoom and pan anywhere, and _constrained navigation_ in which the allowed viewpoints are restricted. For instance, the user may not be able to zoom in or out too far, or may be able to select an item of interest or home view and the system will move to that viewpoint, often using an animated transition. Constrained navigation has the advantage that users are less likely to get lost, though they lose some flexibility.

An alternative to zooming and panning is to use what are called _focus+context_ views in which data in the view is shown in more detail around the focal point on the view and in less detail elsewhere in the view, so as to provide context. Probably the best known focus+context view is the fisheye lens, in which the view is distorted so as to achieve an effect similar to the fish eye lens in photography. Other types of focus+context views remove detail for objects away from the focus or provide detail on a separate layer, for instance using the metaphor of a magnifying lens.

## Visualise

Multiple views are required to understand all but the simplest data. These show complementary aspects of the data. For instance, they might show:

* the same data visualised at different levels of scale for instance an overview and a detailed view,
* different attributes of the data, or
* comprise small multiples showing data at different time periods or for different values of a categorical variable.

A good visual analytics tool provides the views and view manipulation tools that will be of most use to the typical user and controls to customise the view. The degree of customisability depends greatly on the application and the kind of users. Take a look at the [VisGets](https://mariandoerk.de/visgets/video.mp4) tool for exploring posts on on-line forums and consider the choice of views it provides as well as the kinds of interaction provided.

Views can be organised in many different ways:

* *Temporal*:  the viewer can toggle or move between different views, showing one at a time.
* *Side-by-side*: the views are shown next to one another
* *Layered*: the views sit on top of one another.

Each way of organising the views has advantages and disadvantages. Showing the views one at a time has a high cognitive cost as the user must remember information from previously shown views, layering can lead to clutter and less effective visual encodings because of the need to use different encodings for the different layers, while a side-by-side arrangement takes up more screen real estate and each view has less resolution. Nowadays, as display resolution is increasing, I think the side-by-side arrangement should be the first choice considered.

Linking different views of the data is important if they are to be effective. Some of the ways of linking different views are

* *Shared visual encodings*. This includes using the same color or shape encoding for an attribute shared between the different views.
* *Alignment and common scale*. This is particularly useful in small multiples so as to allow ready comparison between the different views. It is used very effectively in scatter plot matrices.
* *Shared filtering*. Filtering in one view affects all views. This allows filters to be linked with the appropriate views. Thus one view might show data organised by time with a time line for filtering by date while another view might show the data organised by category with check boxes to select categories.
* *Shared selection*. Highlighting selected objects in all views is a powerful way of synchronising the views. This is often called brushing and typically occurs on mouse hover.
* *Shared navigation*. Zooming and panning affects all relevant views.

A crucial part of the view are the keys, labels and legends which explain what the view is of and how to read the visual encoding. It is surprising how often these are forgotten. Labelling and gridding should be consistent across different views.

A common use of multiple views is for navigation. A common approach is to provide the user with both a *detailed* and *overview* of the data, usually shown side-by-side but sometime overlaid. The two views are linked in that the position of the detailed view is always shown on the overview and sometimes can be controlled from the overview. Depending upon the application either the detailed or the overview may be larger.

## Analytics

Visual analytics is not only about visualisation, it is also about analytics. The choice of these is application specific. Some common kinds of analytics are

* *Item aggregation, clustering and smoothing*. Aggregating multiple items into a new item is one way of reducing complexity and allowing the wood to emerge from the trees. Totals, averages, counts, clustering, curve and surface fitting, and spatial clustering are all ways to aggregate/combine items. The box plot is a good example of a visualisation that aggregates information about a distribution.
* *Attribute aggregation* reduces the number of attributes by combining attributes to give a new attribute. Dimension reduction techniques such as PCA or MDS are examples of attribute reduction.
* *Data transformation* allows the user to scale or combine data sets
* *Identifying interesting views* is less common but potentially very useful. This might for example analyse correlations between all attribute pairs and only show those with a correlation above some threshold.

One pitfall to be aware of when showing the result of some kind of analytics is to not mislead the viewer. It is good practice to allow the viewer to see the raw data together with the results of clustering or smoothing so that the can judge the efficacy of the fit.

## General usability and interaction guidelines

The development of visual analytics tools is an application of human-centerer design. The acronym PACT (People, Activities, Context and Technology) summarises this approach. The designer needs to understand the background and skills of the people who will use the system and take account of their perceptual and cognitive abilities. They need to involve these end-users in the design of the system from the very beginning and really listen to their advice and criticisms.  They need to understand what they want to use the system for, the context in which it will be used and what sort of technology it will need to run on. It is worth emphasising again the need to design and test the application with real users all the way through implementation. For me this is the golden rule of HCI (Human Computer Interaction) design.

There are of course many other principles in effective HCI design. These include ensuring that new users can quickly learn how to use the tool. This requires using familiar conventions and using a consistent and predictable interaction model. The interface should allow the user to complete their tasks _flexibly_ by not unnecessarily constraining the order of operations and by allowing them to customise it to their needs and wants. Finally the system should be robust. Visual feedback should let the user know in what state the system is in and it should be easy to recover from mistakes.

When developing an interactive system it is important to think about latency: how long will it take for the system to respond to the user. This significantly affects the user experience. The system will feel responsive if the system provides feedback in the following time scales (Table based on Table 6.1 from _Visualization Analysis and Design_ by T. Munzner, 2014):

| Level of Responsiveness | Response Time (in seconds) |           Example           | 
|:------------------------|:---------------------------|:----------------------------|
|  Perceptual processing  |             0.1            |        Screen update        |
|    Immediate response   |              1             | Visual feedback on selection or animated transition between frames |
|      Brief task         |             10             |       Sort or filter        |

From the user’s perspective it is important for the system to provide feedback, usually visual, that the action they have requested has been completed.  Highlighting selected elements is an example of visual feedback. If the operation is going to take longer than they might expect then some kind of visual indication of progress is a good idea.

## Summary

In this topic we have investigated how to design visual analytics tools and interfaces. This is a complex area and requires understanding basic HCI design principles and methodologies. In my view the most important is to employ a participatory design process in which the end-users of the system are involved in the design from the very beginning and are frequently given the opportunity to provide feedback on the evolving design.

We have looked at the kinds of tasks the tool should support and also key elements in the interface such as view manipulation and navigation, linking different views, and kinds of analytics to provide.

*** 

REFERENCES AND FURTHER READING
This topic is based upon

Pretorius, A. Johannes, Helen C. Purchase, and John T. Stasko. Tasks for multivariate network analysis. In _Multivariate Network Visualization_, pp. 77-95. Springer International Publishing, 2014.

Ward, Matthew O., Georges Grinstein, and Daniel Keim. Chapters 11-13 of _Interactive data visualization: foundations, techniques, and applications (2nd Ed)_. CRC Press, 2015.

Munzner, Tamara. Chapters 11-14 of _Visualization Analysis and Design_. CRC Press, 2014.

Further reading

* Chapters 11-14 of Munzner, 2014.

