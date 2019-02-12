# New sources of data

## Big data

We have talked about the future of data visualisation in terms of new kinds of display and interaction technologies. As we have discussed another driver for changes in data visualisation is the availability of data. And as data scientists we should be well aware that Big Data is here (see Wikipedia on [Big Data](https://en.wikipedia.org/wiki/Big_data)).

Some of the reasons for the massive increase in data are social media, higher resolution scientific instruments such as radio and optical telescopes, RFID and other object tagging, remote sensing and wireless sensor networks, software logs, cameras and microphones. Data visualisation is often promoted as one of the ways of handling such Big Data. This certainly has some truth but the immense size of the data sources, terabytes or even petabytes, means that considerable aggregation, filtering and selection is required before any kind of visualisation is possible. Visual analytics with its  human-in-the-loop exploration model using using both analytics and visualisation seems one of the best approaches.

\url{diagrams_datasets/section3/Viegas-UserActivityonWikipedia-300x226.gif}

Visualisation of daily Wikipedia edits taken from Wikipedia entry on Big Data by Fernanda B. Viégas. Wikipedia is terabytes in size and an example of big data. <br> License: Copyright © License: CC Attribution 2.0 Generic (CC BY 2.0) 

## Internet of Things (IoT)

One of the most interesting sources of Big Data is the _Internet of Things (IoT)_ or more grandiosely the _Internet of Everything (IoE)_. This is “the network of physical objects—devices, vehicles, buildings and other items embedded with electronics, software, sensors, and network connectivity—that enables these objects to collect and exchange data.” ([Wikipedia](https://en.wikipedia.org/wiki/Internet_of_Things)). A recent [blog](https://www.datasciencecentral.com/profiles/blogs/what-is-the-internet-of-everything-ioe) post on Data Science Central suggest that by 2020, this has the potential to connect 50 billion people, devices and things. That’s an awful lot of data and its coming very soon. Also see [How Big Will The Internet of Things Be?](https://datafloq.com/read/how-big-will-the-internet-of-things-be/523)

One of the characteristics of this kind of sensor data is that it is streamed (streamed data is V for Velocity in the The 4 Vs of Big Data (see the [IBM Infographic](https://www.ibmbigdatahub.com/infographic/four-vs-big-data))). Real time analysis and visualisation of  large quantities of streamed data is almost certainly going to be a  major preoccupation for data scientists in the next decade. A number of graphical tools based around the data flow programming paradigm are being developed to support this kind of analysis. Shown below are a couple of interactive tools that allow you to connect to various data sources and process them in a series of steps or a pipeline. Both node-red (IBM), and StreamTools (NYT) are free downloads if you would like to try either.

## Node-red

Instructions for installing and running node-red (Windows) and for setting up a Twitter feed using node-red are [here](diagrams_datasets/section3/Node-RED1.pdf)

If you just want to see node-red running:

<video width="320" height="240" controls>
  <source src="diagrams_datasets/section3/node-red-vs-Apple.mp4" type="video/mp4">
</video>


This video shows a twitter feed running at a reasonable speed, seems people are twittering about Apple constantly (and bear in mind you only get access to about 1% of feeds for free, see [firehose vs garden hose vs spritzer](https://www.adweek.com/socialtimes/twittery-things-you-forgot-existed/482699/)). The pipeline then feeds the tweets into a sentiment analysis node (essentially a dictionary that categorizes into positive, negative and neutral terms) which then splits into 3 output files. There’s also a ‘debug’ siding, so you can see what’s going on, output is far right. In the video debug is turned off and on, but note that the files will keep filling up even if it’s off.

StreamTools

(on a Mac)

<video width="320" height="240" controls>
  <source src="diagrams_datasets/section3/streamTools.mp4" type="video/mp4">
</video>

## Summary

Not only will new kinds of display and interaction devices change data visualisation. Another driver for change is Big Data and in particular the new kinds of streamed data available from massive interconnected sensor networks like the Internet of Things.




