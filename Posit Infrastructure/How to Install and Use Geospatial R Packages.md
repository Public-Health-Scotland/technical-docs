# Installing and Using Geospatial R Packages

## Purpose

Geospatial R packages enable analysis and visualisation of geospatial data, such as maps, coordinates and spatial features.

This document aims to provide users of R in Posit Workbench guidance on how to compile, install and load geospatial R packages, specifically:

- [{sf}](https://r-spatial.github.io/sf/)
- [{terra}](https://rspatial.github.io/terra/)
- [{sp}](https://github.com/edzer/sp)
- [{raster}](https://rspatial.github.io/raster/reference/raster-package.html)
- [{leaflet}](https://rstudio.github.io/leaflet/)

Please note: {rgdal} has now been retired from CRAN and has therefore been removed from this documentation. However, versions of {leaflet} >= 2.2.0 do not depend on this package. To avoid dependency on obsolete packages, older versions should only be installed if strictly necessary. Please try to use the most up-to-date versions wherever possible.

## Setting environment variables

**!!! IMPORTANT !!!**

Geospatial R packages rely on geospatial libraries installed in the underlying Linux operating system.  We need to tell R where to find these geospatial libraries.  We do this by setting _environment variables_.

The following R code **must** be run _prior_ to compiling, installing and loading geospatial R packages.  You can do this by including this R code at the start of your R script.

```r
# Set environment variables to point to installations of geospatial libraries ----

## Amend 'LD_LIBRARY_PATH' ----

# Get the existing value of 'LD_LIBRARY_PATH'
old_ld_path <- Sys.getenv("LD_LIBRARY_PATH") 

# Append paths to GDAL and PROJ to 'LD_LIBRARY_PATH'
Sys.setenv(LD_LIBRARY_PATH = paste(old_ld_path,
                                   "/usr/gdal34/lib",
                                   "/usr/proj81/lib",
                                   sep = ":"))

rm(old_ld_path)

## Specify additional proj path in which pkg-config should look for .pc files ----

Sys.setenv("PKG_CONFIG_PATH" = "/usr/proj81/lib/pkgconfig")

## Specify the path to GDAL data ----

Sys.setenv("GDAL_DATA" = "/usr/gdal34/share/gdal")
```
Alternatively, you can include this code in your personal or the project's [.Rprofile](https://support.posit.co/hc/en-us/articles/360047157094-Managing-R-with-Rprofile-Renviron-Rprofile-site-Renviron-site-rsession-conf-and-repos-conf#:~:text=Rprofile-,.,directory%2C%20and%20project%2Dlevel%20.) file, and the R code will be run automatically every time you open a session or the project. See [Adding code to your .Rprofile](#adding-code-to-your-rprofile)

## Installing geospatial R packages

Geospatial R packages must be compiled and installed from source, rather than as binary files.  The reason for this is that the packages need to know where the geospatial libraries are installed in the underlying Linux operating system.  A simple call of the `install.packages()` function will not suffice.  As such, please follow the instructions below exactly.

### Step 1 - Remove geospatial R packages and their dependencies (if installed)

```r
# List of geospatial packages that will be installed
geo_pkgs <- c("leaflet", "raster", "sp", "terra", "sf")

# List of geospatial package dependencies
geo_deps <- unique(
  unlist(tools::package_dependencies(packages = geo_pkgs,
                                     recursive = TRUE)))

# Remove geospatial packages and their dependencies
pkgs_to_remove <- unique(unlist(c(geo_pkgs, geo_deps)))
remove.packages(pkgs_to_remove)
```

### Step 2 - Install the `{parallelly}` package to identify number of CPUs available

Packages will compile and install in significantly less time if your Posit Workbench session has multiple CPUs and you tell R to use these CPUs.

The `{parallelly}` package allows the number of CPUs available to be correctly identified in Posit Workbench session running in Kubernetes.

```r
# Remove 'parallelly' if it is already installed
remove.packages("parallelly")

# Install the 'parallelly' package
install.packages("parallelly")

# Identify the number of CPUs available
ncpus <- as.numeric(parallelly::availableCores())
```

### Step 3 - Install geospatial package dependencies that can be installed as binaries

Many of the dependencies of the geospatial R packages can be installed as binaries, rather than first being compiled from source.  Binaries are pre-compiled versions of the R packages.  Installing binaries is much faster than compiling from source, so it makes sense to install these dependencies as binaries.

```r
# Get list of geospatial package dependencies that can be installed as binaries
geo_deps_bin <- sort(setdiff(geo_deps, geo_pkgs))

# Remove packages that are already installed from the list of geospatial package dependencies
geo_deps_bin <- sort(setdiff(geo_deps_bin, as.data.frame(installed.packages())$Package))

# Install these as binaries
install.packages(pkgs = geo_deps_bin,
                 repos = c("https://ppm.publichealthscotland.org/all-r/__linux__/centos7/latest"),
                 Ncpus = ncpus)
```

### Step 4 - Install geospatial R packages from source

We first need to define the _configuration arguments_ that we will use to compile the geospatial R packages.  These tell R where the various geospatial libraries are installed and that the geospatial R packages should be compiled using this information.

```r
geo_config_args <- c("--with-gdal-config=/usr/gdal34/bin/gdal-config",
                     "--with-proj-include=/usr/proj81/include",
                     "--with-proj-lib=/usr/proj81/lib",
                     "--with-geos-config=/usr/geos310/bin/geos-config")
```

Now we can compile and install the geospatial R packages from source as follows:

_Note: this will take a while!_

```r
# Install the {sf} package
install.packages("sf",
                 configure.args = geo_config_args,
                 INSTALL_opts = "--no-test-load",
                 repos = c("https://ppm.publichealthscotland.org/all-r/latest"),
                 Ncpus = ncpus)

# Install the {terra} package
install.packages("https://ppm.publichealthscotland.org/all-r/latest/src/contrib/Archive/terra/terra_1.7-29.tar.gz",
                 repos = NULL,
                 type = "source",
                 configure.args = geo_config_args,
                 INSTALL_opts = "--no-test-load",
                 Ncpus = ncpus)

# Install the {sp} package
install.packages("sp",
                 configure.args = geo_config_args,
                 INSTALL_opts = "--no-test-load",
                 repos = c("https://ppm.publichealthscotland.org/all-r/latest"),
                 Ncpus = ncpus)

# Install the {raster} package
install.packages("https://ppm.publichealthscotland.org/all-r/latest/src/contrib/Archive/raster/raster_2.5-8.tar.gz",
                 repos = NULL,
                 type = "source",
                 configure.args = geo_config_args,
                 INSTALL_opts = "--no-test-load",
                 Ncpus = ncpus)

# Install the {leaflet} package
install.packages("https://ppm.publichealthscotland.org/all-r/latest/src/contrib/Archive/leaflet/leaflet_2.1.0.tar.gz",
                 repos = NULL,
                 type = "source",
                 dependencies = FALSE,
                 configure.args = geo_config_args,
                 INSTALL_opts = "--no-test-load",
                 Ncpus = ncpus)
```

## Loading geospatial R packages

Before you load any geospatial R packages, please make sure you run the code in [Setting environment variables](#Setting-environment-variables).  You **must** do this in every session you open before loading geospatial R packages.

You must also ensure that you loaded the geospatial libraries so that R can see them:

```r
dyn.load("/usr/gdal34/lib/libgdal.so")
dyn.load("/usr/geos310/lib64/libgeos_c.so", local = FALSE)
```

Again the above R code **must** be run in every session you open before loading geospatial R packages.

Then, geospatial R packages can be loaded in the same way as normal with calls to the `library()` function e.g.

```r
library(terra)
```

## Adding code to your .Rprofile

You can add code to your personal `.Rprofile` or create and add code to a project's file. Adding code to your personal `.Rprofile` will work *for you* but no one else, adding it to a project's `.Rprofile` will work *for anyone* loading the project but this will need to be done for every project (that uses geospatial packages).

You can use the [`{usethis}`](https://usethis.r-lib.org/) package to easily open the correct file.
-  `usethis::edit_r_profile("user")` will open your personal `.Rprofile` for editing.
-  `usethis::edit_r_profile("project")` will open the current project's  `.Rprofile` for editing (and will error if you're not in a project).

You should add all of the below code (comments are optional).

```r
# Set environment variables to point to installations of geospatial libraries ----

# Append paths to GDAL and PROJ to 'LD_LIBRARY_PATH'
Sys.setenv(
  LD_LIBRARY_PATH = paste(
    Sys.getenv("LD_LIBRARY_PATH"),
    "/usr/gdal34/lib",
    "/usr/proj81/lib",
    sep = ":"
  )
)

# Specify additional proj path in which pkg-config should look for .pc files ----

Sys.setenv("PKG_CONFIG_PATH" = "/usr/proj81/lib/pkgconfig")

# Specify the path to GDAL data ----

Sys.setenv("GDAL_DATA" = "/usr/gdal34/share/gdal")

# Load geospatial libraries
dyn.load("/usr/gdal34/lib/libgdal.so")
dyn.load("/usr/geos310/lib64/libgeos_c.so", local = FALSE)
```

<details>

<summary>This code will automatically add the required code</summary>

You will need to change `"~/.Rprofile"` to `"<path to project>/.Rprofile"` to make it work on a project.

```r
# Content to append
profile_content <- c(
  "# Set environment variables to point to installations of geospatial libraries ----",
  "# Append paths to GDAL and PROJ to 'LD_LIBRARY_PATH'",
  "Sys.setenv(LD_LIBRARY_PATH = paste(Sys.getenv(\"LD_LIBRARY_PATH\"), \"/usr/gdal34/lib\", \"/usr/proj81/lib\", sep = ':'))",
  "",
  "# Specify additional proj path in which pkg-config should look for .pc files ----",
  "Sys.setenv(\"PKG_CONFIG_PATH\" = \"/usr/proj81/lib/pkgconfig\")",
  "",
  "# Specify the path to GDAL data ----",
  "Sys.setenv(\"GDAL_DATA\" = \"/usr/gdal34/share/gdal\")",
  "",
  "# Load geospatial libraries",
  "dyn.load(\"/usr/gdal34/lib/libgdal.so\")",
  "dyn.load(\"/usr/geos310/lib64/libgeos_c.so\", local = FALSE)",
  ""
)

# Write to the .Rprofile - append if it already exists.
readr::write_lines(
  x = profile_content,
  file = "~/.Rprofile",
  append = TRUE
)
```

</details>
