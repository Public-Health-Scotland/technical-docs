# Installing and Using Geospatial R Packages

## Purpose

Geospatial R packages enable analysis and visualisation of geospatial data, such as maps, coordinates and spatial features.

This document aims to provide users of R in Posit Workbench guidance on how to compile, install and load geospatial R packages, specifically:

- [{sf}](https://r-spatial.github.io/sf/)
- [{terra}](https://rspatial.github.io/terra/)
- [{sp}](https://github.com/edzer/sp)
- [{raster}](https://rspatial.github.io/raster/reference/raster-package.html)
- [{rgdal}](https://cran.r-project.org/web/packages/rgdal/index.html)
- [{leaflet}](https://rstudio.github.io/leaflet/)

## Setting environment variables

**!!! IMPORTANT !!!**

Geospatial R packages rely on geospatial libraries installed in the underlying Linux operating system.  We need to tell R where to find these geospatial libraries.  We do this by setting _environment variables_.

The following R code **must** be run _prior_ to compiling, installing and loading geospatial R packages.  You can do this by including this R code at the start of your R script.  Alternatively, you can include the R code in your project's [.Rprofile](https://support.posit.co/hc/en-us/articles/360047157094-Managing-R-with-Rprofile-Renviron-Rprofile-site-Renviron-site-rsession-conf-and-repos-conf#:~:text=Rprofile-,.,directory%2C%20and%20project%2Dlevel%20.) file, and the R code will be run automatically every time you open the project.

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

## Installing geospatial R packages

Geospatial R packages must be compiled and installed from source, rather than as binary files.  The reason for this is that the packages need to know where the geospatial libraries are installed in the underlying Linux operating system.  A simple call of the `install.packages()` function will not suffice.  As such, please follow the instructions below exactly.

### Step 1 - Remove geospatial R packages and their dependencies (if installed)

```r
# List of geospatial packages that will be installed
geo_pkgs <- c("leaflet", "rgdal", "raster", "sp", "terra", "sf")

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

# Identify number of CPUs available
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
install.packages("terra",
                 configure.args = geo_config_args,
                 INSTALL_opts = "--no-test-load",
                 repos = c("https://ppm.publichealthscotland.org/all-r/latest"),
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

# Install the {rgdal} package
install.packages("https://ppm.publichealthscotland.org/all-r/latest/src/contrib/Archive/rgdal/rgdal_1.5-25.tar.gz",
                 repos = NULL,
                 type = "source",
                 configure.args = geo_config_args,
                 INSTALL_opts = "--no-test-load",
                 Ncpus = ncpus)

# Install the {leaflet} package
install.packages("leaflet",
                 repos = c("https://ppm.publichealthscotland.org/all-r/__linux__/centos7/latest"),
                 Ncpus = ncpus)
```

## Loading geospatial R packages

Before loading any geospatial R packages, please ensure that you have run the code in [Setting environment variables](#Setting-environment-variables).  You **must** do this in every session that you open before loading geospatial R packages.

You must also ensure that you loaded the geospatial libraries so that R can see them:

```r
dyn.load("/usr/gdal34/lib/libgdal.so")
dyn.load("/usr/geos310/lib64/libgeos_c.so", local = FALSE)
```

Again the above R code **must** be run in every session that you open before loading geospatial R packages.

Then, loading geospatial R packages can be loaded in the same way as normal with calls to the `library()` function e.g.

```r
library(terra)
```
