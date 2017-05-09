Introduction to data visualization
========================================================
author: John M. Drake & Andrew W. Park
date: 
autosize: true


Why this workshop
========================================================

"Coding is a basic science skill"
- Dr. James Olds, Assistant Director for Biological Sciences, National Science Foundation

Overview
========================================================

- Data visualization
- Data wrangling
- Writing computer programs
- Modeling
- Project management


R/RStudio
========================================================

![alt text](Rlogo.png)

***

<www.r-project.org/>


Why look at data?
========================================================

![alt text](data-visualise.png)


How to look at data?
========================================================

- Scatterplot
- Box-and-whisker diagram
- Barplot
- Map
- Network


A grammar of graphics
========================================================

Grammar - The fundamental principles or rules of an art or science (OED, quoted in Wickham 2010)

***

![alt text](wickham-2010-figs1-2.png)


A plot
========================================================

Consists of
- A dataset and mappings from *variables* to *aesthetics*
- One or more *layers*
- A *scale* for each mapping
- A *coordinate system*
- A *facet specification* (usually for multi-panel plots)

A layer
========================================================

Consists of
- Data and aethetic mapping
- A statistical transformation
- A geometric object
- Position adjustment

***

![alt text](wickham-2010-figs1-2.png)



A graphing template
========================================================

`ggplot(data=<DATA>) + <GEOM_FUNCTION>(mapping=aes(<MAPPINGS>))`


Aesthetics
========================================================

An *aesthetic* is a visual property attached to some data in a plot, e.g. 

* Size
* Shape
* Color

Slide With Plot
========================================================

![plot of chunk unnamed-chunk-1](visualization-presentation-figure/unnamed-chunk-1-1.png)

References
========================================================

Wickham, H. 2010. A layered grammar of graphics. *Journal of Computational and Graphical Statistics* 19:3–28

