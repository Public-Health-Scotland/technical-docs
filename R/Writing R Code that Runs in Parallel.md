# Writing R Code that Runs in Parallel

## Purpose

This document aims to provide R users in Public Health Scotland with an introduction to the concepts of Parallel Processing, describe how to run `{dplyr}` code in parallel using the `{multidplyr}` package, explain the benefits of doing so, along with some of the downsides.

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

## Example

### Creating a Large Dataset with 256 Numeric Columns

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
