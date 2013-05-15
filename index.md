---
title       : Introduction to googleVis
subtitle    : Lancaster University, 21 May 2013
author      : Markus Gesmann
job         : Maintainer of the googleVis and ChainLadder packages
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
license     : by-nc-sa
github      :
  user      : mages
  repo      : Introduction_to_googleVis
---

## Disclaimer

1. I am an autodidact 
2. What I present here works for me
3. Read and follow the official [Google Chart API documentation](https://developers.google.com/chart/) and [Terms of Service](https://developers.google.com/readme/terms)
4. Sometimes you have re-load this presentation for the charts and all slides to appear

---

## Agenda

* Introduction and motivation
* Google Chart Tools
* R package googleVis
  * Concepts of googleVis
  * Case studies




--- .class #id 

## Hans Rosling: No more boring data

<iframe width="420" height="315" src="http://www.youtube.com/embed/hVimVzgtD6w" frameborder="0" allowfullscreen></iframe>

---

## Motivation for googleVis

* Inspired by Hans Rosling’s talks we wanted to use interactive data visualisation tools to foster the dialogue between data analysts and others

* We wanted moving bubbles charts as well

* The software behind Hans’ talk was bought by Google and integrated as motion charts into their Visualisation API

* Ideally we wanted to use R, a language we knew

* Hence, we had to create an interface between the Google Chart Tools and R

--- 

## Overview of googleVis

* [googleVis](http://code.google.com/p/google-motion-charts-with-r/) is a package for [R](http://www.r-poject.org/) and provides an interface between R and the [Google Chart Tools](https://developers.google.com/chart/)

* The functions of the package allow users to visualise data with the Google Chart Tools without uploading their data to Google

* The output of googleVis functions is html code that contains the data and references to JavaScript functions hosted by Google

* To view the output a browser with an internet connection is required, the actual chart is rendered in the browser; some charts require Flash

* See also: **Using the Google Visualisation API with R**, 
  [The R Journal, 3(2):40-44, December 2011](http://journal.r-project.org/archive/2011-2/RJournal_2011-2_Gesmann+de~Castillo.pdf) and googleVis [package vignette](http://cran.r-project.org/web/packages/googleVis/vignettes/googleVis.pdf)

---

## Introduction to Google Chart Tools

* Google Chart Tools provide a way to visualize data on web sites

* The API makes it easy to create interactive charts

* It uses JavaScript and DataTable / JSON as input

* Output is either HTML5/SVG or Flash

* Browser with internet connection required to display chart

* Please read the Google [Terms of Service](https://developers.google.com/terms/) before you start

---

## Structure of Google Charts

The chart code has five generic parts:

1. References to Google’s AJAX and Visualisation API
2. Data to visualise as a DataTable
3. Instance call to create the chart
4. Method call to draw the chart including options
5. HTML &lt;div&gt; element to add the chart to the page

---

## How hard can it be?

* Transform data into JSON object 
* Wrap some HTML and JavaScript around it 
* Thus, googleVis started life in August 2010


----

## Motion chart example


```r
library(googleVis)
plot(gvisMotionChart(Fruits, "Fruit", "Year", options = list(width = 600, height = 400)))
```

<!-- MotionChart generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:02 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataMotionChartID26a273ec108d () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 "Apples",
2008,
"West",
98,
78,
20,
"2008-12-31" 
],
[
 "Apples",
2009,
"West",
111,
79,
32,
"2009-12-31" 
],
[
 "Apples",
2010,
"West",
89,
76,
13,
"2010-12-31" 
],
[
 "Oranges",
2008,
"East",
96,
81,
15,
"2008-12-31" 
],
[
 "Bananas",
2008,
"East",
85,
76,
9,
"2008-12-31" 
],
[
 "Oranges",
2009,
"East",
93,
80,
13,
"2009-12-31" 
],
[
 "Bananas",
2009,
"East",
94,
78,
16,
"2009-12-31" 
],
[
 "Oranges",
2010,
"East",
98,
91,
7,
"2010-12-31" 
],
[
 "Bananas",
2010,
"East",
81,
71,
10,
"2010-12-31" 
] 
];
data.addColumn('string','Fruit');
data.addColumn('number','Year');
data.addColumn('string','Location');
data.addColumn('number','Sales');
data.addColumn('number','Expenses');
data.addColumn('number','Profit');
data.addColumn('string','Date');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartMotionChartID26a273ec108d() {
  var data = gvisDataMotionChartID26a273ec108d();
  var options = {};
options["width"] =    600;
options["height"] =    400;

     var chart = new google.visualization.MotionChart(
       document.getElementById('MotionChartID26a273ec108d')
     );
     chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "motionchart";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartMotionChartID26a273ec108d);
})();
function displayChartMotionChartID26a273ec108d() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartMotionChartID26a273ec108d"></script>
 
<!-- divChart -->
  
<div id="MotionChartID26a273ec108d"
  style="width: 600px; height: 400px;">
</div>


---


## googleVis version 0.4.2 provides interfaces to 

* Flash based
  * Motion Charts
  * Annotated Time Lines
  * Geo Maps
* HMTL5/SVG based
  * Maps, Geo Charts and Intensity Maps
  * Tables, Gauges, Tree Maps
  * Line-, Bar-, Column-, Area- and Combo Charts
  * Scatter-, Bubble-, Candlestick-, Pie- and Org Charts

