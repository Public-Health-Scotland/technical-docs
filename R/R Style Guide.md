# R Style Guide

This document is a coding style guide for using R within PHS. It is designed to allow enough flexibility for working on different projects while maintaining consistency across the organisation and ensuring that code can be easily read and shared. As a foundation, the [Tidyverse style guide](https://style.tidyverse.org/) is used, with some additional guidance on how to use R in a way that is consistent with the rest of PHS.

*Adapted from guidance originally written by Anna Price and David Caldwell, Public Health Scotland.*

***

## 1 - Information at the start of a script

Every script should begin with the following basic information:  

* Name of file
* Data release (if applicable)
* Original author(s)\*
* Original date\*
* Updated by\*
* Updated date\*

* Written/run on (e.g. Posit Workbench - RStudio)
* Version of R that the script was written for

* Description of content

* Approximate run time
* Approximate memory usage

\* This information is not required if Git (or another version control system) is being used to track changes to a script.

## 2 - Sections

All scripts should be split into numbered sections. This should be done using at least three hashes (`#`) at the start of a section header in order to clearly differentiate section titles from general annotations.

Following the section header with at least four dashes (or hashes) also allows sections to collapse and an automatic contents table to be created in the "Jump To" menu at the bottom of the editor for navigation. (Note that when writing R Markdown scripts, collapsable sections are created using at least one hash at the start of a line.)

We recommend using sub-sections, creating headings with 1 or 2 leading hashes, especially if particular sections are very long.

RStudio has a shortcut for creating sections - either press `ctrl`+`shift`+`R` or go to Code in the main menu and select Insert section.

## 3 - Structure

The exact structure of a script should be decided by the analyst writing the code and should be appropriate for the analyses being carried out. However, as a general rule, there should be a housekeeping section at the start - this should be the only section of the script which requires manual changes for future updates and includes:

* loading packages
* setting filepaths and extract dates
* functions (defined here or sourced from another file)
* setting plot parameter
* specifying codes (e.g. ICD-10 codes) once for generic calculations such as incidence rates

If the script is part of a project with multiple scripts, it is instead recommended that code for all scripts that require manual changes for future updates be kept in a separate script that is then sourced using the `source()` function. This minimises the number of edits required which lowers the risk of error. If there is a conflict, e.g., two scripts need a different `start_date` variable, both should be defined with clear naming.

Finally, it is useful to mark the end of a script, e.g., `### END OF SCRIPT ###`

## 4 - Commenting

Scripts should be appropriately commented. Comments are used to explain your code to others who may have to interact with the code. They should be succinct so that the script is readable but detailed enough so that another analyst could understand, run and edit it.

Comments can also be used for instruction and if so this should be clearly marked e.g.
`# TO DO - Needs re-written to reduce looping`

Use one hash to comment out annotations.

It is also important that code-readability shouldn't rely on comments. If the code is not clear enough to be understood without comments, consider rewriting.

## 5 - Functions

R is a functional language. Using functions improves code readability, testability and shareability. Functions should generally be used in preference to loops in order to reduce the amount of code needed.

Small functions which are specific to one piece of analysis should be defined in the housekeeping section at the start, but generic functions which are used across a project or multiple projects should be saved in a separate script and sourced in. Function names should be verbs which describe what the function does.

## 6 - Checks and warnings

Checks, conditional operations and warnings should be built into code in order to automate processes as much as possible. For example, the following code produces `NA` if a number of less than 10 is given, and returns a warning.

```{r}
x <- 9
if (x <= 10) {
  warning("`x` must be less than 10 to produce a model.")
  result <- NA
} else {
  result <- coef(glm(rpois(x, lambda = 5) ~ 1))
}
```

## 7 - Projects

It is highly recommended that you **use RStudio projects**, which organize your work into different contexts, each one with a different working directory. Projects eliminate the need to set up your working directory each time, allow you to use Git for version control and allow you to have multiple R sessions open at the same time (each one with a different project), as well other perks to help you manage your work.

A blank R project structure can be downloaded from the GitHub repo, [r-project-structure](https://github.com/Public-Health-Scotland/r-project-structure). A similar blank structure for R Shiny apps can be found in [rshiny-project-structure](https://github.com/Public-Health-Scotland/rshiny-project-structure). A PHS package has also been developed with templates, [phstemplates](https://github.com/Public-Health-Scotland/phstemplates).

## 8 - Recommended packages and Tidyverse

Just as the foundation for the PHS R Style guide is the Tidyverse style guide, so is the foundation for the recommended packages. [Recommended R packages](Recommended%20R%20Packages.md) are documented, and updated based on how we use R at PHS.

It's also worth noting that "tidy" data analysis is best performed on data in a tidy (long) format, where each column represents one variable and each row represents one observation ([Hadley Wickham, 2014](https://www.jstatsoft.org/article/view/v059i10)).

## 9 - Recommended style guide

We recommend following Hadley Wickham's [tidyverse style guide](http://style.tidyverse.org/). Please refer to this document for guidance on:

* file names
* object names
* spacing
* indentation
* curly brackets
* assignment

To help clean up your code, the [`{lintr}`](https://lintr.r-lib.org/) package provides an automated check for compliance with the tidyverse style guide and warns you about potential mistakes or problems.

Even better the [`{styler}`](https://styler.r-lib.org/) package can automatically reformat code (making only cosmetic changes) so that you can always have consistent well formatted code with minimal effort.

## 10 - R User Group

The PHS R User Group shares good practice amongst the user community and is a useful support system for users requiring assistance. You can join the [PHS R User Group on Teams](https://teams.microsoft.com/l/team/19%3ae9f55a12b7d94ef49877ff455a07f035%40thread.tacv2/conversations?groupId=ec4250f9-b70a-4f32-9372-a232ccb4f713&tenantId=10efe0bd-a030-4bca-809c-b5e6745e499a) for news, events, and technical queries.
