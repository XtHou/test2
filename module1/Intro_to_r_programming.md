# Introduction to R programming"

The expectation is that you already know at least the basics of programming, but that you haven’t programmed in R previously. So here you are introduced you to R; installing it; its major features and basic programming concepts; its specific capabilities for doing probability and statistics; and a brief guide to reference material. All of these are well-documented on the Internet, so mostly this submodule will just provide a path through some of this literature. If you read through the links, install and do the exercises, and complete this module’s programming assignment, you will be well on your way with R programming. In subsequent modules we will freely illustrate data analysis concepts with R code.

R is free software that originally was modelled on the prior (rather expensive) statistical programming language and platform called S (see the [R](https://en.wikipedia.org/wiki/R_(programming_language)) and [S](https://en.wikipedia.org/wiki/S_(programming_language)) descriptions at wikipedia). Like much free software, students, researchers and academics around the world have made contributions to R, with the result that it has become quite a powerful statistical modeling programming language and is well worth learning.

## Installation and basics

The first step is to read [Torfs & Brauer’s “A (Very) Short Introduction to R” [pdf]](https://cran.r-project.org/doc/contrib/Torfs+Brauer-Short-R-Intro.pdf). It explains how to download and install R and RStudio from CRAN (the Comprehensive R Archive Network). (It explains this for Windows, but for Macs it’s also completely straightforward; [CRAN [website]](https://cran.r-project.org), by the way, stands for The Comprehensive R Archive Network and holds all the software and documentation you really need for R.) RStudio is a graphical user interface that make programming, testing and running R programs easier, so I recommend installing it. After installation, you should read through the rest of this introduction, doing the examples in R or RStudio (the “ToDos”). That will give you a decent start on programming, including R’s control structures, data structures, graphing, file operations, etc.

The first step in using RStudio should always be to set your working directory to the directory where your source or data are, using the **setwd()** command in your console. If you make that your habit, you will avoid a lot of confusion. You can always use **getwd()** to confirm your location.

## Reference material

When you have specific questions about what function to use for what, etc., there are a large number of good references for R. Here are some:

* The wikibooks’ [“R Programming” [website]](https://en.wikibooks.org/wiki/R_Programming). This includes quite a lot of easily accessed reference material. It also has introductory material and guides to statistical methods, such as clustering and maximum likelihood estimation.
* The [CRAN manuals [website; pdf]](https://cran.r-project.org/doc/manuals/). These include “An Introduction to R” [pdf, 100pp], installation details, a thorough language specification and the “R Reference Index”, which is a 9 MB pdf comprehensive manual.
* Johnson’s [“RTips. Revival 2014!” [website; pdf]](http://pj.freefaculty.org/R/Rtips.html) updates a document begun in 1999. This is (in pdf form) 72 pages of good guidance on using R for statistical tasks.

***







