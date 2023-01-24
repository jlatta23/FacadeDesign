# Facade Design Tool - JR Latta Project Showcase
3D Facade Design Tool. Realtime Rendering, Material Optimizations, Parametric Pattern Creation, Auto Generate 3D Revit Object
This is a page to discuss the design tool I built for a facade fabrication company.

Demo Version: https://app.designflows.com/

![DesignStages](https://user-images.githubusercontent.com/90107864/214193219-47f6c33b-b6b4-4073-9aaa-57bbb8777a7c.png)

## Background
The current workflow for building facade design is:

1) Architect sketches facade elevations in CAD / BIM modeling software
2) Architect talks to manufacturer about their specific project
3) Architect sends over CAD file to fabricator for price estimate and feedback
4) Manufacturer sends architect samples of the materials
5) Fabricator calculates material optimization and pricing estimate
6) Architect uses this to adjust their design
7) Repeat until the design matches aesthetics and price

My Facade Design Tool gives architects the power to design this.
* Architect designs their project using design tool


## Parametric Pattern Engine

![ParametricPattern](https://user-images.githubusercontent.com/90107864/214188258-fb6c1578-a9f7-4fce-a648-7c671d7a5549.jpg)
The parametric pattern engine makes facade panel layout creation much easier. By defining rows and offsets, architects can create unique patterns that meet their aesthetic goals.

## Material Optimizations - Genetic Algorithm
There is a fundamental optimization problem during the facade design process: 

**How do we cut the panels out of standard sheet sizes to minimize material waste?**

This is a studied problem that falls under the names of "Shape Packing", "Shape Nesting", "2D Bin Packing". We built our own custom genetic algorithm due to extra contstraints and parameters (eg. certain materials have grooves that must align, we want to re-use the leftover material ("offal") and rectangular leftover material is more valuable)

This becomes a generative design process when architects iterate on their facade concepts. By giving architects the ability to automatically calculate these optimal material utilizations, they can create an aesthetically pleasing pattern that performs well.

![tutorialpopup_optimizationresultstab](https://user-images.githubusercontent.com/90107864/214191956-80439a72-d99d-4abc-9336-1254f5e0bd73.png)

## Realtime Rendering - ThreeJS

ThreeJS is a Javascript library for using Physically Based Rendering experiences. This design tool provides an interactive 3D environment with realistic materials.

![CoverPage](https://user-images.githubusercontent.com/90107864/214192717-2a647e37-1302-49d4-b9be-7f2e49eed6b8.jpg)

## Automatic 3D Revit Model Generation

Revit is the modeling tool of choice of over 95% of architecture firms in the US. While it is a great tool for documenation, it is very cumbersome to create advanced models and layouts. This design tool automatically generates a Revit model once the architect has finalized their design.

![tutorialpopup_revit](https://user-images.githubusercontent.com/90107864/214193360-742a6300-95a8-4426-be42-063f08714c52.png)

