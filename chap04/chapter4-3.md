# Activity: Relational data analysis and visualisation with R

## Relational/network data & visualizations

We can represent networks or relationships (think of a family tree, or social groups) as graphs. Starting with Part A, basic graphs, then Part B, adding direction ( e.g. ‘friend’ may not have a known direction but ‘child’ does) then looking at some analytics (Part C), i.e. who are the people in the centre of a network (think the office manager in an organisation), how strong are connections, who is or is not connected to whom.

We’re going to introduce and look at the following aspects of networks:

* nodes
* edges
* direction
* weights
* degree
* diameter
* sub graphs

Networks or graphs or network graphs have nodes (also called vertices), usually things like people  and edges (sometimes called arcs) which connect two nodes and which represent a relationship such as “friend” or “owes-money”. The edges are said to be weighted if they have a value. e.g. A owes B $10.

A network graph is called directed if the edges have a direction e.g. I owe you money, you owe him money, he owes me money, (let’s just call the whole thing off).

Which you could represent as: me->you, you->him, him->me

## A. Basic graphs {-}

We use the igraph library http://igraph.org/r/

Start by specifying a graph using numbers to represent nodes such that a pair of numbers means a connection e.g:

* 1-2, 1-3, 2-3, 3-4

Which would give us 4 nodes where 1 has and edge with (is connected to) 2 and 3, 2 to 3, and 3 to 4.

The first thing you want to do is to store this data in R.

Here are two different way of presenting this data in R (you will have the same result):


```r
library(igraph)
g <- graph.formula(1-2, 1-3, 2-3, 2-4) # the connections, 1 to 2, 1 to 3 etc.
# or g <- graph(c(1,2,1,3,2,3,2,4), directed = FALSE)
```

And display

```r
plot(g)
```

Let’s investigate the important properties of a graph.

**Vertices** first, should be 4

```r
V(g)
```

**Edges** then, should be also 4

```r
E(g)
```

What are other important properties?

**Diameter**, of course.

If you do not know what it is, have a look at: http://stackoverflow.com/questions/3174569/what-is-meant-by-diameter-of-a-network

Do not confuse it with circle diameter, although they have some similarities.


```r
diameter(g)
```

Node-link is not the only way to present a graph.

Another common way is the **adjacent matrix**.


```r
get.adjacency(g) # a matrix view
```

Nodes deserve to have names.


```r
V(g)$name <- c("Adam", "Bob", "Con", "Doug")
# and replot using $name
plot(g, vertex.label = V(g)$name) # add labels
get.adjacency(g) # have a look at the new matrix
```

## B. Directed graphs {-}

In some use cases, **directions** are very important.

So, how to present the directed graph in R?

Direction is usually represented by an arrow in real life, here, let’s pretend it means ‘owes money to’

The syntax is a little strange in R, ‘1-+2’ means ‘edge from 1 to 2’

or you can use directed = TRUE then the order specifies direction (so 1-2 IS NOT THE SAME as 2-1)


```r
dg <- graph.formula(1-+2, 1-+3, 2-+3, 2-+4) # so '1' owes '2'and '3' etc.
plot(dg)
```

<mark class="big">**Can you have both 1-2 and 2-1?**</mark>

<mark class="big">**Who does ‘4’ owe money to?**</mark>

Again, we need names to make it more readable (interesting), alphabetically such that ‘A’ is 1, ‘B’ is 2 etc.


```r
V(dg)$name <- c("Adam", "Bob", "Con", "Doug") # names! 
plot(dg, vertex.label = V(dg)$name)
```

We now have the connections, but every connection seems the same.

<mark class="big">***What’s the strength of the connection?*** **i.e. How much money does Adam owe Bob?**</mark>


```r
is.weighted(dg)
```

There are no ‘weights’ or debts… yet

Add (random) values to the connections (the edges):


