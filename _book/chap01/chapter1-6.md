# Designing Data Visualisations

One of the most widely used frameworks for understanding the design and evaluation of data visualisations was developed by Tamara Munzner. This has three parts:

* **What** is the kind of data to be visualised?
* **Why** is the data being visualised–what task does the user wish to perform?
* **How** is the data visually represented and what interaction is provided

Questions come from application and do not care about the ***how*** (at first).

## What: Kinds of data

Different sorts of visualisation are appropriate for different kinds of data. I’ll use the following classification for different kinds of datasets and different kinds of data. In this unit we will be mainly interested in four kinds of dataset:

* *Tabular dataset*: By this I mean data that is conceptually organised into a table with each row corresponding to a different data point or item and each column corresponds to different attributes of the data. This is the sort of data that traditional statistics works with and that R is designed for.
* *Network dataset*: This is data that consists of nodes or items  and links between these nodes which represent different kinds of abstract relationships such as ‘reports-to’ or ‘is-married-to’. The items can contain attributes. A *hierarchy* is a kind of network dataset.
* *Spatial dataset*: This is data in which items are associated with a geographic location or region and this geographic key is a natural way in which to organise and understand the data.
* *Textual dataset*: this kind of data set consists of sequences of words and punctuation.

These are not the only kinds of way data can be organised but they are the most common kinds of dataset used in data science and data visualisation. One other way of organising data used in scientific visualisation is the _field_ in which data is sampled from a continuous, conceptually infinite domain.  An example of a data organised as a field is an X-ray image.

Attributes in data items are simple values that can be measured or logged. They can be

* *Categorical*: data that does not have an inherent ordering. It is often organised into a hierarchy. Examples include names.
* *Ordered*: data that can be ranked or ordered. It has two subtypes
    + *Ordinal*: data that can be ranked but for which the difference between items does not make arithmetic sense. Examples include clothes’ sizes (small, medium, large) and survey response scales such as one that allows respondents to select from a 5-point scale such as  ‘disagree strongly’, ‘disagree’, ‘neutral’, ‘agree’, ‘agree strongly’.
    + *Quantitative*: data that has a magnitude supporting arithmetic comparison. For instance height or weight. This may be integer or a real number. Time is an important example of quantitative data. Sometimes quantitative data is split into _interval_ vs _ratio_ data but this distinction is usually not that important. The difference is that ratio data has a natural 0 while interval data does not. Thus length is an example of ratio data while date is an example of interval data.
    
Ordered data can either be _sequential_, in which case there is a minimum and maximum value, or _diverging_ in which case it can be understood as two sequences going in opposite directions, e..g. like/dislike scales from -5 to 5 are diverging around the neutral value of 0. Ordered data can also be cyclic where the values wrap around. Time measurements are often cyclic, e.g. months in the year.

The data being displayed is not only the original data but maybe data, such as statistical values, computed from the original data.

## Why: The tasks

When designing a visualisation it is fundamental to understand what are the high-level goals and tasks it needs to support. There have been many classifications of these.

*Discovery*: The fundamental task that an analyst wants to achieve is to derive insight or knowledge from the data. The desired outcome might be to formulate a hypothesis (“discover the unexpected”) or to test a hypothesis (“confirm the expected”). The hypotheses may take the form of cause-and-effect relationships, trends, correlations or clusters.

*Presentation*: This goal refers to presenting insight or knowledge that has already been found to some intended audience.

*Enjoy*: This goal refers to creating data visualisations that are intended to entice casual users to engage with the data. This might be for instance an attractive infographic or a visualisation like [Name Voyager](http://www.babynamewizard.com) which shows the evolution of children’s names.

We shall focus on the discovery task. This relies on performing a series of analytical tasks:

* *Search* for elements that satisfy certain properties, if they exist. This might be locating a known data point, filtering the data, or finding outliers.
* *Identify* the properties of a single data item
* *Compare* or *rank* elements
* *Visually* identify patterns in some subset of elements. Examples include trends, correlations, clusters or categories.
* Calculate *derived* properties not originally in the data. These may be data transformations, data aggregations or may be statistical properties such as regression lines or clusters

Analytical tasks rely on presentation tasks:

* *Visualise* by mapping elements and their attributes to visual variables to create a view
* *Manipulate (or configure)* a view by navigating and selecting subsets of elements

There are other user tasks that support analytical tasks

* *Annotate* visual elements with text or graphical elements
* *Record* visualisation elements so that they can be preserved and accessed outside the analytics tool. For example, Tableau records a graphical history, with snapshots showing how the current visualisation was reached
* *Revisit* an earlier visualisation or relocate an element or pattern that was previously found by the analyst

## How: The vis idioms

Once you know **what** you wish to visualise and **why** you want to visualise, you need to decide **how** best to visualise it. Munzner divides this into:

* **(Visual) Encoding**: how data is mapped to visual and spatial variables in each view;
* **Manipulate**: how the user interacts with the visualisation and data
* **Facet**: How different views are arranged and combined
* **Reduction and Statistical Analysis**: The different ways for aggregating, filtering and statistical analysis of the data.

## Summary

In this topic we have introduced Munzner’s **What-Why-How** framework for understanding data visualisation design. In subsequent modules we will look in more detail at common visual encodings and analysis for different kinds of data.

***

REFERENCES AND FURTHER READING

This topic is based upon

Munzner, Tamara. Chapters 11-14 of *Visualization Analysis and Design*. CRC Press, 2014.

Pretorius, A. Johannes, Helen C. Purchase, and John T. Stasko. Tasks for multivariate network analysis. In *Multivariate Network Visualization*, pp. 77-95. Springer International Publishing, 2014.

Ward, Matthew O., Georges Grinstein, and Daniel Keim. Chapters 11-13 of *Interactive data visualization: foundations, techniques, and applications (2nd Ed)*. CRC Press, 2015.

Further reading

* Chapters 2-3 of Munzner, 2014.


***


