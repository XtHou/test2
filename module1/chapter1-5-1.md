## Activity: Exploring & Visualising Data with Tableau Public'

### Tableau Public

One of the best Data Analysis tools according to KDnuggets is:

1. [Tableau Public](https://www.tableau.com/public): “Tableau democratizes visualization in an elegantly simple and intuitive tool.”
<br>
[Top 10 Data Analysis Tools for Business](https://www.kdnuggets.com/2014/06/top-10-data-analysis-tools-business.html)

The ‘Public’ in the name refers to the promotion of online sharing of visualisations (in fact the only way you can save them, see: https://public.tableau.com/s/gallery). 

Which may be why there’s a free version of the software available, download and install:
https://public.tableau.com/s/download

(Tableau Desktop is available for educational users if anyone is interested, and you can save your visulisations locally with it).

### A. Worksheets and Dashboards

#### Step 1. Get data ready

Download and examine the data “[Cultural-Exchange-International-Program-LA-Dept-of-Cultural-Affairs.xlsx](../data/Cultural-Exchange-International-Program-LA-Dept-of-Cultural-Affairs1.xlsx)” here:

![](diagrams/chapter1/section5/tableau-01-768x173.png)

<br>

The data is already in “**row-oriented tables**” format. Which means, in this data file:

* Each row is a entity (or an object, or a record)

* Each column is a property of this entity (or this object, or this record)

Usually, this is the preferred format for most tools and data processing languages (like R).

However, you cannot expect all data are in this perfect format. If it is not the case, do Data wrangling!

More information about file format can be found at: [Tableau Help: Tips for Working with Your Data](https://onlinehelp.tableau.com/current/pro/desktop/en-us/data_tips.htm).

#### Step 2. Load data into Tableau

Open Tableau Public (TP), there are two ways to load the data:

* at the left top click “**Excel**” and navigate to the file you just downloaded.

* Just drag your file and drop it into Tableau Public window.

![](diagrams/chapter1/section5/tableau-10-open.png)


#### Step 3.  Data Source View

TP will try to determine your **data types** automatically, the common types are:

* \# => numbers
* Abc => text (strings)
* An earth symbol => geographic/locations

Usually this automatic process works fine, but please remember to check that the data type inferred by TP is exactly the data type you want, sometime TP will make mistakes.

The most common mistake is that TP will sometimes treat longitude and latitude numbers as #, but we usually want them be treated as geographic type.

To change the type, just click the **symbol (#, Abc, Earth symbol and etc.)**.

![](diagrams/chapter1/section5/tableau-10-data-source.png)


#### Step 4. Create worksheet

Go to worksheet by clicking on $\color{#FF5733}{\text{‘Sheet 1’}}$ (at bottom of display, as shown below)


![](diagrams/chapter1/section5/tableau-10-sheet.png)

to see the TP interface:

![](diagrams/chapter1/section5/tableau-10-interface.png)

Shown on the left, data has been split into

* **Dimensions**; by default, Tableau treats any field containing qualitative, categorical information as a dimension;
* **Measures**;  and any field containing numeric (quantitative) information as a measure.

This modular treatment of information – that is to say, the treatment of individual data fields as independent components instead of an interdependent table – enables us to pick and choose what specific pieces of data we want to visualise against one another. 

Shown in the middle, top down, are ‘**Pages**’ ‘**Filters**’ and ‘**Marks**’ and then ‘**Columns**’ & ‘**Rowsm**’ then a ‘**Drop field here**’ table (you can drop fields on all of these middle controls):

![](diagrams/chapter1/section5/TP6.png)


#### Step 5. Create Visualisations

For our first visualisation, we will create a simple horizontal bar graph measuring City/Country against the Total Award Amounts granted to the artists from said locations.

* Drag ‘City,Country’ from **Dimensions** and drop it to **Rows**
* Drag ‘Total Award Amount’ from **Measures** and drop it to **Columns**
* Maybe also try to switch Rows and Columns

![](diagrams/chapter1/section5/tableau-10-first-bar-300x298.png)

#### Step 6

Try sorting by using the control attached to ‘‘Total Award Amount’ on the axis.

![](diagrams/chapter1/section5/tableau-10-sort.png)


#### Step 7

Imagine we wanted to see what individual grant amounts compose the Total Award Amount for each Country/Region. To achieve this, we would want to differentiate between “Grantees”. 

The “Marks” functions will allow you to insert further detail into your visualization.  Click and drag your “Grantee” dimension into the “Marks” table beneath the icons (as below). Your visualization should now feature individual segments, which you can click for details about all the dimensions and measures you have worked into your visualization (you can see for example that Cuba has two segments).

![](diagrams/chapter1/section5/TP8.png)

**Who were the two recipients in Havana, Cuba and how much?**

**(Notice the SUM(Total Award Amount) above, how about other measures, try max, min, total, mean..?)**

#### Step 8. One more dimension

We can add another dimension, e.g. ‘Discipline’ but let’s distinguish it somehow (colour!).
Drag ‘Discipline’ onto ‘Colour’:

![](diagrams/chapter1/section5/tableau-10-color-768x611.png)


**Which Discipline was granted the most, the least?**

**Which countries got funding for film?**

#### Step 9. Change colors

Don’t like those colours? By clicking the “Color” in the “Marks” window, you can customize the color palette, adjusting to the distribution of information present in your visualization.

![](diagrams/chapter1/section5/tableau-10-color-chooser-208x300.png)

Then ‘Edit colors’

![](diagrams/chapter1/section5/tableau-10-color-palette-300x271.png)


#### Step 10. Filtering

Filter by year. Drag ‘Year’ onto ‘Filters’ to see:

![](diagrams/chapter1/section5/tableau-10-year.png)


And ‘OK’ to select all (2009 to 2013). Now all this data is wrapped up and ready to go, let’s try a geographical view.

#### Step 11. Map

Start a new sheet, the icon to the right of ‘Sheet1’ below

![](diagrams/chapter1/section5/TP13.png)

Drag and drop ‘Country’ onto the table below ‘Rows’ (use the larger of the ‘Drop field here’ cells):

![](diagrams/chapter1/section5/tableau-10-country-768x611.png)

=>

![](diagrams/chapter1/section5/tableau-10-map-1-768x611.png)


This launches a map, change it from a symbol map to a **filled map** using the ‘Show me’ dialog at right, drag ‘Country’ onto ‘Label’ also:

![](diagrams/chapter1/section5/tableau-10-fuse-14-768x496.png)


Now look for the measures labeled ‘Latitude’ and ‘Longitude’

**What does ‘generated’ mean?**

#### Step 12. Color the map

Drag ‘Total Award Amount’ onto ‘Color’ (the default colour range is gradient green, change it if you hate green!):

![](diagrams/chapter1/section5/tableau-10-fuse-13-768x496.png)


#### Step 13. Combine work sheets into a dashborad

Combining sheets in a ‘New Dashboard’ (icon below)

![](diagrams/chapter1/section5/TP16-300x24.png)


Drag from top left to ‘Drop sheets here’

![](diagrams/chapter1/section5/tableau-10-fuse-15-768x496.png)


Optional: Share (if you have a tableau account).
(based on http://dh101.humanities.ucla.edu/wp-content/uploads/2014/09/Tableau_Public_Tutorial.pdf)

### B. Fuse tables

Sometimes (actually most of the time), the data is not stored in a single file.

For example, one file stores the **state name** and **state population** in Australia; another file stores the **state name** and **state population density** in Australia.

You want to explore the relationship between **population** and **population density** across different **states** in Australia.

For this very simple example, you could simply open Excel and copy and paste.

However, for real, large data, it takes ages to do so, as you have to link them correctly record (row) by record (row).

TP provides the functionality to fuse multiple data sets by linking records (rows) through the “linking property” you specify for each data set.

Now we are going to introduce the procedures.

Download the example data sets, they are ‘[Shape of US Congressional District Boundaries, 110th Congress](https://www.alexandriarepository.org/wp-content/uploads/20151013033033/Shape-of-US-Congressional-District-Boundaries-110th-Congress.csv)‘ and ‘[Household heating by Congressional District – 2008](https://www.alexandriarepository.org/wp-content/uploads/20151013033033/Household-heating-by-Congressional-District-2008.csv)‘.

#### Step 1. Load the first data set

Open TP first.

Drag the first data set “Shape-of-US-Congressional-District-Boundaries-110th-Congress.csv” and drop it into the TP windows.

![](diagrams/chapter1/section5/tableau-10-fuse-01-768x496.png)


#### Step 2. Load the second data set

Drag the second data set “Household-heating-by-Congressional-District-2008.csv” and drop it into the previous TP windows.

![](diagrams/chapter1/section5/tableau-10-fuse-021-768x497.png)


#### Step 3. Configure the fuse

You need to specify the way you want to fuse the data sets.

* left data: first data set, Shape-of-US-Congressional-District-Boundaries-110th-Congress.csv and

* right data: second data set, Household-heating-by-Congressional-District-2008.csv

The 4 different ways to fuse are (TP shows them with visulisations – Venn diagram!):

* Inner, only fuse the rows (with the specified property) where the same value exists in both the left data and right data, drop the rows where the value only exists in one side.

* Left, fuse the rows (with the specified property) that exist in the left data, and drop the row if it is in the right data but not in the left data.

* Right, fuse the rows (with the specified property) that exist in the right data, and drop the rows if it is in the left data but not in the right data.

* Full order, fuse the rows (with the specified property) that exist in either side.

<br><br>

You also need to specify the linking properties for each side. In this case, let’s choose

* “***id***” for the left
* “***Two-Digital District***” for the right

And “inner” model to fuse.

![](diagrams/chapter1/section5/tableau-10-fuse-03.png)

The fused table is shown in the “data view”.

Close the above window.

![](diagrams/chapter1/section5/tableau-10-fuse-04-768x496.png)

And now you can create your “sheet” and use properties from both table to implement your visulisations!

![](diagrams/chapter1/section5/tableau-10-fuse-05-225x800.png)

**Try different fuse models, and how many rows you can get in each way?**

### C. Choropleth Map

Choropleth map is a map with regions filled by different colors representing different properties.

One use case is using different color to present different type.

Another is using gradient color to present quantitative data.

You will learn more details in  [Module 3 of FIT5147](https://www.alexandriarepository.org/syllabus/making-sense-of-spatial-data/).

#### Step 1. Data always go first

Download the data from [Household-heating-by-State-2008.csv](https://www.alexandriarepository.org/wp-content/uploads/20151006100756/Household-heating-by-State-2008.csv) and “drag & drop”.

Make sure “State” column is marked as “geographic/locations”.

#### Step 2. Create the map

Create a new “Sheet”, and drag “States” to the center.

![](diagrams/chapter1/section5/tableau-10-fuse-07-768x496.png)

If you can see your map os US, congratulations! And you might choose to go to **Step 3** directly.

If your map cannot be generated properly, or you are looking at Australia, do not panic. This is not your fault, but TP has done something wrong.

Let’s fix it. Click on the top toolbar: **Map => Edit Locations**

![](diagrams/chapter1/section5/tableau-10-fuse-08-768x510.png)

You should look at the following window:

![](diagrams/chapter1/section5/tableau-10-fuse-09.png)

TP locate all your data into Australia……Maybe it is because of the self-locate service on your machine.

Anyway, change it to “United States” and press “OK”.

![](diagrams/chapter1/section5/tableau-10-fuse-10-768x496.png)


#### Step 3. Color the map

Drag “% Housing Units That Are Mobile Homes” to “Color” in “Marks” section.

Rename it if you think this name is so long…

![](diagrams/chapter1/section5/tableau-10-fuse-11-768x496.png)


#### Step 4. More map options

Click the top toolbar: **Map => Map Layers**

![](diagrams/chapter1/section5/tableau-10-fuse-12-215x800.png)

Try different options, what do they mean?

You can even add a colored data layer! You may want to remove your previous color first.

Where does the data come from?

<br><br>

Remember the “generated”? Investigate what can/cannot be generated?

<br><br>

Now its time to move on and see how to do this in R.

<br><br>

***


