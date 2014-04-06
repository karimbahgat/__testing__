# This repository and README is just for my own use to test various GitHub and Markdown functionality. Nothing interesting to see here here. 

# MARKDOWN TESTING BELOW:

# Documentation for Python Geographic Visualizer (GeoVis)

A complete geographic visualization module for the Python programming language
intended for easy everyday-use by novices and power-programmers alike.
It has one-liners for quickly visualizing a shapefile,
building and styling basic maps with multiple shapefile layers,
and/or saving to imagefiles. Uses the built-in Tkinter
or other third-party rendering modules to do its main work.
The current version is functional, but should be considered
a work in progress with potential bugs, so use with care.

Dependencies: None, but it is recommended to have Aggdraw, PIL, or PyCairo.
System Compatibility: Python version 2.x and Windows. 
License: Creative Commons Attribution-ShareAlike (CC BY-SA). For more details see: http://creativecommons.org/licenses/by-sa/4.0/

Author: Karim Bahgat (karim.bahgat.norway<at>gmail.com)
Homepage: https://github.com/karimbahgat/geovis
Date: February 21, 2014


## Contents

### geovis.AskColor(...):
  
  Pops up a temporary tk window asking user to visually choose a color.
  

### geovis.AskFieldName(...):
  - no documentation for this function

### geovis.AskNumber(...):
  - no documentation for this function

### geovis.AskShapefilePath(...):
  - no documentation for this function

### geovis.AskString(...):
  - no documentation for this function

### geovis.Classifier(...) --> class object
  