Run ```demo(googleVis)``` to see [examples](http://code.google.com/p/google-motion-charts-with-r/wiki/GadgetExamples) of all charts and read the [vignette](http://cran.r-project.org/web/packages/googleVis/vignettes/googleVis.pdf) for more details.

----

## Key ideas of googleVis

* Create wrapper functions in R which generate html files with references to Google's Chart Tools API
* Transform R data frames into [JSON](http://www.json.org/) objects with [RJSONIO](http://www.omegahat.org/RJSONIO/)


```r
library(RJSONIO)
dat <- data.frame(x = LETTERS[1:2], y = 1:2)
cat(toJSON(dat))
```

```
## {
##  "x": [ "A", "B" ],
## "y": [ 1, 2 ] 
## }
```

* Display the HTML output with the R HTTP help server

---

## The googleVis concept

* Charts: *'gvis' + ChartType*
* For a motion chart we have


```r
M <- gvisMotionChart(data, idvar='id', timevar='date', 
                     options=list(), chartid)
```


* Output of googleVis is a list of list

* Display the chart by simply plotting the output: ```plot(M)```
* Plot will generate a temporary html-file and open it in a new browser window 
* Specific parts can be extracted, e.g. 
  * the chart: ```M$html$chart``` or 
  * data: ```M$html$chart["jsData"]```

---

## gvis-Chart structure

List structure:

<img height=350 src="https://dl.dropbox.com/u/7586336/googleVisExamples/gvisObject.png" alt="gvis object structure" />

---


## Line chart with options set


```r
df <- data.frame(label=c("US", "GB", "BR"), val1=c(1,3,4), val2=c(23,12,32))
Line <- gvisLineChart(df, xvar="label", yvar=c("val1","val2"),
        options=list(title="Hello World", legend="bottom",
                titleTextStyle="{color:'red', fontSize:18}",                         
                vAxis="{gridlines:{color:'red', count:3}}",
                hAxis="{title:'My Label', titleTextStyle:{color:'blue'}}",
                series="[{color:'green', targetAxisIndex: 0}, 
                         {color: 'blue',targetAxisIndex:1}]",
                vAxes="[{title:'Value 1 (%)', format:'##,######%'}, 
                                  {title:'Value 2 (\U00A3)'}]",                          
                curveType="function", width=500, height=300                         
                ))
```

Options in googleVis have to follow the Google Chart API options

---

## Line chart with options

```r
plot(Line)
```

<!-- LineChart generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:03 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataLineChartID26a2f32d470 () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 "US",
1,
23 
],
[
 "GB",
3,
12 
],
[
 "BR",
4,
32 
] 
];
data.addColumn('string','label');
data.addColumn('number','val1');
data.addColumn('number','val2');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartLineChartID26a2f32d470() {
  var data = gvisDataLineChartID26a2f32d470();
  var options = {};
options["allowHtml"] = true;
options["title"] = "Hello World";
options["legend"] = "bottom";
options["titleTextStyle"] = {color:'red', fontSize:18};
options["vAxis"] = {gridlines:{color:'red', count:3}};
options["hAxis"] = {title:'My Label', titleTextStyle:{color:'blue'}};
options["series"] = [{color:'green', targetAxisIndex: 0}, 
                         {color: 'blue',targetAxisIndex:1}];
options["vAxes"] = [{title:'Value 1 (%)', format:'##,######%'}, 
                                  {title:'Value 2 (£)'}];
options["curveType"] = "function";
options["width"] =    500;
options["height"] =    300;

     var chart = new google.visualization.LineChart(
       document.getElementById('LineChartID26a2f32d470')
     );
     chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "corechart";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartLineChartID26a2f32d470);
})();
function displayChartLineChartID26a2f32d470() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartLineChartID26a2f32d470"></script>
 
<!-- divChart -->
  
<div id="LineChartID26a2f32d470"
  style="width: 500px; height: 300px;">
</div>


---

## On-line changes

You can enable the chart editor which allows users to change the chart.

```r
plot(gvisLineChart(df, options = list(gvis.editor = "Edit me!", height = 350)))
```

<!-- LineChart generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:03 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataLineChartID26a252190cdb () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 "US",
1,
23 
],
[
 "GB",
3,
12 
],
[
 "BR",
4,
32 
] 
];
data.addColumn('string','label');
data.addColumn('number','val1');
data.addColumn('number','val2');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartLineChartID26a252190cdb() {
  var data = gvisDataLineChartID26a252190cdb();
  var options = {};
options["allowHtml"] = true;
options["height"] =    350;

    chartLineChartID26a252190cdb = new google.visualization.ChartWrapper({
         dataTable: data,       
         chartType: 'LineChart',
         containerId: 'LineChartID26a252190cdb',
         options: options
    });
    chartLineChartID26a252190cdb.draw();
    

}

  function openEditorLineChartID26a252190cdb() {
      var editor = new google.visualization.ChartEditor();
      google.visualization.events.addListener(editor, 'ok',
        function() { 
          chartLineChartID26a252190cdb = editor.getChartWrapper();  
          chartLineChartID26a252190cdb.draw(document.getElementById('LineChartID26a252190cdb')); 
      }); 
      editor.openDialog(chartLineChartID26a252190cdb);
  }
    
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "charteditor";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartLineChartID26a252190cdb);
})();
function displayChartLineChartID26a252190cdb() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartLineChartID26a252190cdb"></script>
 
<!-- divChart -->
<input type='button' onclick='openEditorLineChartID26a252190cdb()' value='Edit me!'/>  
<div id="LineChartID26a252190cdb"
  style="width: 600px; height: 350px;">
</div>


---

## Change motion chart settings


```r
plot(gvisMotionChart(Fruits, "Fruit", "Year", options = list(width = 500, height = 350)))
```

<!-- MotionChart generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:03 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataMotionChartID26a26a9b27f8 () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 "Apples",
2008,
"West",
98,
78,
20,
"2008-12-31" 
],
[
 "Apples",
2009,
"West",
111,
79,
32,
"2009-12-31" 
],
[
 "Apples",
2010,
"West",
89,
76,
13,
"2010-12-31" 
],
[
 "Oranges",
2008,
"East",
96,
81,
15,
"2008-12-31" 
],
[
 "Bananas",
2008,
"East",
85,
76,
9,
"2008-12-31" 
],
[
 "Oranges",
2009,
"East",
93,
80,
13,
"2009-12-31" 
],
[
 "Bananas",
2009,
"East",
94,
78,
16,
"2009-12-31" 
],
[
 "Oranges",
2010,
"East",
98,
91,
7,
"2010-12-31" 
],
[
 "Bananas",
2010,
"East",
81,
71,
10,
"2010-12-31" 
] 
];
data.addColumn('string','Fruit');
data.addColumn('number','Year');
data.addColumn('string','Location');
data.addColumn('number','Sales');
data.addColumn('number','Expenses');
data.addColumn('number','Profit');
data.addColumn('string','Date');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartMotionChartID26a26a9b27f8() {
  var data = gvisDataMotionChartID26a26a9b27f8();
  var options = {};
options["width"] =    500;
options["height"] =    350;

     var chart = new google.visualization.MotionChart(
       document.getElementById('MotionChartID26a26a9b27f8')
     );
     chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "motionchart";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartMotionChartID26a26a9b27f8);
})();
function displayChartMotionChartID26a26a9b27f8() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartMotionChartID26a26a9b27f8"></script>
 
<!-- divChart -->
  
<div id="MotionChartID26a26a9b27f8"
  style="width: 500px; height: 350px;">
</div>

Change displaying settings via the browser, then copy the state string from the 'Advanced' tab and set to `state` argument in `options`.
Ensure you have newlines at the beginning and end of the string. 

---

## Motion chart with initial settings changed


```r
myStateSettings <- '\n{"iconType":"LINE", "dimensions":{
    "iconDimensions":["dim0"]},"xAxisOption":"_TIME",
    "orderedByX":false,"orderedByY":false,"yZoomedDataMax":100}\n'
plot(gvisMotionChart(Fruits, "Fruit", "Year", 
      options=list(state=myStateSettings, height=320)))
```

