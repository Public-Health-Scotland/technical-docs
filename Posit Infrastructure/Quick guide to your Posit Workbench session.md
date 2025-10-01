# Quick guide to your Posit Workbench session

## Who is this for?

* Every user of the Posit Workbench, regardless of expertise level. 
* The information has been kept as basic as possible.

## What is this quick guide about?

* Many of us are using much less memory and CPUs than we have requested for our sessions.
* This is inefficient: Posit is hosted on a pay-as-you-go Cloud platform (Microsoft Azure), so we should minimise costs by ensuring we only request the resources we need each time.
* This guide contains tips for making your sessions more efficient.  

## How much memory do I need?

Computer random access memory (RAM) gives applications a place to store and quickly access data that are actively in use. This is referred to as memory.
Your session needs to have sufficient memory available to be able to load the required data into memory and load the required packages. Use the table below as a starting point:

| Number of rows | Number of columns | Session memory recommendation |
|---|---|---|
| <= 100,000 | <= 10 | 2,048 MB (2GB) |
| <= 1 million | <= 5 | 4,096 MB (4 GB) (the session default)  |
| <= 1 million | <= 10 | 8,192 MB (8 GB) |
| <= 10 million | <= 5 | 32,768 MB (32 GB) |
| <= 10 million | <= 10 | 65,536 MB (64 GB) |
| <= 10 million | <= 100 | 786,432 MB (768 GB) |

During your session, you can see how much memory you've used using the pie chart graphic on the Environment tab. Checking this when you use Posit Workbench will help you learn how much memory your typical sessions are likely to require. 

![Memory usage pie chart](https://github.com/Public-Health-Scotland/technical-docs/assets/110984847/338dd117-417d-4436-be3a-87347176adbc)

Remember you can also remove unused data frames from memory as suggested in the "Coding with R Section" of the [Best Practice with R in Posit Workbench](Best%20Practice%20with%20R%20in%20Posit%20Workbench.md) document.  

More detailed information on the Knowledge Base:

*	[Memory usage when processing SMR01](Memory%20Usage%20in%20SMR01.md)

*	[More technical information about Kubernetes profiles, memory, and CPU](Posit%20Workbench%20and%20Kubernetes.md)

*	[How to Use the R Studio Profiling Tool](How%20to%20Use%20the%20R%20Studio%20Profiling%20Tool.md): for measuring how much time and memory are required for a script. Optimal memory and CPU requirements, plus run time, could then be added to the script's header. 

## How many CPUs do I need?  
The Central Processing Unit (CPU) is the primary component of a computer that executes instructions.

*	For writing and running chunks of code in an interactive session, 1 CPU is more than sufficient. 
*	If you are running code that relies on parallel processing (things like matrix multiplications or complex statistical models) you could request 2 or more CPUs. Check to see if this speeds up the processing (and whether this compensates for the additional cost of 6p per hour per number of CPUs).

## What if my session needs to run overnight?
*	Sessions are closed automatically at 7:15pm every day.
*	If you have work that needs to continue beyond 7:15pm you should add the word NIGHT at the start of the session name when starting that session. If you're working on a project, your project will also need the word NIGHT in its name.

## How can I use less memory?
Using the parquet file format from the `{arrow}` package uses less memory and is faster to write. 

*	Install and load the arrow package
```{r}
install.packages("arrow", repos = c("https://ppm.publichealthscotland.org/all-r/__linux__/centos7/latest"))
library("arrow")
```
*	Write files using `write_parquet()`:
```{r}
data("iris")
write_parquet(iris, "my_iris_data.parquet", compression = "zstd")
rm(iris)
```
*	Read data in using `read_parquet()`:
```{r}
my_iris_data <- read_parquet("my_iris_data.parquet")
```
* Read only the subset of columns you need with the `col_select` argument.
```{r}
my_iris_data <- read_parquet("my_iris_data.parquet", col_select = c(Species, starts_with("Sepal")))
```


## Symptoms of not having requested enough memory/CPU:
If your session tries to use more memory than requested, the session will close. Prior to this occurring, you may notice that files can't be autosaved and the session becomes unresponsive.  	

## My profile is too small: how can I request more memory/CPU?
*	Your Kubernetes profile is initially set to 1 CPU and a maximum of 4096 MB of memory.
*	If you find you need more CPU/memory, please complete [this form](https://forms.office.com/e/VEutAJ8p9Y)
  
## Further general information about Posit Workbench sessions:
*	[Best Practice with R in Posit Workbench](Best%20Practice%20with%20R%20in%20Posit%20Workbench.md)
* [Recommended Global Options for RStudio](Recommended%20Global%20Options%20for%20RStudio.md)


