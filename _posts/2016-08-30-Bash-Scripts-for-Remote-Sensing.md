---
layout:     post
title:      "Bash Scripts for Remote Sensing"
subtitle:   "Learn GNU/Linux command lines programming for Remote Sensing purposes"
date:       2016-08-30 12:00:00
author:     "Javier Lopatin"
header-img: "img/unix_terminal.png"
tags:
- Bash
- GDAL
---

In this short tutorial you will find some simple tools to process raster images in batch mode using GDAL in GNU/Linux systems.

GDAL is a translator library for raster and vector geospatial data formats that is released under an [X/MIT](https://trac.osgeo.org/gdal/wiki/FAQGeneral#WhatlicensedoesGDALOGRuse)
style [Open Source license by the Open Source Geospatial Foundation](http://www.osgeo.org/).

As GDAL is written in C/C++ is usually faster that other languages/software's, e.g. Python or R, so is usually a good idea learn at least basic syntaxes when processing big and/or many raters.

#### Some basic GDAL examples

- For example, GDAL can be use to convert the raster format. The command used for this task is call [`gdal_translate`](http://www.gdal.org/gdal_translate.html), and the syntax is like:

```bash
gdal_translate -of outputFormat inImage outImage
```

e.g., if you want to convert a IMG raster into GTiff, the syntax will be:

```bash
gdal_translate -of GTiff image.img image.tiff
```

- Other example is [`gdalwarp`](http://www.gdal.org/gdalwarp.html) and `gdalcalcstats` commands for image mosaicing, reprojection and warping, and obtation of pre-calculated statistics (usually to build pyramids and process big images), respectively. The syntaxes go like these:

```bash
 # to change a raster projection
gdalwarp -t_srs 'target projection' inImage.tif outImage.tif

# to change a raster resolution
gdalwarp -r cubic -multi -wt Float32 -of GTiff -tr outputResolution -outputResolution inImage.tif outImage.tif

# to build pyramids
gdalcalcstats inImage -ignore 0
```

More examples of GDAL utilities can be found [here](http://www.gdal.org/gdal_utilities.html).

#### Batch processing

Batch processing is very useful when working with many images. In GNU/Linux systems the syntaxis very simple:

```bash
for f in img1 img2 img3
do
 echo "Processing $f"
 # do something on $f
done
```
That code will apply the function `$f` to img1, img2 and img3. if you want to apply a function to all, e.g., `.tif` images in the inPath folder the code will be as follow:

```bash
FILES=inPath/*tif
for f in $FILES
do
 echo "Processing $f"
 # do something on $f
done
```

A real example could be convert all `.img` images to `.tif`:

```bash
FILES=inPath/*img
for f in $FILES
do
 echo "Processing $f"
 filename=`basename ${f} .${3}` # obtain the filename
 echo "Output: ${2}/${filename}.tif" # set the outImage
gdal_translate -of GTiff ${f} ${2}/${filename}.tif
done
```


#### Create executable scripts

Other powerful option is create executable bash scripts to use the above scripts.

For this matter you can save the bash cript in a `.sh` file and run it from the terminal, e.g.:

```bash
sh Convert2TIFF.sh
```

A more flexible option will be add Parser for command-line options. This can be done easily by adding `${N°}` statements, where for example a `${1}` and `${2}` correspond to the first and second arguments. For example:

```bash
FILES=$1/*.$3
for f in $FILES
do
  echo "Processing $f file..."
  filename=`basename ${f} .${3}`
  echo "Output: ${2}/${filename}.tif"
  gdal_translate -of GTiff ${f} ${2}/${filename}.tif
done
```

This code have 3 arguments: the first for the input directory , the second for the output directory and the last one for the input files extension (fixing the output format to `.tiff`). To run the code in the terminal and convert al `.img` images:

```bash
sh Convert2TIFF.sh inFolderPath outFolderPath img
```

You can download some bash scripts from [here](https://github.com/JavierLopatin/Bash-Scripts-for-Remote-Sensing).