<!-- MotionChart generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:03 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataMotionChartID26a2705d4175 () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 "Apples",
2008,
"West",
98,
78,
20,
"2008-12-31" 
],
[
 "Apples",
2009,
"West",
111,
79,
32,
"2009-12-31" 
],
[
 "Apples",
2010,
"West",
89,
76,
13,
"2010-12-31" 
],
[
 "Oranges",
2008,
"East",
96,
81,
15,
"2008-12-31" 
],
[
 "Bananas",
2008,
"East",
85,
76,
9,
"2008-12-31" 
],
[
 "Oranges",
2009,
"East",
93,
80,
13,
"2009-12-31" 
],
[
 "Bananas",
2009,
"East",
94,
78,
16,
"2009-12-31" 
],
[
 "Oranges",
2010,
"East",
98,
91,
7,
"2010-12-31" 
],
[
 "Bananas",
2010,
"East",
81,
71,
10,
"2010-12-31" 
] 
];
data.addColumn('string','Fruit');
data.addColumn('number','Year');
data.addColumn('string','Location');
data.addColumn('number','Sales');
data.addColumn('number','Expenses');
data.addColumn('number','Profit');
data.addColumn('string','Date');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartMotionChartID26a2705d4175() {
  var data = gvisDataMotionChartID26a2705d4175();
  var options = {};
options["width"] =    600;
options["height"] =    320;
options["state"] = "\n{\"iconType\":\"LINE\", \"dimensions\":{\n    \"iconDimensions\":[\"dim0\"]},\"xAxisOption\":\"_TIME\",\n    \"orderedByX\":false,\"orderedByY\":false,\"yZoomedDataMax\":100}\n";

     var chart = new google.visualization.MotionChart(
       document.getElementById('MotionChartID26a2705d4175')
     );
     chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "motionchart";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartMotionChartID26a2705d4175);
})();
function displayChartMotionChartID26a2705d4175() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartMotionChartID26a2705d4175"></script>
 
<!-- divChart -->
  
<div id="MotionChartID26a2705d4175"
  style="width: 600px; height: 320px;">
</div>


---

## Displaying geographical information

Plot countries' S&P credit rating sourced from Wikipedia

```r
library(XML)
url <- "http://en.wikipedia.org/wiki/List_of_countries_by_credit_rating"
x <- readHTMLTable(readLines(url), which=3)
levels(x$Rating) <- substring(levels(x$Rating), 4, 
                            nchar(levels(x$Rating)))
x$Ranking <- x$Rating
levels(x$Ranking) <- nlevels(x$Rating):1
x$Ranking <- as.character(x$Ranking)
x$Rating <- paste(x$Country, x$Rating, sep=": ")
G <- gvisGeoChart(x, "Country", "Ranking", hovervar="Rating",
                options=list(gvis.editor="S&P", 
                             colorAxis="{colors:['#91BFDB', '#FC8D59']}"))
```


---

## Chart countries' S&P credit rating

```r
plot(G)
```

<!-- GeoChart generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:04 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataGeoChartID26a27a74a1f4 () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 "Abu Dhabi, UAE",
"Abu Dhabi, UAE: AA",
3 
],
[
 "Albania",
"Albania: B+",
14 
],
[
 "Andorra",
"Andorra: A-",
7 
],
[
 "Angola",
"Angola: BB-",
12 
],
[
 "Argentina",
"Argentina: B-",
16 
],
[
 "Aruba",
"Aruba: A-",
7 
],
[
 "Australia",
"Australia: AAA",
1 
],
[
 "Austria",
"Austria: AA+",
2 
],
[
 "Azerbaijan",
"Azerbaijan: BBB-",
10 
],
[
 "Bahamas",
"Bahamas: BBB",
9 
],
[
 "Bahrain",
"Bahrain: BBB",
9 
],
[
 "Bangladesh",
"Bangladesh: BB-",
12 
],
[
 "Barbados",
"Barbados: BB+",
11 
],
[
 "Belarus",
"Belarus: B-",
16 
],
[
 "Belgium",
"Belgium: AA",
3 
],
[
 "Belize",
"Belize: B-",
16 
],
[
 "Benin",
"Benin: B",
15 
],
[
 "Bermuda",
"Bermuda: AA-",
4 
],
[
 "Bolivia",
"Bolivia: BB-",
12 
],
[
 "Bosnia and Herzegovina",
"Bosnia and Herzegovina: B",
15 
],
[
 "Botswana",
"Botswana: A-",
7 
],
[
 "Brazil",
"Brazil: BBB",
9 
],
[
 "Bulgaria",
"Bulgaria: BBB",
9 
],
[
 "Burkina Faso",
"Burkina Faso: B",
15 
],
[
 "Cambodia",
"Cambodia: B",
15 
],
[
 "Cameroon",
"Cameroon: B",
15 
],
[
 "Canada",
"Canada: AAA",
1 
],
[
 "Cape Verde",
"Cape Verde: B+",
14 
],
[
 "Chile",
"Chile: AA-",
4 
],
[
 "China",
"China: AA-",
4 
],
[
 "Colombia",
"Colombia: BBB",
9 
],
[
 "Cook Islands",
"Cook Islands: B+",
14 
],
[
 "Costa Rica",
"Costa Rica: BB",
13 
],
[
 "Croatia",
"Croatia: BB+",
11 
],
[
 "Curacao",
"Curacao: A-",
7 
],
[
 "Cyprus",
"Cyprus: CCC",
18 
],
[
 "Czech Republic",
"Czech Republic: AA-",
4 
],
[
 "Denmark",
"Denmark: AAA",
1 
],
[
 "Dominican Republic",
"Dominican Republic: B+",
14 
],
[
 "Ecuador",
"Ecuador: B",
15 
],
[
 "Egypt",
"Egypt: CCC+",
17 
],
[
 "El Salvador",
"El Salvador: BB-",
12 
],
[
 "Estonia",
"Estonia: AA-",
4 
],
[
 "Fiji",
"Fiji: B",
15 
],
[
 "Finland",
"Finland: AAA",
1 
],
[
 "France",
"France: AA+",
2 
],
[
 "Gabon",
"Gabon: BB-",
12 
],
[
 "Georgia",
"Georgia: BB-",
12 
],
[
 "Germany",
"Germany: AAA",
1 
],
[
 "Ghana",
"Ghana: B",
15 
],
[
 "Greece",
"Greece: B-",
16 
],
[
 "Grenada",
"Grenada: SD",
19 
],
[
 "Guatemala",
"Guatemala: BB",
13 
],
[
 "Guernsey",
"Guernsey: AA+",
2 
],
[
 "Honduras",
"Honduras: B+",
14 
],
[
 "Hong Kong",
"Hong Kong: AAA",
1 
],
[
 "Hungary",
"Hungary: BB",
13 
],
[
 "Iceland",
"Iceland: BBB-",
10 
],
[
 "India",
"India: BBB-",
10 
],
[
 "Indonesia",
"Indonesia: BB+",
11 
],
[
 "Ireland",
"Ireland: BBB+",
8 
],
[
 "Isle of Man",
"Isle of Man: AA+",
2 
],
[
 "Israel",
"Israel: A+",
5 
],
[
 "Italy",
"Italy: BBB+",
8 
],
[
 "Jamaica",
"Jamaica: CCC+",
17 
],
[
 "Japan",
"Japan: AA-",
4 
],
[
 "Jordan",
"Jordan: BB",
13 
],
[
 "Kazakhstan",
"Kazakhstan: BBB+",
8 
],
[
 "Kenya",
"Kenya: B+",
14 
],
[
 "Kuwait",
"Kuwait: AA",
3 
],
[
 "Latvia",
"Latvia: BBB",
9 
],
[
 "Lebanon",
"Lebanon: B",
15 
],
[
 "Liechtenstein",
"Liechtenstein: AAA",
1 
],
[
 "Lithuania",
"Lithuania: BBB",
9 
],
[
 "Luxembourg",
"Luxembourg: AAA",
1 
],
[
 "Template:Country data FYROM",
"Template:Country data FYROM: BB",
13 
],
[
 "Malaysia",
"Malaysia: A-",
7 
],
[
 "Malta",
"Malta: BBB+",
8 
],
[
 "Mexico",
"Mexico: BBB",
9 
],
[
 "Mongolia",
"Mongolia: BB-",
12 
],
[
 "Montenegro",
"Montenegro: BB-",
12 
],
[
 "Montserrat",
"Montserrat: BBB-",
10 
],
[
 "Morocco",
"Morocco: BBB-",
10 
],
[
 "Mozambique",
"Mozambique: B+",
14 
],
[
 "Netherlands",
"Netherlands: AAA",
1 
],
[
 "New Zealand",
"New Zealand: AA",
3 
],
[
 "Nigeria",
"Nigeria: BB-",
12 
],
[
 "Norway",
"Norway: AAA",
1 
],
[
 "Oman",
"Oman: A",
6 
],
[
 "Pakistan",
"Pakistan: B-",
16 
],
[
 "Panama",
"Panama: BBB",
9 
],
[
 "Papua New Guinea",
"Papua New Guinea: B+",
14 
],
[
 "Paraguay",
"Paraguay: BB-",
12 
],
[
 "Peru",
"Peru: BBB",
9 
],
[
 "Philippines",
"Philippines: BBB-",
10 
],
[
 "Poland",
"Poland: A-",
7 
],
[
 "Portugal",
"Portugal: BB",
13 
],
[
 "Qatar",
"Qatar: AA",
3 
],
[
 "Ras Al Khaimah, UAE",
"Ras Al Khaimah, UAE: A",
6 
],
[
 "Romania",
"Romania: BB+",
11 
],
[
 "Russia",
"Russia: BBB",
9 
],
[
 "Rwanda",
"Rwanda: B",
15 
],
[
 "Saudi Arabia",
"Saudi Arabia: AA-",
4 
],
[
 "Senegal",
"Senegal: B+",
14 
],
[
 "Serbia",
"Serbia: BB-",
12 
],
[
 "Singapore",
"Singapore: AAA",
1 
],
[
 "Slovakia",
"Slovakia: A",
6 
],
[
 "Slovenia",
"Slovenia: A-",
7 
],
[
 "South Africa",
"South Africa: BBB",
9 
],
[
 "South Korea",
"South Korea: A+",
5 
],
[
 "Spain",
"Spain: BBB-",
10 
],
[
 "Sri Lanka",
"Sri Lanka: B+",
14 
],
[
 "Suriname",
"Suriname: BB-",
12 
],
[
 "Sweden",
"Sweden: AAA",
1 
],
[
 "Switzerland",
"Switzerland: AAA",
1 
],
[
 "Taiwan",
"Taiwan: AA-",
4 
],
[
 "Thailand",
"Thailand: BBB+",
8 
],
[
 "Trinidad and Tobago",
"Trinidad and Tobago: A",
6 
],
[
 "Tunisia",
"Tunisia: BB-",
12 
],
[
 "Turkey",
"Turkey: BB+",
11 
],
[
 "Uganda",
"Uganda: B+",
14 
],
[
 "Ukraine",
"Ukraine: BB",
13 
],
[
 "United Kingdom",
"United Kingdom: AA",
3 
],
[
 "United States",
"United States: AA+",
2 
],
[
 "Uruguay",
"Uruguay: BBB-",
10 
],
[
 "Venezuela",
"Venezuela: B+",
14 
],
[
 "Vietnam",
"Vietnam: BB-",
12 
],
[
 "Zambia",
"Zambia: B+",
14 
] 
];
data.addColumn('string','Country');
data.addColumn('string','Rating');
data.addColumn('number','Ranking');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartGeoChartID26a27a74a1f4() {
  var data = gvisDataGeoChartID26a27a74a1f4();
  var options = {};
options["width"] =    556;
options["height"] =    347;
options["colorAxis"] = {colors:['#91BFDB', '#FC8D59']};

    chartGeoChartID26a27a74a1f4 = new google.visualization.ChartWrapper({
         dataTable: data,       
         chartType: 'GeoChart',
         containerId: 'GeoChartID26a27a74a1f4',
         options: options
    });
    chartGeoChartID26a27a74a1f4.draw();
    

}

  function openEditorGeoChartID26a27a74a1f4() {
      var editor = new google.visualization.ChartEditor();
      google.visualization.events.addListener(editor, 'ok',
        function() { 
          chartGeoChartID26a27a74a1f4 = editor.getChartWrapper();  
          chartGeoChartID26a27a74a1f4.draw(document.getElementById('GeoChartID26a27a74a1f4')); 
      }); 
      editor.openDialog(chartGeoChartID26a27a74a1f4);
  }
    
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "charteditor";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartGeoChartID26a27a74a1f4);
})();
function displayChartGeoChartID26a27a74a1f4() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartGeoChartID26a27a74a1f4"></script>
 
