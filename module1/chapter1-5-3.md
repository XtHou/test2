## Activity: Exploring & Visualising Data with D3'

In this activity, you are going to use D3 to build a choropleth map.

Do not worry, it will be easier than you expect…

### Introduction

[D3](). (**Data-Driven Documents**) is a HTML5/SVG + JavaScript based data visualisation toolkit. It allows you to create dynamic and interactive data visualisation that can be viewed in a  web browser. D3 is a JavaScript library. JavaScript is a programming language for web pages. It is used to create web pages from dynamic content and change them in response to user interaction. Along with HTML and CSS it is one of the pillars of modern web page design.

D3 has its origins in [Protovis](https://ieeexplore.ieee.org/document/5290720/). D3 is extremely powerful and allows you to create almost any kind of visualisation you can imagine. You can have a look at some of the examples:
https://github.com/mbostock/d3/wiki/Gallery

If you look at the code you can see that this power comes at a price: D3 is quite complicated and relies on several different concepts. However, in this activity, we are not going to dive into all the details. Instead, you can have some hands-on experience of using D3. Later in the unit you will learn more about D3. Or if you cant wait there is  a free comprehensive online tutorials of D3:

[D3 Tutorials by Scott Murray](http://alignedleft.com/tutorials/d3)

If you are unfamiliar with JavaScript you might like to look at the W3C tutorial on JavaScript https://www.w3schools.com/js/

### Preparation

* Download the [map file](https://www.alexandriarepository.org/wp-content/uploads/20180220170945/us-states.txt). 
<br>
This file contains the details of maps of different states in USA. Basically, it keeps the records of geographic shapes, like lines, points and etc.
<br>
(optional) Check out http://geojson.org/ for more details.

* Download the [data](https://www.alexandriarepository.org/wp-content/uploads/20180213213252/MobileHomes.csv)
<br>
License: CC Attribution 4.0 International (CC BY 4.0)
<br><br>
To be consistent, we are going to use the same data we used in our R activity.
D3 (or even JavaScript) is not the ideal tool for data processing, so here we use the aggregated data which was calculated by the **$\color{#228B22}{\text{aggregate}}$** function in R.

* Set up a static web server
<br>
For security reason, browsers cannot access local files directly, so a static web server needs to be set up to allow our D3 script to load data. The easiest way to do this is to download
<br>
http://brackets.io/. This is a free text editor with live preview feature which runs a static web server at the back end.  However you can use your favourite text editor and skip this step if you already know how to set up a static web server.
<br>
(Optional)If you prefer to launch a static server, you can do this with:
   
    + Install Python (on Windows, Python should be installed by default for most Linux and Mac OS)
    + Adding Python to your system path (on Windows)
    + Use a terminal (command line) to enter your project directory/folder (with cd command)
    + Running the command:
    <br>
    (for python 2) python -m SimpleHTTPServer 8000
    <br>
    (for python 3) python -m http.server 8000
    + Then you can open http://localhost:8000/ in your browser to access your D3 visualisations.
    
### Set up an HTML page

Using the menu $\color{#34a10a}{\text{File -> New}}$ to create an empty file, save it to the folder you keep all the data you downloaded, with the name us-map.html (of course change the name if you do not like it).

Let’s create a basic HTML page with:


```javascript
<!DOCTYPE html>
<html>
    <head>
        <title>US Mobile Homes choropleth map</title>
    </head>
    <body>
        <svg></svg>
    </body>
</html>
```

If you are using Brackets, click the “lightning” icon on the right to view this very new webpage.

As expected, you will see a blank page, however, if you are careful enough you can find the text on the tab of the browser is “US Mobile Homes choropleth map”.

### Initialise svg canvas

We need a canvas to draw our visualisation.

Luckily, we already defined our $\color{#34a10a}{\text{svg}}$ element in the HTML. (SVG is the HTML5 standard for vector graphics)

We will take advantage of D3’s

* $\color{#34a10a}{\text{selection}}$ function to access the svg element
* $\color{#34a10a}{\text{attr}}$ function to modify the attributes of the svg element, and
* $\color{#34a10a}{\text{style}}$ function to modify the style of the svg element

First, we need to reference D3 library in our webpage, add


```javascript
<script src="https://d3js.org/d3.v4.min.js"></script>
```

to the body section of our HTML.

Create another script section for our own JavaScript code, and initialise the svg element. The whole HTML should look like:


```javascript
<!DOCTYPE html>
<html>
    <head>
        <title>US Mobile Homes choropleth map</title>
    </head>
    <body>
        <svg></svg>
        
        <script src="https://d3js.org/d3.v4.min.js"></script>
        
        <script>
            var width = 960;
            var height = 500;
            
            var svg = d3.select("svg")
                .attr("width", width)
                .attr("height", height)
                .style("border", "1px solid");
        </script>
    </body>
</html>
```

Refresh the webpage in your browser: you should now see our canvas.

Of course, if you are experienced with web development, you know this process could be done without javascript and you could simply write the SVG code

Here we want to demonstrate some basic functions of D3.

### Reading data

We will take advantage of D3’s request functions to load data. (Optional) More details at: https://github.com/d3/d3/blob/master/API.md#requests-d3-request

We can use $\color{#34a10a}{\text{d3.json}}$ and $\color{#34a10a}{\text{d3.csv}}$ function to load our map and data respectively.


```javascript
<!DOCTYPE html>
<html>
    <head>
        <title>US Mobile Homes choropleth map</title>
    </head>
    <body>
        <svg></svg>
        
        <script src="https://d3js.org/d3.v4.min.js"></script>
        
        <script>
            var width = 960;
            var height = 500;
            
            var svg = d3.select("svg")
                .attr("width", width)
                .attr("height", height)
                .style("border", "1px solid");
            
            d3.json("us-states.txt", function(mapData){
                d3.csv("MobileHomes.csv", function(data) {
                    
                });
            });
        </script>
    </body>
</html>
```
### Draw the map

Let’s focus on the map first.

The map file is in GeoJson format and contains pure geographic information.

To draw a map, we need to convert the geographic information (latitude, longitude) to 2D coordinates for the screen (x, y).

This process is called map projection, you will learn (a lot) more details in the future in this unit.

D3 provides lots of different map projections! Probably the most comprehensive collection available in Javascript.  (Optional) https://github.com/d3/d3-geo-projection

We use the following code to define the map projection we are going to use later.


```javascript
// Map projection
var projection = d3.geoAlbersUsa()
  .translate([width / 2, height / 2]) // move the center of the map to the center of our canvas
  .scale([1000]); // scale things down so see entire US
// Define path generator
var path = d3.geoPath() // path generator that will convert GeoJSON to SVG paths
  .projection(projection); // tell path generator to use the previous map projection
```

After this, drawing the map is extremely easy:


```javascript
var states = svg.selectAll("path")
  .data(mapData.features) // bind the geographic data to svg elements
  .enter().append("path") // create one "path" svg element for each datum
  .attr("d", path) // using the map projection to convert geographic information to screen coordinates
  .style("stroke", "black") // change the style properties for the svg 
  .style("stroke-width", "1")
  .style("fill", "white");
```

Now, refresh your webpage, say hello to the US Map.

<br><br>

If you cannot see anything, probably it is again a trick about working directory.

Please use the menu on the top with “**File => Open Folder**” and choose the directory you kept all your files.

Then try the “lightning” button again.

### Color the map

We need a bit data processing first.

To make the color of different states proportional to its value, we need to know:

* the value for each state
* the min and max value among all states

This can be achieved by:


```javascripts
var country2value = {};
var minValue = Infinity;
var maxValue = -1;
data.forEach(function(d){
    var thisValue = d["MobileHomes"];
    country2value[d["States"]] = thisValue;
    
    minValue = Math.min(minValue, thisValue);
    maxValue = Math.max(maxValue, thisValue);
});
```

We also need a color mapping to map the values to colors.

One good possible option is to use the $\color{#34a10a}{\text{d3-scale-chromatic}}$ library. 
<br>
(Optional) https://github.com/d3/d3-scale-chromatic

Let’s reference this library first:

```{}
<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
```

Here, to make choropleth map for comparing values, we want to map the  continuous values to $\color{#34a10a}{\text{Sequential}}$ colors.

This kind of color mapping accepts parameters of numbers from 0 to 1 and mapping them to related colors.

Usually light colors stand for small values, and dark ones for large values.

Two mappings need to be created:

* map values to the range of 0-1
* map the above outputs to colors


```javascript
var value2range = d3.scaleLinear()
    .domain([minValue, maxValue])
    .range([0, 1])
var range2color = d3.interpolateBlues;
```

Thanks for your patience, now it is the time to finish with just a few more line of code.


```javascript
states.style("fill", function(d){
    return range2color(value2range(country2value[d.properties.name]));
});
```

<br><br>

The whole web page should look like:

```{}
<!DOCTYPE html>
<html>
    <head>
        <title>US Mobile Homes choropleth map</title>
    </head>
    <body>
        <svg></svg>
        
        <script src="https://d3js.org/d3.v4.min.js"></script>
        <script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
        
        <script>
            var width = 960;
            var height = 500;
            
            var svg = d3.select("svg")
                .attr("width", width)
                .attr("height", height)
                .style("border", "1px solid");
            
             // Map projection
            var projection = d3.geoAlbersUsa()
              .translate([width / 2, height / 2]) // move the center of the map to the center of our canvas
              .scale([1000]); // scale things down so see entire US
            
            // Define path generator
            var path = d3.geoPath() // path generator that will convert GeoJSON to SVG paths
              .projection(projection); // tell path generator to use the previous map projection
                
            
            d3.json("us-states.txt", function(mapData){
               
                var states = svg.selectAll("path")
                  .data(mapData.features) // bind the geographic data to svg elements
                  .enter().append("path") // create one "path" svg element for each datum
                  .attr("d", path) // using the map projection to convert geographic information to screen coordinates
                  .style("stroke", "black") // change the style properties for the svg 
                  .style("stroke-width", "1")
                  .style("fill", "white");
                
                d3.csv("MobileHomes.csv", function(data) {
                    
                    var country2value = {};
                    var minValue = Infinity;
                    var maxValue = -1;
                    data.forEach(function(d){
                        var thisValue = d["MobileHomes"];
                        country2value[d["States"]] = thisValue;
                        
                        minValue = Math.min(minValue, thisValue);
                        maxValue = Math.max(maxValue, thisValue);
                    });
                    
                    var value2range = d3.scaleLinear()
                        .domain([minValue, maxValue])
                        .range([0, 1])
                    
                    var range2color = d3.interpolateBlues;
                    
                    states.style("fill", function(d){
                        return range2color(value2range(country2value[d.properties.name]));
                    });
                });
            });
        </script>
    </body>
</html>
```

<br><br>

**QUESTION**: Compare D3 with R and Tableau Public for data visualisation – which do you prefer and why?

***










