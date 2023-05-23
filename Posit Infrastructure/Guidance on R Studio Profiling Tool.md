# Guidance on R Studio Profiling Tool

## What is Profiling

Profiling is a form of analysing your code that measures, for example, the space (memory) or time usage for particular subsets of it, or the frequency and duration of function calls. The programmer can use profiling to measure how much computational resources are needed (memory / time), or to identify and optimize the slowest code portions.


## Installing `profvis`

To install `profvis` you can click on the `Profiling>Start Profiling` button on the top menu. Then, you will be displayed with the following pop-up:

![Profiling Pop-up](https://user-images.githubusercontent.com/46680486/240343188-329bfdfd-fd21-487f-9a41-7c64161bd5cb.png)

Click on `Yes`.

An alternative installation method is to run the following command in the console:
```r
install.packages("profvis")
```


## Using `profvis`

There are multiple ways to start and stop the profiler:

1. **From the Profile menu**, you can start and stop the profiler. Additionally, you can also run a selected block of code with profiling. The most simple workflow consists in starting the profiler, executing the code you want to analyse (e.g. sourcing a script) and then stopping the profiler.

2. **Calling the `profvis()` function**. For example:

```r
library(profvis)
profvis({
  data(diamonds, package = "ggplot2")
  plot(price ~ carat, data = diamonds)
  m <- lm(price ~ carat, data = diamonds)
  abline(m, col = "red")
})
```

At the end of both profiling procedures, you will be shown the `profvis` report, which is explained in the following section.

## Interpreting the results

The `profvis` report consists of two main parts: the Data view and the Flame Graph view. 

1. The **Data view** can be seen by clicking on the Data tab. It provides a top-down tabular display, reporting how much memory was used during the analysed processes and how much time they took. The information on the first level is of special interest as it allows **specifying the memory of the Posit Workbench instance** required for running the script. As an advice, instances should always be at least 25% \todo{does this seem too high?} higher than the maximum memory used on your script.

![Profvis Data View](https://user-images.githubusercontent.com/46680486/240356070-70f5827e-ce91-43a2-b977-9bef741d9394.png)

2. The **Flame Graph view** horizontal axis represents time in milliseconds, and the vertical direction represents the function calls stack. The bottom-most items on the stack represent the functions that take up the most time. As you travel up the stack, you can see which functions called other functions. This view, is recommended for spotting the subsets of your code that consume the most time, and therefore, it is a valuable input to explore how your code could be optimised.

![Profvis Flame Graph View](https://user-images.githubusercontent.com/46680486/240357493-4ccb9c32-fdcb-41a6-b646-86783766be09.png)