<!-- divChart -->
<input type='button' onclick='openEditorGeoChartID26a27a74a1f4()' value='S&P'/>  
<div id="GeoChartID26a27a74a1f4"
  style="width: 556px; height: 347px;">
</div>


---

## Geo chart with markers
Display earth quake information of last 30 days

```r
library(XML)
eq <- read.csv("http://earthquake.usgs.gov/earthquakes/feed/v0.1/summary/2.5_week.csv")
eq$loc=paste(eq$Latitude, eq$Longitude, sep=":")

G <- gvisGeoChart(eq, "loc", "Depth", "Magnitude",
                   options=list(displayMode="Markers", 
                   colorAxis="{colors:['purple', 'red', 'orange', 'grey']}",
                   backgroundColor="lightblue"), chartid="EQ")
```


---

## Geo chart of earth quakes

```r
plot(G)
```

<!-- GeoChart generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:04 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataEQ () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 33.66,
-118.375,
1.5,
4 
],
[
 51.164,
179.479,
35.3,
4.3 
],
[
 30.397,
103.1,
10.5,
4.4 
],
[
 -18.527,
-71.402,
59.3,
4.3 
],
[
 33.98,
-116.767,
17.9,
3.1 
],
[
 26.835,
57.757,
10,
4.5 
],
[
 58.588,
-152.512,
8.2,
3 
],
[
 -10.88,
113.842,
10,
4.6 
],
[
 46.148,
151.117,
119.8,
5.3 
],
[
 60.581,
-151.157,
26.5,
2.6 
],
[
 51.59,
-176.113,
35.7,
2.7 
],
[
 13.042,
-88.771,
84.2,
4.4 
],
[
 60.322,
-152.429,
100.5,
2.9 
],
[
 32.586,
105.195,
16.5,
4.7 
],
[
 18.221,
-68.557,
101,
2.9 
],
[
 -4.546,
153.212,
67.8,
5 
],
[
 31.468,
86.569,
26,
5.1 
],
[
 35.549,
-97.16,
4.3,
2.6 
],
[
 1.059,
97.44,
41.7,
4.8 
],
[
 1.063,
97.397,
34.2,
4.6 
],
[
 36.814,
140.59,
8.3,
4.6 
],
[
 -27.192,
-178.004,
147,
4.9 
],
[
 51.444,
-176.056,
22.4,
2.5 
],
[
 59.81,
-153.605,
121.7,
2.9 
],
[
 65.571,
-134.944,
8.9,
4.3 
],
[
 62.866,
-148.828,
63.7,
3.2 
],
[
 18.294,
-67.554,
9,
2.8 
],
[
 38.819,
-122.804,
4,
3 
],
[
 38.91,
88.174,
14.7,
4.6 
],
[
 60.039,
-152.666,
121.3,
3.3 
],
[
 17.865,
-67.065,
10,
2.5 
],
[
 -4.58,
152.824,
69.1,
5.7 
],
[
 -5.488,
151.686,
41.9,
4.9 
],
[
 39.916,
72.333,
25,
4.3 
],
[
 18.73,
-64.761,
25,
2.8 
],
[
 -15.613,
-73.132,
112,
5.7 
],
[
 -0.556,
130.303,
25.3,
4.6 
],
[
 -18.624,
-173.45,
7.1,
4.9 
],
[
 33.154,
75.837,
10.9,
4.7 
],
[
 18.27,
-67.062,
24,
2.5 
],
[
 33.156,
75.78,
50.6,
4.2 
],
[
 0.775,
92.437,
32.5,
5.7 
],
[
 18.783,
-64.65,
49,
2.7 
],
[
 36.284,
69.759,
140.4,
4 
],
[
 18.973,
-64.101,
58,
3.1 
],
[
 -1.142,
-77.477,
171,
4.3 
],
[
 62.119,
-150.254,
8.5,
3.4 
],
[
 51.947,
-171.805,
11.2,
2.7 
],
[
 -8.236,
122.099,
204.1,
4.6 
],
[
 56.2,
162.696,
10,
5 
],
[
 58.647,
-152.71,
92.9,
3.4 
],
[
 -27.867,
-66.635,
188.8,
4.5 
],
[
 45.612,
-111.737,
9.5,
2.7 
],
[
 -6.54,
129.879,
148.3,
4.7 
],
[
 58.675,
-153.671,
null,
2.6 
],
[
 37.095,
-112.117,
15.3,
2.5 
],
[
 50.891,
178.862,
35,
4.5 
],
[
 36.682,
-117.746,
12,
2.6 
],
[
 32.209,
-115.259,
17.8,
2.6 
],
[
 35.62,
-90.55,
9.9,
2.8 
],
[
 17.901,
-67.309,
8,
2.7 
],
[
 58.738,
-153.863,
11.5,
2.9 
],
[
 58.795,
-153.948,
4,
4.3 
],
[
 52.778,
-168.949,
23.8,
3.6 
],
[
 18.748,
145.294,
601.8,
6.8 
],
[
 -18.096,
-175.136,
201.9,
4.9 
],
[
 31.128,
-104.746,
4.3,
2.7 
],
[
 -3.037,
130.264,
37.8,
4.2 
],
[
 2.782,
125.31,
155.5,
4.9 
],
[
 28.395,
51.791,
10.5,
4.8 
],
[
 19.283,
-155.568,
5.5,
2.7 
],
[
 62.259,
-151.398,
77.3,
3.2 
],
[
 41.047,
-123.333,
34.9,
2.5 
],
[
 48.586,
154.872,
54.1,
4.5 
],
[
 -6.509,
129.702,
158.6,
4.7 
],
[
 34.01,
-37.547,
10,
4.9 
],
[
 36.778,
140.5,
29,
4.6 
],
[
 -7.949,
-79.913,
55.6,
4.9 
],
[
 59.551,
-152.888,
102.6,
2.8 
],
[
 -3.003,
130.185,
36.7,
4.4 
],
[
 63.233,
-150.397,
100.8,
2.5 
],
[
 62.305,
-151.1,
67.3,
2.7 
],
[
 19.406,
-64.154,
104,
3.4 
],
[
 60.812,
-151.758,
71,
3.1 
],
[
 -19.872,
-177.779,
548.8,
4.6 
],
[
 10.308,
-85.816,
40.5,
4.4 
],
[
 0.76,
125.368,
85.7,
4.8 
],
[
 10.246,
-85.893,
39.4,
4.3 
],
[
 21.914,
143.807,
175.6,
5.1 
],
[
 44.026,
147.811,
53.4,
5.6 
],
[
 29.531,
52.699,
13.9,
4.4 
],
[
 60.602,
-149.439,
0.1,
2.8 
],
[
 52.508,
-171.941,
45,
5.7 
],
[
 19.343,
-155.036,
6.1,
2.5 
],
[
 -7.635,
128.012,
171,
4.4 
],
[
 -6.509,
128.066,
317.7,
4.6 
],
[
 1.176,
-101.293,
10,
4.7 
],
[
 63.334,
-150.038,
105.1,
2.6 
],
[
 62.911,
-150.837,
94.8,
2.8 
],
[
 18.569,
-68.453,
125,
3.6 
],
[
 -3.109,
-77.589,
23.5,
4.6 
],
[
 -26.177,
-69.223,
7.8,
5.6 
],
[
 -21.01,
-68.545,
130.7,
5.3 
],
[
 26.734,
57.813,
25.2,
4.4 
],
[
 -22.083,
170.256,
17.9,
4.8 
],
[
 27.402,
57.369,
10,
4.1 
],
[
 18.262,
-67.17,
109,
3 
],
[
 26.791,
57.742,
25.9,
5.4 
],
[
 39.554,
73.033,
41.3,
4.8 
],
[
 -6.459,
154.228,
48.1,
4.8 
],
[
 26.637,
57.7,
26,
4.5 
],
[
 46.637,
152.647,
68.9,
4.8 
],
[
 -6.401,
154.27,
45,
4.8 
],
[
 13.563,
-91.285,
33.4,
5.8 
],
[
 19.184,
-64.808,
66,
3.1 
],
[
 58.794,
-153.92,
15.2,
4.5 
],
[
 26.525,
57.961,
24.1,
4.2 
],
[
 18.773,
-67.449,
8,
2.8 
],
[
 59.831,
-153.645,
192,
2.9 
],
[
 26.92,
57.677,
20,
4.4 
],
[
 69.83,
-146.391,
49.6,
4.3 
],
[
 19.469,
-67.796,
51,
3 
],
[
 19.381,
-155.243,
3.5,
2.8 
],
[
 39.992,
-120.795,
11.9,
2.5 
],
[
 26.744,
57.749,
19.3,
4.2 
],
[
 13.676,
-91.303,
64.6,
4.3 
],
[
 26.472,
57.749,
20.1,
4.5 
],
[
 26.851,
57.856,
10,
4.5 
],
[
 26.766,
57.769,
25,
5.6 
],
[
 26.691,
57.52,
9.6,
4.6 
],
[
 26.717,
57.762,
10,
4.9 
],
[
 26.754,
57.677,
10.1,
4.9 
],
[
 -17.944,
-175.075,
205.4,
6.5 
],
[
 54.453,
-161.487,
9.9,
2.9 
],
[
 -15.763,
-71.534,
157.8,
4.3 
],
[
 24.749,
123.251,
28.7,
4.5 
],
[
 50.998,
-177.742,
17.5,
2.9 
],
[
 18.311,
-64.875,
80,
2.9 
],
[
 26.651,
57.903,
23.5,
4.7 
],
[
 -26.159,
-69.345,
15.4,
5.4 
],
[
 51.949,
-170.869,
25.6,
2.9 
],
[
 -3.756,
129.726,
40.5,
4.5 
],
[
 36.178,
70.855,
103.3,
4.4 
],
[
 37.694,
143.949,
10,
4.5 
],
[
 26.73,
57.66,
27,
4.3 
],
[
 26.665,
57.769,
24.7,
4.6 
],
[
 17.913,
-65.953,
12,
2.5 
],
[
 26.749,
57.779,
22.2,
5 
],
[
 11.604,
-87.371,
35,
4.2 
],
[
 40.331,
-124.591,
20.2,
3.7 
],
[
 26.809,
58.058,
10,
4.3 
],
[
 26.555,
57.696,
24.7,
4.3 
],
[
 26.619,
57.712,
25,
4.4 
],
[
 30.108,
51.636,
11,
4 
],
[
 32.822,
12.442,
14.8,
4.7 
],
[
 -18.537,
-173.665,
42.7,
4.7 
],
[
 26.822,
57.794,
25,
4.7 
],
[
 19.483,
-67.807,
50,
3.2 
],
[
 26.919,
57.53,
30,
4.4 
],
[
 44.341,
148.261,
108.4,
4.6 
],
[
 26.788,
57.944,
30.2,
5 
],
[
 26.577,
57.581,
25.6,
4.7 
],
[
 26.685,
57.941,
27.3,
5.3 
],
[
 26.773,
57.766,
23.8,
4.8 
],
[
 26.64,
57.861,
25.8,
4.6 
],
[
 26.812,
57.8,
26.5,
4.5 
],
[
 26.754,
57.95,
35,
4.6 
],
[
 -15.895,
-72.424,
92.7,
4.7 
],
[
 26.784,
57.88,
14,
6 
],
[
 61.25,
-147.05,
2.2,
2.7 
],
[
 30.242,
102.967,
12,
4.4 
],
[
 51.948,
-171.011,
35.8,
4.2 
],
[
 30.312,
102.947,
17.7,
4.6 
],
[
 33.531,
-116.447,
9.9,
2.5 
],
[
 -6.478,
154.41,
56.6,
5 
],
[
 21.908,
94.716,
109.5,
4.3 
],
[
 51.811,
-170.76,
28.1,
3.1 
],
[
 14.099,
-91.362,
89.4,
5.1 
],
[
 51.111,
-179.403,
6.8,
3 
],
[
 -28.959,
-13.232,
7.7,
5.7 
],
[
 -7.548,
127.81,
158.1,
4.4 
],
[
 55.809,
165.403,
34,
4.6 
],
[
 18.95,
-64.379,
30,
2.8 
],
[
 51.796,
-176.007,
13.6,
3.1 
],
[
 -6.175,
103.67,
26.5,
4.8 
],
[
 43.917,
-105.707,
9.4,
3.1 
],
[
 52.045,
177.495,
12.3,
2.9 
],
[
 52.391,
177.665,
7.1,
3.1 
],
[
 -17.981,
168.629,
145.7,
4.6 
],
[
 17.915,
-65.948,
12,
2.8 
],
[
 -17.644,
-178.803,
541,
4.3 
],
[
 40.424,
-124.442,
25.8,
2.5 
],
[
 51.518,
177.366,
57.2,
4.8 
],
[
 15.009,
-92.549,
88.5,
4 
],
[
 14.819,
-92.53,
74.7,
4.2 
],
[
 19.128,
-65.356,
11,
3.2 
],
[
 67.535,
139.288,
13.4,
5.4 
],
[
 55.495,
-160.108,
64,
2.8 
],
[
 56.743,
-154.874,
6.3,
2.5 
],
[
 40.343,
-124.612,
22.8,
2.7 
],
[
 -53.107,
25.676,
19.3,
4.7 
],
[
 49.929,
157.295,
34.2,
4.5 
],
[
 37.373,
-121.724,
8.3,
3.5 
],
[
 35.759,
-83.912,
21.8,
2.5 
],
[
 19.171,
-65.32,
36,
3.3 
],
[
 59.543,
-152.77,
96,
2.8 
],
[
 60.19,
-146.39,
2.7,
2.9 
],
[
 -12.142,
-77.049,
93.5,
4 
],
[
 51.701,
179.288,
80.5,
2.5 
],
[
 63.75,
-23.224,
10,
4.2 
],
[
 -0.684,
123.226,
23.2,
4.7 
],
[
 61.623,
-146.535,
14.6,
2.5 
],
[
 55.526,
161.399,
99.3,
4.4 
],
[
 33.96,
-118.416,
12,
2.9 
],
[
 19.391,
-155.278,
3,
2.6 
],
[
 39.141,
16.082,
18.5,
3.4 
],
[
 54.303,
-162.479,
27,
2.6 
],
[
 19.785,
-156.197,
13.8,
2.8 
],
[
 38.356,
-122.18,
9.9,
2.5 
],
[
 16.948,
-97.97,
21.7,
4.5 
],
[
 63.727,
-23.069,
10.2,
4.7 
],
[
 1.584,
126.55,
35.2,
4.4 
],
[
 4.386,
123.904,
470.7,
4.9 
],
[
 63.604,
-23.744,
10,
4.5 
],
[
 27.834,
63.46,
11.5,
4.5 
],
[
 50.946,
157.744,
45.6,
4.3 
],
[
 51.137,
-178.205,
28.3,
2.7 
],
[
 18.935,
-64.159,
41,
2.9 
],
[
 35.541,
-97.25,
6,
2.5 
],
[
 -55.793,
-27.251,
10,
4.9 
],
[
 18.853,
-67.222,
9,
2.7 
],
[
 1.306,
128.17,
110.1,
5 
],
[
 39.973,
-120.795,
3.5,
2.9 
],
[
 -3.781,
135.515,
29.9,
4.7 
],
[
 10.247,
-62.32,
45.5,
4.5 
],
[
 64.065,
-23.081,
9.8,
4.2 
],
[
 -5.373,
153.751,
64.7,
4.6 
],
[
 18.37,
-64.939,
96,
2.5 
],
[
 19.632,
-64.44,
14,
3.3 
],
[
 26.848,
57.823,
25.7,
4.9 
],
[
 1.369,
127.06,
130.5,
4.8 
],
[
 54.159,
-164.156,
25.6,
2.7 
],
[
 14.366,
-92.617,
35.1,
4.1 
],
[
 51.849,
-178.841,
2.8,
2.9 
],
[
 54.402,
-165.279,
172.3,
2.6 
],
[
 21.564,
143.014,
308.7,
4.3 
] 
];
data.addColumn('number','Latitude');
data.addColumn('number','Longitude');
data.addColumn('number','Depth');
data.addColumn('number','Magnitude');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartEQ() {
  var data = gvisDataEQ();
  var options = {};
options["width"] =    556;
options["height"] =    347;
options["displayMode"] = "Markers";
options["colorAxis"] = {colors:['purple', 'red', 'orange', 'grey']};
options["backgroundColor"] = "lightblue";

     var chart = new google.visualization.GeoChart(
       document.getElementById('EQ')
     );
     chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "geochart";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartEQ);
})();
function displayChartEQ() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartEQ"></script>
 