```r
wdg <- dg # copy, wdg is going to be a weighted directed graph
E(wdg)$weights <- runif(ecount(wdg)) * 1000 # random debts, up to $1000
plot(wdg, vertex.label = V(wdg)$name, edge.width=E(wdg)$weights)
```

<mark class="big">**Oops, what happened!?** What are these weights anyway?</mark>


```r
E(wdg)$weights # as specified, random values from 0 to 1000
```

What happened is that we plotted edges, as lines, with widths up to 1000 (pixels), which is a mess, so be careful!

Now we scale them down.


```r
plot(wdg, vertex.label = V(wdg)$name, edge.width=E(wdg)$weights / 100) # so scale, but we might lose our arrows...
```

<mark class="big">Do you like the way R put your nodes? Let’s play with the layout.</mark>

There are lots of layouts in R.

Let’s try star first.


```r
plot(wdg, vertex.label = V(wdg)$name, edge.width=E(wdg)$weights / 100, layout = layout.star)
```

Actually, in RStudio, when you input the parameter: layout = layout. there will be a drop down box with different layout options.

Our debts graph is a bit basic (small) for layout testing, try a bigger one.

Note: some layouts have special requirement for the graph data, e.g. `bipartite`, look into them if you are interested!


```r
# http://www.r-bloggers.com/going-viral-with-rs-igraph-package/
 
G <- graph( c(1,2,1,3,1,4,3,4,3,5,5,6,6,7,7,8,8,9,3,8,5,8), directed = F )
 
# Assign attributes to the graph
G$name <- "Change my layout, I dare you"
 
# Assign attributes to the graph's vertices
V(G)$name  <- toupper(letters[1:9])
V(G)$color <- sample(rainbow(9),9,replace=FALSE)
 
# Assign attributes to the edges
E(G)$weight <- runif(length(E(G)),.5,4)
# Plot the graph
plot(G, layout = layout.auto, 
     main = G$name,
     vertex.label = V(G)$name,
     vertex.size = 25,
     vertex.color= V(G)$color,
     vertex.frame.color= "white",
     vertex.label.color = "white",
     vertex.label.family = "sans",
     edge.width=E(G)$weight, 
     edge.color="black")
```

<mark class="big">**Your turn, change the layout**</mark>

There are also a selection of built in layouts or types of graph e.g.


```r
par(mfrow=c(2,2)) # 2 x 2 display
 
g <- graph.full(n=5, directed = FALSE, loops = FALSE)
plot(g)
 
g <- graph.star(n=5, mode="out")
plot(g)
 
g <- graph.star(n=5, mode="in")
plot(g)
 
g = graph.ring(n=5)
plot(g)
```

If you get an error like:

Error in .Call.graphics(C_palette, value) : invalid graphics state

Please click the “cross” button at above the plot area (beside the broomstick button) .
If you get “plot region too large” in the plot area, please enlarge the plot area.

And we can add some colour:


```r
par(mfrow=c(1,1))
g <- graph.full(5)
E(g)$weight <- runif(ecount(g)) # random weights, run again for different result
E(g)$width <- 1
E(g)$color <- "red"
E(g)[ weight < 0.5 ]$width <- 2
E(g)[ weight < 0.5 ]$color <- "blue"
plot(g, layout=layout.circle, edge.width=E(g)$width, edge.color= E(g)$color)
E(g)$weight
```

Sub graphs (select part of a graph):


```r
g1 <- make_star(5)
g2 <- induced_subgraph(g1, 1:2) # select vertices 
g3 <- subgraph.edges(g1, 1:3, TRUE) # select edges
 
par(mfrow=c(1,3))
 
plot(g1)
plot(g2)
plot(g3)
```

## C. Analysis of Network Data {-}

### The Karate club {-}

Explore the famous Karate club network e.g. who are the major players (or actors), the groups.

Let’s look at the data first.


```r
library(igraphdata) 
data(karate) # load the built-in graph data
?karate
V(karate)
E(karate)
get.adjacency(karate)
```

