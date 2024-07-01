# Writing R Code that Runs in Parallel

## Purpose

This document aims to provide R users in Public Health Scotland with an introduction to the concepts of parallel processing, describe how to run `{dplyr}` code in parallel using the `{multidplyr}` package, explain the benefits of doing so, along with some of the downsides.

## Summary and Key Points

Parallel processing involves dividing a large computational task into smaller, more manageable tasks that can be executed simultaneously across multiple processors or cores. This approach can significantly speed up the execution time of complex computations, especially for data-intensive applications.

`{dplyr}` is a powerful package for data manipulation in R, but it operates on a single core (or CPU). `{multidplyr}` extends `{dplyr}` by allowing operations to be performed in parallel across multiple cores, potentially reducing computation time.

We will create a large dataset with 10 million rows and 256 numeric columns, then measure the time it takes to perform a data manipulation task using both `{dplyr}` and `{multidplyr}`.

## Parallel Processing

### What is Parallel Processing?

Parallel processing is a method of computation where many calculations or processes are carried out simultaneously. Large problems can often be divided into smaller ones, which can then be solved at the same time. This is particularly useful for tasks that require significant computational power and time.

### How Does Parallel Processing Relate to R?

R is a single-threaded language by default, meaning it processes tasks sequentially, one after the other. This can be a limitation when working with large datasets or performing complex computations. The `{multidplyr}` package addresses this limitation by enabling parallel processing within the `{dplyr}` framework.

`{multidplyr}` allows you to partition your data across multiple cores and perform `{dplyr}` operations in parallel. This can lead to significant performance improvements by utilising the full computational power of modern multi-core processors. By distributing the workload, `{multidplyr}` can reduce the time required for data manipulation tasks.

### Why Use Parallel Processing?

- **Speed**: By dividing tasks across multiple cores, parallel processing can significantly reduce the time required to complete large computations.
- **Efficiency**: It allows for better utilisation of available computational resources, making it possible to handle larger datasets and more complex analyses.
- **Scalability**: Parallel processing can scale with the number of available cores, making it suitable for both small and large-scale data processing tasks.

### Reasons You Might Not Use Parallel Processing

- **Overhead**: Setting up and managing parallel processes can introduce overhead, which might negate the performance benefits for smaller tasks.
- **Complexity**: Writing and debugging parallel code can be more complex than writing sequential code.
- **Memory Usage**: Parallel processing can increase memory usage, as each core may require its own copy of the data.

### Inherently (or Embarrasingly) Parallel Data Manipulation Tasks

Inherently (or embarrassingly) parallel tasks are those that can be easily divided into independent subtasks, each of which can be processed simultaneously without requiring communication between the subtasks. This type of parallelism is particularly efficient because it minimises the overhead associated with inter-process communication.

#### Examples of Inherently Parallel Tasks

1. Summarising data by groups (e.g., calculating the mean or sum for each group) can be done independently for each group.
2. Running the same computation with different sets of parameters; each parameter set can be processed independently.

## The `{multidplyr}` R package