<!-- divChart -->
  
<div id="EQ"
  style="width: 556px; height: 347px;">
</div>


---

## Org chart

```r
Org <- gvisOrgChart(Regions, options=list(width=600, height=250,
                               size='large', allowCollapse=TRUE))
plot(Org)
```

<!-- OrgChart generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:04 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataOrgChartID26a27f34d8fa () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 "Global",
null,
"10" 
],
[
 "America",
"Global",
"2" 
],
[
 "Europe",
"Global",
"99" 
],
[
 "Asia",
"Global",
"10" 
],
[
 "France",
"Europe",
"71" 
],
[
 "Sweden",
"Europe",
"89" 
],
[
 "Germany",
"Europe",
"58" 
],
[
 "Mexico",
"America",
"2" 
],
[
 "USA",
"America",
"38" 
],
[
 "China",
"Asia",
"5" 
],
[
 "Japan",
"Asia",
"48" 
] 
];
data.addColumn('string','Region');
data.addColumn('string','Parent');
data.addColumn('string','Val');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartOrgChartID26a27f34d8fa() {
  var data = gvisDataOrgChartID26a27f34d8fa();
  var options = {};
options["width"] =    600;
options["height"] =    250;
options["size"] = "large";
options["allowCollapse"] = true;

     var chart = new google.visualization.OrgChart(
       document.getElementById('OrgChartID26a27f34d8fa')
     );
     chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "orgchart";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartOrgChartID26a27f34d8fa);
})();
function displayChartOrgChartID26a27f34d8fa() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartOrgChartID26a27f34d8fa"></script>
 
