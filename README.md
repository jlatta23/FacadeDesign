# Facade Design Tool - Project Showcase
3D Facade Design Tool. I discuss the design tool I built for a facade fabrication company.

Demo Version: https://app.designflows.com/

- [Background](#background)
- [Parametric Pattern Engine](#parametric-pattern-engine)
- [Material Optimizations - Genetic Algorithm](#material-optimizations---genetic-algorithm)
  - [Overview](#overview)
  - [Example Process](#example-process)
  - [How does the optimization algorithm work?](#how-does-the-optimization-algorithm-work)
- [Realtime Rendering](#realtime-rendering)
- [Automatic Revit Model Generation](#automatic-revit-model-generation)

# Background
The current way architects design facades is cumbersome and involves a lot of back and forth email communication. The current workflow for building facade design is some variant of:

1) Architect sketches facade elevations in CAD / BIM modeling software (1-4 hours)
2) Architect talks to manufacturer about their specific project (Teams and phone calls)
3) Architect sends CAD file and Fabricator calculates material optimization and pricing estimate (1 week)
4) Architect uses this to adjust his/her design
5) Repeat until the design matches aesthetics and price

This Facade Design Tool gives architects the power to do this all at their own convenience, leveraging the concepts of generative design.

![DesignStages](https://user-images.githubusercontent.com/90107864/214193219-47f6c33b-b6b4-4073-9aaa-57bbb8777a7c.png)


# Parametric Pattern Engine

The tool has a parametric pattern engine to lay out the facade panels. By defining rows, columns, and offsets, architects can create unique patterns that meet their aesthetic goals. 

The current industry technique involves having younger architectural draftsmen sketch out multiple panel configurations, taking up to an hour depending on the size and complexity. With this parametric engine and live updating 3D viewer, an architect can iterate through many ideas in a short amount of time. 

![ParametricPattern](https://user-images.githubusercontent.com/90107864/214188258-fb6c1578-a9f7-4fce-a648-7c671d7a5549.jpg)


# Material Optimizations - Genetic Algorithm
## Overview
There is a fundamental optimization problem during the facade design process: 

**Objective: Minimize Material Waste. Manufacturers make raw facade material in specific dimensions, so the architects must design panels that cut well out of these dimensions.**

This is a studied problem that falls under the names of "Shape Packing", "Shape Nesting", "2D Bin Packing", etc. However, many third party and open-source solutions don't directly fit our business needs. We built our own custom genetic algorithm due to extra contstraints and parameters (eg. certain materials have grooves that must align, or we want to re-use the leftover material ("offal") and certain sizes/shapes are more valuable).

## Example Process
Let's see how this process works using the Facade Design Tool and the desired pattern below.

![OptimizationFacade](https://user-images.githubusercontent.com/90107864/214717265-6be399ce-7d3c-4ffe-9c90-36ddb282ab19.jpg)

**1) Here are the manufacturer sheet sizes for this facade material and finish:**

![StandardSheetSizes](https://user-images.githubusercontent.com/90107864/214717671-ae49b2cb-891e-49c6-b533-11b809fb3b34.jpg)

**2) Let's get the panel dimensions used in the design.**

![OptimizationPanelList](https://user-images.githubusercontent.com/90107864/214717747-5bb708d6-532c-47be-8dd8-71cb343e67e0.jpg)

**3) Run the optimization: Calculate the best way to cut these panels out of the two sheet sizes.**
We can visually see how the algorithm placed the panels inside the manufacturer stock sheets. Some panels were simply entire sheets or sheets cut into two pieces while others involved complex placement.

The algorithm decided to use only the 120 x 48 inch stock sheets. This design only wastes 3.4% of the facade material, a very good result and well below the average of 23%.

![opt_result](https://user-images.githubusercontent.com/90107864/214728511-08d71c17-4ba0-4ba6-8083-059306350f91.jpg)


## How does the optimization algorithm work?

We created a genetic algorithm to calculate the "best" solution, where "best" means least material waste. In other contexts, a solution with more material waste but better waste dimensions, can be "better" because of handling and re-usability but that is outside the scope of this discussion. The problem of putting shapes into other shapes has come up in many different fields and is commonly referred to as the "2D Bin packing problem."  Computationally, it's an NP-hard problem so we should focus on developing solid heuristic algorithms. 

The genetic algorithm works like this:
1) Initialize a population of solutions. Include a lot that place the biggest panels first -- a solid heuristic.
2) Calculate the material waste for each solution (percentage of space that isn't a panel)
3) Select the best solutions to be parents for the next generation
4) Perform genetic mutations. Example mutations are to add some random sheets with random panels or find sheets with good optimization and repeat them.
5) Repeat steps 2-4. 

Usually it takes 10-40 seconds to find a good solution. There are many more flavors of this algorithm and extra constraints but they all follow this general process.

# Realtime Rendering

ThreeJS is a Javascript library for using Physically Based Rendering experiences. This design tool provides an interactive 3D environment with realistic materials.

By combining normal maps, AO maps, bump maps, with various lighting sources, we can achieve a realistic rendering of the manufacturer's facade material. The architect can zoom in, rotate, and pan around to see it from different angles.

![CoverPage](https://user-images.githubusercontent.com/90107864/214192717-2a647e37-1302-49d4-b9be-7f2e49eed6b8.jpg)

# Automatic Revit Model Generation

Revit is the modeling tool of choice of over 95% of architecture firms in the US. While it is a great tool for documenation, it is very cumbersome to create advanced models and layouts. This design tool automatically generates a Revit model once the architect has finalized their design.

![tutorialpopup_revit](https://user-images.githubusercontent.com/90107864/214193360-742a6300-95a8-4426-be42-063f08714c52.png)

