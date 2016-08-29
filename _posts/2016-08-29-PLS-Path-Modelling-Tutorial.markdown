---
layout:     post
title:      "PLS Path Modeling"
subtitle:   "Path analysis to model Remote Sensing data"
date:       2016-08-29 12:00:00
author:     "Javier Lopatin"
header-img: "_posts/PLS-Path-Modelling-Tutorial-Figures/output_4_0.png"
---


<p>This is a tutorial about PLS Path Modeling applied to Geocience. The sample data is part of the analysis of <a href="http://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6990570">THIS</a> paper.</p> 
<p>See more information on PLS-PM <a href="http://gastonsanchez.com/PLS_Path_Modeling_with_R.pdf">here</a>.</p>



```R
library(plspm)

## set working directory
setwd("C:/Users/Lopatin/Dropbox/Publicaciones/OBIA-PLSPM")
 
## Load data
datapls <- read.table("datapls.txt", header=T, sep="", dec=".") 
```


```R
## Set the inner model
# rows of the inner model matrix
Hieght.Canopies  = c(0, 0, 0, 0, 0, 0, 0)
Midle1.Canopies  = c(0, 0, 0, 0, 0, 0, 0)
Midle2.Canopies  = c(0, 0, 0, 0, 0, 0, 0)
Low.Canopies     = c(0, 0, 0, 0, 0, 0, 0)
OBIA             = c(1, 1, 1, 1, 0, 0, 0)
Topography       = c(0, 0, 0, 0, 0, 0, 0)
Richness         = c(0, 0, 0, 0, 1, 1, 0)
```