Start by plotting the club in glorious colour with edges & nodes scaled to represent importance or weight.

1. Add label and define shape of vertices.


```r
# Reproducible layout
set.seed(42)
 
# Now decorate, starting with labels and shapes
V(karate)$label <- sub("Actor ", "", V(karate)$name)
V(karate)$shape <- "circle"
```

2. Distinguish the faction.


```r
# Differentiate two factions by color.
V(karate)[Faction == 1]$color <- "red"
V(karate)[Faction == 2]$color <- "dodgerblue"
```

3. Make the most popular one more obvious (make the circle proportional)
<br>
**Investigate what is graph strength.**


```r
# Vertex area proportional to vertex strength
# (i.e., total weight of incident edges).
V(karate)$size <- 4*sqrt(graph.strength(karate))
V(karate)$size2 <- V(karate)$size * .5
```

4. Make the connections proportional

```r
# Weight edges by number of common activities
E(karate)$width <- E(karate)$weight
```

5. We definitely want to find out are there communications within/between faction?

Color the edges!

```r
# Color edges by within/between faction.
F1 <- V(karate)[Faction==1]
F2 <- V(karate)[Faction==2]
E(karate)[ F1 %--% F1 ]$color <- "pink" # F1 to F1 i.e. internal
E(karate)[ F2 %--% F2 ]$color <- "lightblue"
E(karate)[ F1 %--% F2 ]$color <- "yellow"
```

6. If the vertex is too small, you cannot see the labels.

```r
# Offset vertex labels for smaller points (default = 0). # or make all the circles bigger...
V(karate)$label.dist <- ifelse(V(karate)$size >= 10, 0, 0.75)
```

7. Make the layout and plot

```r
l <- layout.kamada.kawai(karate)
plot(karate, layout=l)
```

If you do not like it, **try other layouts!**

Based on: https://github.com/kolaczyk/sand/blob/master/sand/inst/code/chapter3.R

Are there many within/between communications?

### Centrality {-}

A major focus in network analytics is to measure the importance or centrality of nodes:

* Degree – the simplest measure, the higher the degree the more important a node is (more edges = more connections).
* Closeness centrality – captures the idea that a node is central if it is close to many other nodes: this measure varies inversely with the total of the node’s graph theoretic distance to all other nodes in the graph.
* Betweenness centrality – summarises the extent to which the node lies between the other nodes: it is based on counting the number of shortest paths that pass through n.
* Eigenvalues – Status or rank centrality is based on the assumption that a node is more important if it has important neighbours. These are found using eigenvalues and eigenvectors.

It is common to use a node-link diagram in which nodes are placed radially with the nodes of most centrality at the center.

Let’s prepare the data first.


```r
library(sand) # Statistical Analysis of Network Data with R
library(sna) # Tools for Social Network Analysis
library(network)
 
A = get.adjacency(karate, sparse=FALSE) 
 
g = network::as.network.matrix(A) # make a matrix
```

Let’s plot it.

These take a while to render… patience:


```r
lpar(mfrow=c(1,1))
sna::gplot.target(
  g, degree(g), main="Degree", 
  circ.lab = FALSE, # change to TRUE to see legend on concentric blue circles
  circ.col="skyblue", usearrows = FALSE, 
  vertex.col=c("blue", rep("red", 32), "yellow"),
  edge.col="darkgray"
)
```

**What’s the blue circle, the yellow one?**

Let’s try other measurements.


