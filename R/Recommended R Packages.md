# Recommended R packages

This non-exhaustive list of recommended R packages is aimed primarily at beginners. It introduces some commonly used R packages across PHS and groups them into relevant categories. The majority of packages listed cover routine tasks such as reading and writing data files and data manipulation, however there are also recommendations for more specialised areas such as statistical modelling and spatial analysis. If you or your team use a package that isn't mentioned, feel free to recommend it through an [issue](https://github.com/Public-Health-Scotland/technical-docs/issues/new/choose) after reviewing the [contribution guidance](https://github.com/Public-Health-Scotland/technical-docs/blob/main/CONTRIBUTING.md).

Some packages are listed in multiple categories (such as the [DT](https://github.com/rstudio/DT) package which is relevant to data visualisation, RMarkdown and Shiny). Where possible, a link to the relevant GitHub repository for each package is provided. Additionally, Tidyverse is mentioned but is a suite of packages which some other packages are a part.

## Reading and writing data

Package | Description
--- | ---
[phsopendata](https://github.com/Public-Health-Scotland/phsopendata) | PHS package for interacting with the Open Data platform.
[odbc](https://github.com/r-dbi/odbc) | For connecting to database management systems, such as the SMRA datasets.
[readr](https://github.com/tidyverse/readr) | For reading and writing flat files, such as CSV files.
[haven](https://github.com/tidyverse/haven) | For reading and writing SPSS, SAS and Stata files.
[openxlsx](https://github.com/ycphs/openxlsx) | For reading and writing Excel files.
[officer](https://github.com/davidgohel/officer) | For manipulation of Microsoft Word and PowerPoint documents.
[dbplyr](https://github.com/tidyverse/dbplyr) | A `dplyr` back-end for database interaction.
[here](https://github.com/r-lib/here) | For defining relative filepaths when using [RStudio Projects](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects).

## Data manipulation

Package | Description
--- | ---
[phsmethods](https://github.com/Public-Health-Scotland/phsmethods) | PHS package for common data manipulation methods.
[tidyverse](https://github.com/tidyverse) | A collection of related R packages used for data manipulation.
[dplyr](https://github.com/tidyverse/dplyr) | For selecting, filtering, aggregating and other basic operations.
[tidyr](https://github.com/tidyverse/tidyr) | For 'tidying' data, primarily by converting columns to rows and vice-versa.
[stringr](https://github.com/tidyverse/stringr) | For manipulation of character strings.
[lubridate](https://github.com/tidyverse/lubridate) | For working with dates.
[janitor](https://github.com/sfirke/janitor) | For 'cleaning' variable names and data.

## Data visualisation

Package | Description
--- | ---
[phsstyles](https://github.com/Public-Health-Scotland/phsstyles) | PHS package for data visualisation styles.
[ggplot2](https://github.com/tidyverse/ggplot2) | For creating static charts for reports.
[plotly](https://github.com/ropensci/plotly) | For creating interactive charts.
[gganimate](https://github.com/thomasp85/gganimate) | For 'animating' ggplot2 charts.
[leaflet](https://github.com/rstudio/leaflet) | For creating interactive maps.
[DT](https://github.com/rstudio/DT) | For creating interactive tables.
[scales](https://github.com/r-lib/scales) | Scale functions for visualisation.

## RMarkdown

Package | Description
--- | ---
[phstemplates](https://github.com/Public-Health-Scotland/phstemplates/tree/main/R) | PHS package for file templates, including R Markdown templates.
[rmarkdown](https://github.com/rstudio/rmarkdown) | For creating dynamic Word, HTML, PDF and PowerPoint documents using R.
[knitr](https://github.com/yihui/knitr) | For rendering RMarkdown documents.
[DT](https://github.com/rstudio/DT) | For creating interactive tables in HTML documents generated using RMarkdown.

## Shiny

Package | Description
--- | ---
[shiny](https://github.com/rstudio/shiny) | For creating interactive web applications using R.
[shinydashboard](https://github.com/rstudio/shinydashboard) | For customising the layout of Shiny applications.
[shinyWidgets](https://github.com/dreamRs/shinyWidgets) | For extending the widgets available in Shiny.
[shinyjs](https://github.com/daattali/shinyjs) | For performing common JavaScript operations in Shiny applications.
[DT](https://github.com/rstudio/DT) | For creating interactive tables.

## Statistical modelling

Package | Description
--- | ---
[tidymodels](https://github.com/tidymodels) | A collection of tidyverse-inspired related R packages used for statistical modelling.
[broom](https://github.com/tidymodels/broom) | For converting statistical analyses objects into 'tidy' format.
[car](https://github.com/cran/car) | For conducting analysis of variance (ANOVA).
[lme4](https://github.com/lme4/lme4) | For fitting mixed-effects models.
[mgcv](https://github.com/cran/mgcv) | For fitting flexible, non-linear models such as Generalised Additive (Mixed) Models.
[survival](https://github.com/therneau/survival) | For survival analysis.

## Spatial analysis

Package | Description
--- | ---
[sp](https://github.com/edzer/sp) | For loading and manipulating spatial data.
[rmapshaper](https://github.com/ateucher/rmapshaper) | For manipulating spatial data.
[leaflet](https://github.com/rstudio/leaflet) | For creating interactive maps.

## Package Creation and Management

Package | Description
--- | ---
[devtools](https://github.com/r-lib/devtools) | For simplifying common tasks in package development.
[testthat](https://github.com/r-lib/testthat) | For unit testing of functions.
[roxygen2](https://github.com/klutometis/roxygen) | For generating `.Rd` files required to pass `R CMD Check`.
[usethis](https://github.com/r-lib/usethis) | For automating repetitive tasks during package setup.
[remotes](https://github.com/r-lib/remotes) | Installing packages from distributed version control (e.g. GitHub or Gitea).
[pacman](https://github.com/trinker/pacman) | Package management tools for use in R.