<!-- divChart -->
  
<div id="OrgChartID26a27f34d8fa"
  style="width: 600px; height: 250px;">
</div>


---

## Org chart data

```r
Regions
```

```
##     Region  Parent Val Fac
## 1   Global    <NA>  10   2
## 2  America  Global   2   4
## 3   Europe  Global  99  11
## 4     Asia  Global  10   8
## 5   France  Europe  71   2
## 6   Sweden  Europe  89   3
## 7  Germany  Europe  58  10
## 8   Mexico America   2   9
## 9      USA America  38  11
## 10   China    Asia   5   1
## 11   Japan    Asia  48  11
```

Notice the data structure. Each row in the data table describes one node. Each node (except the root node) has one or more parent nodes. 

---


## Tree map
Same data structure as for org charts required.

```r
Tree <- gvisTreeMap(Regions, idvar = "Region", parentvar = "Parent", sizevar = "Val", 
    colorvar = "Fac", options = list(width = 450, height = 320))
plot(Tree)
```

<!-- TreeMap generated in R 3.0.0 by googleVis 0.4.3 package -->
<!-- Wed May 15 23:04:04 2013 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataTreeMapID26a266914654 () {
  var data = new google.visualization.DataTable();
  var datajson =
[
 [
 "Global",
null,
10,
2 
],
[
 "America",
"Global",
2,
4 
],
[
 "Europe",
"Global",
99,
11 
],
[
 "Asia",
"Global",
10,
8 
],
[
 "France",
"Europe",
71,
2 
],
[
 "Sweden",
"Europe",
89,
3 
],
[
 "Germany",
"Europe",
58,
10 
],
[
 "Mexico",
"America",
2,
9 
],
[
 "USA",
"America",
38,
11 
],
[
 "China",
"Asia",
5,
1 
],
[
 "Japan",
"Asia",
48,
11 
] 
];
data.addColumn('string','Region');
data.addColumn('string','Parent');
data.addColumn('number','Val');
data.addColumn('number','Fac');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartTreeMapID26a266914654() {
  var data = gvisDataTreeMapID26a266914654();
  var options = {};
options["width"] =    450;
options["height"] =    320;

     var chart = new google.visualization.TreeMap(
       document.getElementById('TreeMapID26a266914654')
     );
     chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  var chartid = "treemap";

  // Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
  var i, newPackage = true;
  for (i = 0; newPackage && i < pkgs.length; i++) {
    if (pkgs[i] === chartid)
      newPackage = false;
  }
  if (newPackage)
    pkgs.push(chartid);

  // Add the drawChart function to the global list of callbacks
  callbacks.push(drawChartTreeMapID26a266914654);
})();
function displayChartTreeMapID26a266914654() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
    var pkgCount = pkgs.length;
    google.load("visualization", "1", { packages:pkgs, callback: function() {
      if (pkgCount != pkgs.length) {
        // Race condition where another setTimeout call snuck in after us; if
        // that call added a package, we must not shift its callback
        return;
      }
      while (callbacks.length > 0)
        callbacks.shift()();
    } });
  }, 100);
}
 