```r
par(mfrow=c(2,2))
 
sna::gplot.target(
  g, degree(g), main="Degree", 
  circ.lab = FALSE, # change to TRUE to see legend on concentric blue circles
  circ.col="skyblue", usearrows = FALSE, 
  vertex.col=c("blue", rep("red", 32), "yellow"),
  edge.col="darkgray"
)
 
sna::gplot.target(g, closeness(g), main="Closeness",
                  circ.lab = FALSE, circ.col="skyblue",
                  usearrows = FALSE,
                  vertex.col=c("blue", rep("red", 32), "yellow"),
                  edge.col="darkgray")
 
sna::gplot.target(g, betweenness(g), main="Betweenness",
                  circ.lab = FALSE, circ.col="skyblue", 
                  usearrows = FALSE,
                  vertex.col=c("blue", rep("red", 32), "yellow"),
                  edge.col="darkgray")
 
sna::gplot.target(g, evcent(g), main="Eigenvalue",
                  circ.lab = FALSE, circ.col="skyblue",
                  usearrows = FALSE,
                  vertex.col=c("blue", rep("red", 32), "yellow"),
                  edge.col="darkgray")
```

<mark class="big">**We can’t see who’s who so turn labels on with:**</mark>

`displaylabels = TRUE`

https://www.uni-due.de/hummell/man/sna/.sna.gplot.pdf


```r
par(mfrow=c(2,2))
 
sna::gplot.target(
  g, degree(g), main="Degree", 
  circ.lab = FALSE, # change to TRUE to see legend on concentric blue circles
  circ.col="skyblue", usearrows = FALSE, 
  vertex.col=c("blue", rep("red", 32), "yellow"),
  edge.col="darkgray", displaylabels=TRUE
)
 
sna::gplot.target(g, closeness(g), main="Closeness",
                  circ.lab = FALSE, circ.col="skyblue",
                  usearrows = FALSE,
                  vertex.col=c("blue", rep("red", 32), "yellow"),
                  edge.col="darkgray", displaylabels=TRUE)
 
sna::gplot.target(g, betweenness(g), main="Betweenness",
                  circ.lab = FALSE, circ.col="skyblue", 
                  usearrows = FALSE,
                  vertex.col=c("blue", rep("red", 32), "yellow"),
                  edge.col="darkgray", displaylabels=TRUE)
 
sna::gplot.target(g, evcent(g), main="Eigenvalue",
                  circ.lab = FALSE, circ.col="skyblue",
                  usearrows = FALSE,
                  vertex.col=c("blue", rep("red", 32), "yellow"),
                  edge.col="darkgray", displaylabels=TRUE)
```

### Edge centrality {-}

Most network analysis focuses on the nodes/vertices but edges are important too.

Let’s calculate the betweenness for edges.


```r
eb = edge.betweenness(karate) # metric on the edges
```

**What is betweenness?**

Find out which edges are the top 3.


```r
E(karate)[order (eb, decreasing = T)[1:3]]
# One by one
E(karate)[order (eb, decreasing = T)[1]] # 
E(karate)[order (eb, decreasing = T)[2]] #
E(karate)[order (eb, decreasing = T)[3]] #
```

Have a look at the adjacency and look for ’20 & ’32’


```r
par(mfrow=c(1,1))
G <- graph.adjacency(A)
plot(G) # actually it is hard to see
plot(G, vertex.size=5, layout = layout.davidson.harel) # still hard to see 
 
plot(G, vertex.size = 5, vertex.label.dist = 0.5, edge.arrow.size = 0, layout = layout.kamada.kawai) # that's much better
# now look for '20' & '32'
```

Let’s cluster the vertices into different groups by using the **edge measurements (betweenness and short random walks).**


```r
par(mfrow=c(1,2)) # make two plots side by side
 
kk.layout <- layout.kamada.kawai(G) # make a consistent layout for the graphs
# make the left plot
com <- edge.betweenness.community(G)
V(G)$color <- com$membership+1
plot(G, vertex.label.dist=.75,layout=kk.layout,
     main="Edge-Betweenness Communities",
     edge.arrow.size=0.25)
 
# make the right plot
com <- walktrap.community(G)
V(G)$color <- com$membership+1
plot(G, vertex.label.dist = .75, layout=kk.layout,
     main="Walktrap Communities",
     edge.arrow.size=0.25)
```

<mark class="big">What is ‘walktrap’?</mark>








