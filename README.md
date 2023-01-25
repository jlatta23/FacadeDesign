# Facade Design Tool - Project Showcase
3D Facade Design Tool. I discuss the design tool I built for a facade fabrication company.

Demo Version: https://app.designflows.com/

- [Parametric Pattern Engine](#para-pattern)

# Background
The current way architects design facades is cumbersome and involves a lot of back and forth email communication. The current workflow for building facade design is some variant of:

1) Architect sketches facade elevations in CAD / BIM modeling software (1-4 hours)
2) Architect talks to manufacturer about their specific project
3) Architect sends over CAD file to fabricator for price estimate and feedback
5) Fabricator calculates material optimization and pricing estimate (1 week)
6) Architect uses this to adjust his/her design
7) Repeat until the design matches aesthetics and price

This Facade Design Tool gives architects the power to do this all at their own convenience, leveraging the concepts of generative design.

![DesignStages](https://user-images.githubusercontent.com/90107864/214193219-47f6c33b-b6b4-4073-9aaa-57bbb8777a7c.png)


# Parametric Pattern Engine

The tool has a parametric pattern engine to lay out the facade panels. By defining rows, columns, and offsets, architects can create unique patterns that meet their aesthetic goals. 

The current industry technique involves having younger architectural draftsmen sketch out multiple panel configurations, taking up to an hour depending on the size and complexity. With this parametric engine and live updating 3D viewer, an architect can iterate through many ideas in a short amount of time. 

![ParametricPattern](https://user-images.githubusercontent.com/90107864/214188258-fb6c1578-a9f7-4fce-a648-7c671d7a5549.jpg)


## Material Optimizations - Genetic Algorithm
### Overview
There is a fundamental optimization problem during the facade design process: 

**Objective: Minimize Material Waste. Manufacturers make raw facade material in specific dimensions, so the panels architects design must be cut out of these dimensions. How do we cut the panels out of standard sheet sizes to minimize material waste?**

This is a studied problem that falls under the names of "Shape Packing", "Shape Nesting", "2D Bin Packing". However, many third party and open-source solutions don't directly fit our business needs. We built our own custom genetic algorithm due to extra contstraints and parameters (eg. certain materials have grooves that must align, we want to re-use the leftover material ("offal") and rectangular leftover material is more valuable).

### Example Process
Let's calculate the material optimization for this facade.
![OptimizationFacade](https://user-images.githubusercontent.com/90107864/214717265-6be399ce-7d3c-4ffe-9c90-36ddb282ab19.jpg)

**1) Here are the manufacturer sheet sizes for this facade material:**

![StandardSheetSizes](https://user-images.githubusercontent.com/90107864/214717671-ae49b2cb-891e-49c6-b533-11b809fb3b34.jpg)

**2) Let's get the panel dimensions used in the design.**

![OptimizationPanelList](https://user-images.githubusercontent.com/90107864/214717747-5bb708d6-532c-47be-8dd8-71cb343e67e0.jpg)

**3) Run the optimization: Calculate the best way to cut these panels out of the two sheet sizes.**
We can visually see how the algorithm placed the panels inside the manufacturer stock sheets. Some panels were merely entire sheets or sheets cut into two piece while others involved complex placement. This design only wastes 3.4% of the facade material, a very good result and well below the average of 23%.

![results](https://user-images.githubusercontent.com/90107864/214718511-c29377e0-8387-475f-8b02-ac5e75862932.jpg)

### How does the optimization algorithm work?

## Realtime Rendering - ThreeJS

ThreeJS is a Javascript library for using Physically Based Rendering experiences. This design tool provides an interactive 3D environment with realistic materials.

By combining normal maps, AO maps, bump maps, with various lighting sources, we can achieve a realistic rendering of the manufacturer's facade material. The architect can zoom in, rotate, and pan around to see it from different angles.

![CoverPage](https://user-images.githubusercontent.com/90107864/214192717-2a647e37-1302-49d4-b9be-7f2e49eed6b8.jpg)

## Automatic 3D Revit Model Generation

Revit is the modeling tool of choice of over 95% of architecture firms in the US. While it is a great tool for documenation, it is very cumbersome to create advanced models and layouts. This design tool automatically generates a Revit model once the architect has finalized their design.

![tutorialpopup_revit](https://user-images.githubusercontent.com/90107864/214193360-742a6300-95a8-4426-be42-063f08714c52.png)