// jsFooter
 </script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartTreeMapID26a266914654"></script>
 
<!-- divChart -->
  
<div id="TreeMapID26a266914654"
  style="width: 450px; height: 320px;">
</div>


---

## Annotated time line data
Display time series data with notes.

```r
head(Stock)
```

```
##         Date  Device  Value          Title          Annotation
## 1 2008-01-01 Pencils   3000           <NA>                <NA>
## 2 2008-01-02 Pencils  14045           <NA>                <NA>
## 3 2008-01-03 Pencils   5502           <NA>                <NA>
## 4 2008-01-04 Pencils  75284           <NA>                <NA>
## 5 2008-01-05 Pencils  41476 Bought pencils Bought 200k pencils
## 6 2008-01-06 Pencils 333222           <NA>                <NA>
```


---

## Annotated time line


```r
A1 <- gvisAnnotatedTimeLine(Stock, datevar = "Date", numvar = "Value", idvar = "Device", 
    titlevar = "Title", annotationvar = "Annotation", options = list(displayAnnotations = TRUE, 
        legendPosition = "newRow", width = 600, height = 300), chartid = "ATLC")
plot(A1)
```

<iframe src="https://dl.dropboxusercontent.com/u/7586336/googleVisExamples/AnnotatedTimeLineExample.html" frameborder="0", width="620", height="350">Loading</iframe>

---

## Merging gvis-objects


```r
G <- gvisGeoChart(Exports, "Country", "Profit", 
                  options=list(width=250, height=120))
B <- gvisBarChart(Exports[,1:2], yvar="Profit", xvar="Country",                  
                  options=list(width=250, height=260, legend='none'))
M <- gvisMotionChart(Fruits, "Fruit", "Year",
                     options=list(width=400, height=380))
GBM <- gvisMerge(gvisMerge(G,B, horizontal=FALSE), 
                 M, horizontal=TRUE, tableOptions="cellspacing=5")
```


---

## Display merged gvis-objects

```r
plot(GBM)
```

<iframe src="https://dl.dropboxusercontent.com/u/7586336/googleVisExamples/gvisMergeExample.html" frameborder="0", width="620", height="420">Loading</iframe>

---

## Embedding googleVis chart into your web page

Suppose you have an existing web page and would like to integrate the output of a googleVis function, such as ```gvisMotionChart```.

