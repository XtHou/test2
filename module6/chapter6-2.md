# Immersive analytics

In a [Brief history of data visualisation]() we looked at the reasons for the rise of data visualisation and visual analytics. One of the most important was changing technology for producing and presenting graphics. Widespread use of information graphics could not have happened without paper and printing while interactive data visualisation and visual analytics was not possible before the computer. In this topic we look at what new and emerging display and interaction technologies might mean for data science.

![Large tiled-displays with touch and gesture controlled interaction provide the possibility of deep collaboration between data scientists. <br> License: Copyright © Monash University, unless otherwise stated. All Rights Reserved.](diagrams_datasets/section2/ContextuWall-300x213.jpg)  

![Augmented reality promises distributed collaboration between data scientists working in shared virtual environments. <br>License: Copyright © Monash University, unless otherwise stated. All Rights Reserved.](diagrams_datasets/section2/ARVis-300x280.png) 

## New technologies

Virtually all tools for interactive data exploration and visual analytics are targeted towards a standard desktop computer: a single average-sized display, keyboard and mouse. This is not surprising as this is the standard computing environment in business, science and government. However this is changing.

On one hand, we have  the development of expensive bespoke technologies, mainly for scientific visualisation. For example, ultra-high resolution virtual reality environments like the [Monash CAVE2<sup>TM</sup>](https://www.monash.edu/researchinfrastructure/mivp) use wall-mounted displays and head tracking equipment to immerse users in 2D and 3D visualisations. A classic use-case for the CAVE2 is “walk-throughs” of human-scale architectural and engineering models.

<iframe width="730" height="411" src="https://www.youtube.com/embed/xUwR2jKpbsE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

To see the CAVE2 in action take a look at the above video.

On the other hand, we also have the recent entry of touch screens and touch tables into the mainstream marketplace as well as the arrival of technologies such as the Leap Motion, Kinect, zSpace, Oculus Rift and (soon) Microsoft HoloLens. These new devices potentially provide more natural user interfaces than the traditional mouse and keyboard and immersive 2D and 3D visualisations that move far beyond the current HD desktop monitor.  Industry—in particular the entertainment industry— has driven this development and it has progressed rapidly, providing immersive visualisation for a fraction of the cost of the CAVE. As a first step in this direction Tableau have just released [Vizable](https://vizable.tableau.com) an iPad app for visual analytics.

The amount of new, low-cost interaction technology hitting the market is unprecedented. Given the rise of new manufacturing technologies (additive manufacturing) and business models (crowdfunding, etc.) the rate of innovation in display and interaction devices is only going to increase.

## Immersive analytics

I believe it is likely that, like other innovations in graphics production and display technologies have done, the arrival of these new low-cost interaction and display technologies will reshape data visualisation.

At Monash we have a new research initiative exploring how these new user interface and virtual reality technologies can be used in data analytics and data science. We call this [initiative Immersive Analytics](https://www.monash.edu/it/our-research/research-strengths/immersive-analytics). Some of the things we are looking at are:

* *To 3D or not to 3D*: As we have discussed there are currently good reasons to limit the use of 3D when visualising abstract data: occlusion, distortion introduced by perspective and difficulty of interaction. However the new technologies potentially mitigate some of these problems and so the use of 3D for abstract data visualisation may well become more popular.
* *Mixed 2D and 3D visualisation*: 3D visualisation has been used in the physical sciences, engineering and design, and for geospatial analysis while 2D visualisations are used to show tabular and network data. In many larger, multidisciplinary projects, there is a need to combine both sorts of visualisations. For instance, in the life sciences different aspects of a cell are shown using 3D volumes, 2D images and 2D multivariate network data. Emerging technologies provide support for this by allowing holistic visualisations incorporating  both 3D and 2D.
* *Interaction and interface design*: What are the interface ‘tricks’ and affordances such as high-resolution displays, sound, touch and responsive interaction that change the user perception from an allocentric view of the data to a more egocentric and immersive view of the data? What kinds of interaction and interaction devices will allow the user to work as comfortably and productively with 3D data in an AR and VR environment as they can currently work with 2D data in a desktop environment.
* Visualisation platform: While there many information visualisation libraries, like **D3** or **ggplot2**, these are not designed to work with immersive visualisation environments. On the other hand **Unity** is designed for gaming applications rather than analytics while the **Visualization Toolkit (VTK)** is targeted at scientific visualisation applications but not information visualisation. We need information visualisation toolkits that work with immersive visualisation platforms.

These new technologies also open up new opportunities for visual analytics:

* *Immersive narrative visualisation*: The first is to use immersive VR and AR for more effective and engaging presentations to stake-holders such as managers, policy makers and the general public.  Immersive VR is routinely used to present architectural and engineering designs to clients but its use for presenting abstract data to stakeholders has not been considered. Imagine the power of a presentation about health risks or emergency response planning in which the city is modelled in the space around the viewer and key problems are highlighted through data overlays directly on the model which the viewer can interactively explore.
* *Situated analytics*: Augmented reality (AR) displays potentially allow applications to overlay analytics onto objects in the actual physical environment. This could allow environmental scientists or farmers to see sensor data overlaid on top of the landscape they are standing in and perform data analysis in situ. Shoppers could overlay nutritional, environmental and ratings and comments from social media on products as they stroll down the shopping aisle.  No longer must the visual analyst sit at a desk, AR allows visual analytics out into the real-world, potentially ubiquitous and part of everyday life.
* *Collaboration*: Traditionally data scientists perform data analysis  individually, and then report back what they have found. Devices like the CAVE and Oculus Rift potentially support much deeper collaboration between data scientists.

## Representative examples

Here are some examples showing the sort of data visualisation that immersive visualisation environments will support.

The first example is shown in the video clip above. It is a virtual reconstruction of the ancient Angkor temple complex in Cambodia displayed on Monash’s CAVE2 visualisation facility. The reconstruction is programmed in Unity, a popular gaming engine. Not only does this provide a 3D model of the site, but also uses rule-based using multi-agent simulation to reconstruct human activity in and around the complex. Data gathered from the simulation can then be explored using overlaid heatmaps of traffic flows. As well as supporting the evaluation of archeological hypotheses, e.g. on settlement density, detailed 3D interactive animations like that of Angkor are potentially a powerful way to communicate findings to stakeholders.

The second example also utilises the CAVE2. This time the application is ContextuWall, an application that supports distributed collaborative decision making. In this application the images are mirrored on the displays in different locations. Viewers at all locations can interact with the display through their favourite touch screen device by using a finger to “flip” new images on to the shared display or remove, annotate the images and also position them.

![ContextuWall distributed collaboration application running in the CAVE2 at Monash <br> License: Copyright © Monash University, unless otherwise stated. All Rights Reserved.](diagrams_datasets/section2/ContextuWall_Photo-768x512.jpg) 

The third example is another example of collaborative data analysis, but this time with the Oculus Rift personal virtual reality environment. Here we see the two analysts looking at air traffic control data. They can see where the other person is looking and direct them to points of interest.

![Virtual collaboration using the Oculus Rift at Monash SensiLab. <br> License: Copyright © Monash University, unless otherwise stated. All Rights Reserved.](diagrams_datasets/section2/Oculus1-768x434.png) 

## Summary

We can see that new display and interaction technologies will completely change the way in which we can interact with the computer. It is likely that these will also impact on visual analytics and lead to much greater use of immersive visualisation for more abstract data analysis, particularly for collaborative analysis.

*CAVE2 is a trademark of the University of Illinois Board of Trustee*

*** 

FURTHER READING

ElSayed, N., Thomas, B., Marriott, K., Piantadosi, J., & Smith, R. (2015, September). Situated Analytics. _In Big Data Visual Analytics (BDVA)_, 2015 (pp. 1-8). IEEE.

Chandler, T., Cordeil, M., Czauderna, T., Dwyer, T., Glowacki, J., Goncu, C., Klapperstueck, M., Klein, K., Marriott, K., Schreiber, F. and Wilson, E., 2015, Immersive Analytics. In _Big Data Visual Analytics (BDVA)_, 2015 (pp. 1-8). IEEE.