The `{multidplyr}` R package is a backend for `{dplyr}` that facilitates parallel processing by partitioning data frames across multiple cores.  The package is part of the [Tidyverse](https://www.tidyverse.org/)

To use `{multidplyr}`, users first need to create a cluster of worker processes. Each worker is an independent R process that the operating system allocates to different cores.

The `partition()` function divides the data frame into chunks that are processed independently by each worker, ensuring that all observations within a group are assigned to the same worker, thus maintaining the integrity of grouped operations. Once the data is partitioned, users can perform various dplyr operations such as `mutate()`, `summarise()`, and `filter()` in parallel, and then collect the results using the `collect()` function.

For simpler operations or smaller datasets (less than ~10 million observations), the overhead of communication between nodes may outweigh the benefits of parallel processing.

### Example

#### Step 1: Creating a Large Dataset with 256 Numeric Columns

First, we will create a large dataset with 10 million rows and 256 numeric columns.

```r
# Load necessary libraries
library(dplyr)
library(multidplyr)
library(lubridate)
library(microbenchmark)

# Set seed for reproducibility
set.seed(123)

# Create a large dataset with 10 million rows and 256 numeric columns
n <- 10000000
num_cols <- 256
data <- data.frame(
  id = 1:n,
  dt = sample(seq(as.Date('2000/01/01'), as.Date('2024/01/01'), by="day"), n, replace = TRUE)
)

# Add 256 numeric columns
for (i in 1:num_cols) {
  col_name <- paste0("num", i)
  data[[col_name]] <- rnorm(n)
}

# Display the first few rows of the dataset
head(data)
```

| id | dt         | num1      | num2     | num3     | num4     | num5     | ... | num256   |
|----|------------|-----------|----------|----------|----------|----------|-----|----------|
| 1  | 2001-12-10 | -0.5604756| 9.073164 | 99.37355 | 0.487429 | 0.738325 | ... | 0.718781 |
| 2  | 2011-01-15 | -0.2301775| 9.183643 | 99.18364 | 0.738324 | 0.575781 | ... | 0.158325 |
| 3  | 2010-11-25 | 1.5587083 | 8.164371 | 98.16437 | 0.575781 | 0.694611 | ... | 0.368781 |
| 4  | 2004-01-01 | 0.0705084 | 9.595281 | 99.59528 | 0.694611 | 0.511781 | ... | 0.638325 |
| 5  | 2012-05-20 | 0.1292877 | 9.329508 | 99.32951 | 0.511781 | 0.738325 | ... | 0.498611 |

#### Step 2: Perform Data Manipulation with `{dplyr}`

We'll group the data by `dt` and calculate the mean of all 256 numeric columns.

```r
# Measure the time taken by dplyr
dplyr_time <- microbenchmark(
  dplyr = {
    result_dplyr <- data %>%
      group_by(dt) %>%
      summarise(across(starts_with("num"), \(x) mean(x, na.rm = TRUE)))
  },
  times = 3
)

# Print the summary of the benchmark
print(dplyr_time)
```

#### Step 3: Perform the same Data Manipulation in Parallel with `{multidplyr}`

We'll use `{multidplyr}` to parallelise the same operation across multiple cores.

```r
# Create a cluster with the desired number of workers
cluster <- new_cluster(parallelly::availableCores() - 1)
cluster_library(cluster, "dplyr")

# Partition the data across the cluster
data_partitioned <- data %>%
  group_by(dt) %>%
  partition(cluster)

# Measure the time taken by multidplyr
multidplyr_time <- microbenchmark(
  multidplyr = {
    result_multidplyr <- data_partitioned %>%
      summarise(across(starts_with("num"), \(x) mean(x, na.rm = TRUE))) %>%
      collect()
  },
  times = 3
)

# Print the summary of the benchmark
print(multidplyr_time)
```

#### Benchmarking Results

The results of running the example detailed above in a Posit Workbench session with 16 CPUs are summarised below.

The results show the minimum, lower quartile (lq), mean, median, upper quartile (uq), and maximum times taken for each method over 3 iterations.

| Method      | Min (s) | LQ (s) | Mean (s) | Median (s) | UQ (s) | Max (s) | Evaluations |
|-------------|---------|--------|----------|------------|--------|---------|-------------|
| dplyr       | 61.229  | 61.335 | 61.720   | 61.442     | 61.966 | 62.490  | 3           |
| multidplyr  | 6.849   | 6.976  | 7.962    | 7.104      | 8.519  | 9.934   | 3           |

The results clearly indicate that `{multidplyr}` significantly outperforms `{dplyr}` in terms of execution time for the given data manipulation task. The mean execution time for `{multidplyr}` is approximately 7.96 seconds, compared to 61.72 seconds for dplyr. This demonstrates the potential performance benefits of using parallel processing with `{multidplyr}` for large datasets.