In this case you only need the chart output from ```gvisMotionChart```. So you can either copy and paste the output from the R console


```r
print(M, "chart")  #### or cat(M$html$chart)
```

into your existing html page, or write the content directly into a file


```r
print(M, "chart", file = "myfilename")
```

and process it from there.

---

## Embedding googleVis output via iframe

* Embedding googleVis charts is often easiest done via the iframe tag:
* Host the googleVis output on-line, e.g. public Dropbox folder
* Use the iframe tag on your page:

```
<iframe width=620 height=300 frameborder="0"
src="http://dl.dropbox.com/u/7586336/RSS2012/line.html">
Your browser does not support iframe
</iframe>
```

---

## iFrame output

<iframe width=620 height=300 frameborder="0" src="http://dl.dropbox.com/u/7586336/RSS2012/line.html">You browser does not support iframe</iframe>

---

## Including googleVis output in knitr with plot statement

* With version 0.3.2 of googleVis `plot.gvis` gained the argument `'tag'`, which works similar to the argument of the same name in `print.gvis`. 

* By default the tag argument is `NULL` and `plot.gvis` has the same behaviour as in the previous versions of googleVis. 

* Change the tag to `'chart'` and `plot.gvis` will produce the same output as `print.gvis`. 

* Thus, setting the `gvis.plot.tag` value to `'chart'` in `options()` will return the HTML code of the chart when the file is parsed with `knitr`. 

* See the example in `?plot.gvis` for more details

---

## Blog articles with googleVis tips

* [How to set axis options in googleVis](http://lamages.blogspot.co.uk/2013/04/how-to-set-axis-options-in-googlevis.html)
* [World Bank data demo](http://lamages.blogspot.co.uk/2013/03/googlevis-042-with-support-for-shiny.html)
* [First steps of using googleVis on shiny](http://lamages.blogspot.co.uk/2013/02/first-steps-of-using-googlevis-on-shiny.html)
* [Using googleVis with knitr](http://lamages.blogspot.co.uk/2012/10/googlevis-032-is-released-better.html)
* [Rook rocks! Example with googleVis](http://lamages.blogspot.co.uk/2012/08/rook-rocks-example-with-googlevis.html)
* [Plotting share price data](http://lamages.blogspot.co.uk/2012/02/reshaping-world.html)

---

## Other R packages

*  [R animation package allows to create SWF, GIF and MPEG directly](http://animation.yihui.name/)
*  [iplots: iPlots - interactive graphics for R](http://cran.r-project.org/web/packages/iplots/)
*  [Acinonyx aka iPlots eXtreme](http://rforge.net/Acinonyx/index.html)
*  [gridSVG: Export grid graphics as SVG](http://cran.r-project.org/web/packages/gridSVG/index.html)
*  [plotGoogleMaps: Plot HTML output with Google Maps API and your own data](http://cran.r-project.org/web/packages/plotGoogleMaps/)
*  [RgoogleMaps: Overlays on Google map tiles in R](http://cran.r-project.org/web/packages/RgoogleMaps/index.html)
* [rCharts](http://ramnathv.github.io/rCharts/)
* [clickme](https://github.com/nachocab/clickme)

--- 

## How I created these slides


```r
library(slidify)
setwd("~/Dropbox/Lancaster/")
author("Introduction_to_googleVis")
## Edit the file index.Rmd file and then
slidify("index.Rmd")
```


---

## The End. So what ...? 

* googleVis brings interactive plots to R

* Use them to engage with other

* No more boring data

----

## Contact

* Markus Gesmann
* [markus.gesmann gmail.com](mailto:markus.gesmann@gmail.com)
* My blog: [http://lamages.blogspot.com](http://lamages.blogspot.com)

---

## Thanks

* Google, who make the visualisation API available
* All the guys behind www.gapminder.org and Hans Rosling for telling
    everyone that data is not boring 
* Sebastian Perez Saaibi for his inspiring talk on 'Generator
    Tool for Google Motion Charts' at the R/RMETRICS conference 2010
* Henrik Bengtsson for providing the 'R.rsp: R Server Pages'
    package and his reviews and comments
* Duncan Temple Lang for providing the 'RJSONIO' package
* Deepayan Sarkar for showing us in the lattice package how to deal
    with lists of options  
* Paul Cleary for a bug report on the handling of months:
    Google date objects expect the months Jan.- Dec. as 0 - 11 and
    not 1 - 12.
* Ben Bolker for comments on plot.gvis and the usage of temporary
    files  


---

## Thanks 

* John Verzani for pointing out how to use the R http help server
* Cornelius Puschmann and Jeffrey Breen for highlighting a
    dependency issue with RJONSIO version 0.7-1
* Manoj Ananthapadmanabhan and Anand Ramalingam for providing
    ideas and code to animate a Google Geo Map
* Rahul Premraj for pointing out a rounding issue with Google Maps 
* Mike Silberbauer for an example showing how to shade the
    areas in annotated time line charts
* Tony Breyal for providing instructions on changing the Flash
    security settings to display Flash charts locally 
* Alexander Holcroft for reporting a bug in gvisMotionChart
    when displaying data with special characters in column names
* Pat Burns for pointing out typos in the vignette

---

## Thanks

* Jason Pickering for providing a patch to allow for quarterly 
    and weekly time dimensions to be displayed with gvisMotionChart
* Oliver Jay and Wai Tung Ho for reporting an issue with one-row 
    data sets
* Erik Bülow for pointing out how to load the Google API via a
    secure connection
* Sebastian Kranz for comments to enhance the argument list for
    gvisMotionChart to make it more user friendly 
* Sebastian Kranz and Wei Luo for providing ideas and code to
    improve the transformation of R data frames into JSON code
* Sebastian Kranz for reporting a bug in version 0.3.0
* Leonardo Trabuco for helping to clarify the usage of the
    argument state in the help file of gvisMotionChart
* Mark Melling for reporting an issue with jsDisplayChart and
    providing a solution

---

## Thanks

* Joe Cheng for code contribution to make googleVis work with shiny
* John Maindonald for reporting that the WorldBank demo didn't 
    download all data, but only the first 12000 records.
* Sebastian Campbell for reporting a typo in the Andrew and Stock
    data set and pointing out that the core charts, such as line
  charts accept also date variables for the x-axis. 
* John Maindonald for providing a simplified version of the
    WorldBank demo using the WDI package.
* John Muschelli for suggesting to add 'hovervar' as an additional
    argument to gvisGeoChart.

---
## Session Info


```r
sessionInfo()
```

```
## R version 3.0.0 (2013-04-03)
## Platform: x86_64-apple-darwin10.8.0 (64-bit)
## 
## locale:
## [1] en_GB.UTF-8/en_GB.UTF-8/en_GB.UTF-8/C/en_GB.UTF-8/en_GB.UTF-8
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] XML_3.95-0.2    RJSONIO_1.0-3   googleVis_0.4.3 slidify_0.3.3  
## 
## loaded via a namespace (and not attached):
## [1] digest_0.6.3   evaluate_0.4.3 formatR_0.7    knitr_1.2     
## [5] markdown_0.5.4 stringr_0.6.2  tools_3.0.0    whisker_0.3-2 
## [9] yaml_2.1.7
```