A classifier that holds a set of instructions on how to classify a shapefile's visual symbols based on its attribute values. 
The classifier can hold multiple classifications, one for each symbol (e.g. fillsize and fillcolor), and these are added with the AddClassification method. 
When passed to a rendering operations the classifier is used as the recipe on how to symbolize the shapefile. 
This classifier is also needed to render a shapefile's legend.
  
  
| __some__ | __fake__ | __table__ 
| --- | --- | --- 
| for | class | args 
  

  - #### .AddClassification(...):
    
    
    Adds a classification/instruction to the classifier on how to symbolize a particular symbol part (e.g. fillcolor) based on a shapefile's attribute values.
    
    | __option__    | __description__ | __input__ | __input-comment__
    | --- | --- | --- | ---
    | symboltype | a string indicating which type of symbol the classification should apply to. | "fillsize" | the size of a circle, square, pyramid, or the thickness of a line
    | | | "fillwidth" | currently only used for the width of a pyramid when using the pyramid symbolizer
    | | | "fillheight" | currently has no use
    | | | "fillcolor" | hex color to fill the shape
    | | | "outlinewidth" | the width of the outline if any
    | | | "outlinecolor" | hex color to use for outline of shape
    | valuefield | a string with the name of a shapefile attribute field whose values will be used to inform the classification. | string
    | symbolrange | a list or tuple of the range of symbol values that should be used for the symbol type being classified. You only need to assign the edge/breakpoints in an imaginary gradient of symbol values representing the transition from low to high value classes; the values in between will be interpolated if needed. The symbol values must be floats or integers when classifying a size-based symbol type, or hex color strings when classifying a color-based symbol type. | list or tuple
    | classifytype | a string with the name of the mathematical algorithm used to calculate the break points that separate the classes in the attribute values. | "categorical" | assigns a unique class/symbol color to each unique attribute value, so can only be used when classifying color-based symbol types
    | | | "equal classes" | makes sure that there are equally many features in each class, which means that features with the same attribute values can be found in multiple classes
    | | | "equal interval" | classes are calculated so that each class only contains features that fall within a value range that is equally large for all classes
    | | | "natural breaks" | the Fisher-Jenks natural breaks algorithm, adapted from the Python implementation by Daniel J. Lewis (http://danieljlewis.org/files/2010/06/Jenks.pdf), is used to find 'natural' breaks in the shapefile dataset, i.e. where the value range within each class is as similar as possible and where the classes are as different as possible from each other. This algorithm is notorious for being slow for large datasets, so for datasets larger than 1000 records the calculation will be limited to a random sample of 1000 records (thanks to Carston Farmer for that idea, see: http://www.carsonfarmer.com/2010/09/adding-a-bit-of-classification-to-qgis/), and in addition that calculation will be performed 6 times, with the final break points being the sample mean of all the calculations. For large datasets this means that the natural breaks algorithm and the resultant map classification may turn out differently each time; however, the results should be somewhat consistent especially due to the random nature of the approach and the multiple sample means.
    | nrclasses | an integer or float for how many classes to subdivide the data and symbol values into. | Integer or float
    
    

  - #### .AddCustomClass(...):
    - no documentation for this method

  - #### .AddValue(...):
    - no documentation for this method

  - #### .CalculateClasses(...):
    - no documentation for this method

  - #### .GetClassifications(...):
    - no documentation for this method

  - #### .GetSymbol(...):
    - no documentation for this method

  - #### .GetValues(...):
    - no documentation for this method

### geovis.Color(...):
  
  Returns a hex color string of the color options specified.
  NOTE: New in v0.2.0, basecolor, intensity, and brightness no longer defaults to random, and it is no longer possible to call an empty Color() function (a basecolor must now always be specified).
  
  **Arguments:**
  
  | __option__    | __description__ | __input__
  | basecolor | the human-like name of a color. Always required, but can also be set to 'random'. | string
  | *intensity | how strong the color should be. Must be a float between 0 and 1, or set to 'random' (by default uses the 'strong' style values, see 'style' below). | float between 0 and 1
  | *brightness | how light or dark the color should be. Must be a float between 0 and 1 , or set to 'random' (by default uses the 'strong' style values, see 'style' below). | float between 0 and 1
  | *style | a named style that overrides the brightness and intensity options (optional). |
  
  Valid style names are:
  
  - 'strong'
  - 'dark'
  - 'matte'
  - 'bright'
  - 'pastelle'
  

### geovis.NewMap(...) --> class object
  
  Creates and returns a new map based on previously defined mapsettings.
  
  *Takes no arguments*
  

  - #### .AddLegend(...):
    
    Draws a basic primitive legend based on an input classifier object.
    
    **Arguments:**
    
    | __option__    | __description__
    

  - #### .AddShape(...):
    - no documentation for this method

  - #### .AddText(...):
    - no documentation for this method

  - #### .AddToMap(...):
    
    Add a shapefile to the map.
    
    **Arguments:**
    
    | __option__    | __description__
    | shapefilepath | the path string of the shapefile to add.
    | **customoptions | any series of named arguments of how to style the shapefile visualization (optional). Valid arguments are: fillcolor, fillsize (determines the circle size for point shapefiles, line width for line shapefiles, and has no effect for polygon shapefiles), outlinecolor, outlinewidth.
    

  - #### .DrawCircle(...):
    - no documentation for this method

  - #### .DrawLine(...):
    - no documentation for this method

  - #### .DrawRectangle(...):
    - no documentation for this method

  - #### .SaveMap(...):
    
    Save the map to an image file.
    
    **Arguments:**
    
    | __option__    | __description__
    | savepath      | the string path for where you wish to save the map image. Image type extension must be specified ('.png','.gif',...)
    

  - #### .ViewMap(...):
    
    View the created map embedded in a Tkinter window. Map image can be panned, but not zoomed. Offers a 'save image' button to allow to interactively save the image.
    

### geovis.SaveShapefileImage(...):
  
  Quick task to save a shapefile to an image.
  
  **Arguments:**
  
  | __option__    | __description__
  | shapefilepath | the path string of the shapefile.
  | savepath      | the path string of where to save the image, including the image type extension.
  | **customoptions | any series of named arguments of how to style the shapefile visualization (optional). Valid arguments are: fillcolor, fillsize (determines the circle size for point shapefiles, line width for line shapefiles, and has no effect for polygon shapefiles), outlinecolor, outlinewidth.
  

### geovis.SetMapBackground(...):
  
  Sets the mapbackground of the next map to be made. At startup the mapbackground is transparent (None).
  
  **Arguments:**
  
  | __option__    | __description__
  | mapbackground | takes a hex color string, as can be created with the Color function. It can also be None for a transparent background (default).
  

### geovis.SetMapDimensions(...):
  
  Sets the width and height of the next map. At startup the width and height are set to the dimensions of the window screen.
  
  **Arguments:**
  
  | __option__    | __description__
  | width         | an integer.
  | height        | an integer
  

### geovis.SetMapZoom(...):
  
  Not yet in use... Should be able to take xextents and yextents, as well as receive a shapefileobj or shapeobj to automatically zoom to their bboxes.
  

### geovis.SetRenderingOptions(...):
  
  Sets certain rendering options that apply to all visualizations or map images.
  
  **Arguments:**
  
  | __option__    | __description__
  | renderer | a string describing which Python module will be used for rendering. This means you need to have the specified module installed. Valid renderer values are 'aggdraw' (default), 'PIL', 'pycairo', 'tkinter'. Notes: If you have no renderers installed, then use Tkinter which comes with all Python installations, be aware that it is significantly slow, memory-limited, and cannot be used to save images. Currently PyCairo is not very well optimized, and is particularly slow to render line shapefiles. 
  | numpyspeed | specifies whether to use numpy to speed up shapefile reading and coordinate-to-pixel conversion. Must be True (default) or False.
  | reducevectors | specifies whether to reduce the number of vectors to be rendered. This can speed up rendering time, but may lower the quality of the rendered image, especially for line shapefiles. Must be True or False (default).
  

### geovis.Shapefile(...) --> class object
  - no documentation for this class

  - #### .ClearSelection(...):
    - no documentation for this method

  - #### .InvertSelection(...):
    - no documentation for this method

  - #### .SelectByQuery(...):
    
    Make a query selection on the shapefile so that only those features where the query evaluates to True are returned.
    
    **Arguments:**
    
    __option__    | __description__
    query | a string containing Python-like syntax (required). Feature values for fieldnames can be grabbed by specifying the fieldname as if it were a variable (case-sensitive). Note that evaluating string expressions is currently case-sensitive, which becomes particularly unintuitive for less-than/more-than alphabetic queries.
    inverted | a boolean specifying whether to invert the selection (default is False).
    

### geovis.ShapefileFolder(...):
  
  A generator that will loop through a folder and all its subfolder and return information of every shapefile it finds. Information returned is a tuple with the following elements (string name of current subfolder, string name of shapefile found, string of the shapefile's file extension(will always be '.shp'))
  **Arguments:**
  
  | __option__    | __description__
  | folder | a path string of the folder to check for shapefiles.
  

### geovis.ViewShapefile(...):
  
  Quick task to visualize a shapefile and show it in a Tkinter window.
  
  **Arguments:**
  
  | __option__    | __description__
  | shapefilepath | the path string of the shapefile.
  | **customoptions | any series of named arguments of how to style the shapefile visualization (optional). Valid arguments are: fillcolor, fillsize (determines the circle size for point shapefiles, line width for line shapefiles, and has no effect for polygon shapefiles), outlinecolor, outlinewidth.
  

