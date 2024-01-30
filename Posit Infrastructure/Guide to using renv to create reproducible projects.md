# Guide to using [{renv}](https://rstudio.github.io/renv/) to create reproducible projects

## Purpose

Our code should be reproducible and shareable. But sometimes things fail to run properly when we return to them, or on a colleague's machine. The R package [{renv}](https://rstudio.github.io/renv/) ensures that the exact set of packages (and their versions) required to run the code in a specific project are recorded and kept available to current and future users. 

This guide provides basic step-by-step instructions for using [{renv}](https://rstudio.github.io/renv/), as well as more detailed information. 

## Step-by-step instructions

Pre-requisite: a project (preferably version-controlled using git).

#### Setting up [{renv}](https://rstudio.github.io/renv/) for the first time in a project:
1.	Open the project.
2.	Call `renv::init()` to initialise renv within that project. This can take a while depending on the size of the project.
3.	Calling `renv::status()` should confirm the new 'lockfile' is synced with the project (i.e., contains details of all the required packages).
4.	Commit the changes (additional files and folders) to version control.

#### Adding (/removing) packages to the project:
1.	Install (or remove) the required packages as usual. 
2.	Change the code, by adding (or removing) calls to `library()` or `require()`.
3.	Calling `renv::status()` will tell you there are changes that aren’t recorded in the lockfile.
4.	Calling `renv::snapshot()` will record any changes into the lockfile.
5.	Calling `renv::status()` should now confirm everything's synced. 
6.	Commit the changes to version control.

#### Using a project that has already had [{renv}](https://rstudio.github.io/renv/) initialised (e.g., when collaborating on a colleague's project):
1.	Ensure the project is synced with the latest version-controlled repository (e.g., `git pull` from github).
2.	Call `renv::restore()` to make sure your local version of the project has all the required packages.
3.	Calling `renv::status()` should now confirm everything's synced. 

## More detail about what [{renv}](https://rstudio.github.io/renv/) does

[{renv}](https://rstudio.github.io/renv/) works by storing the exact versions of each package used within each project. This helps to isolate the project from any external changes that might have caused problems (e.g., updating/removing packages when working on a different project). Once [{renv}](https://rstudio.github.io/renv/) is initialised in a project it stays on unless deliberately turned off (see [Introduction to renv](https://rstudio.github.io/renv/articles/renv.html)). 

When you initialise [{renv}](https://rstudio.github.io/renv/) in a project (renv::init()) it searches the scripts for any calls to `library()` or `require()` and identifies which versions of each package are in use. The following files/folders are then added to the project:
* The folder `renv/library`: this is used for storing the packages. If the project is version-controlled using git a `.gitignore` file will be written to `renv/`, so that this library is ignored when changes to the project are committed.  
* The lockfile `renv.lock`: this stores the details of the packages (including the versions used). 
* The profile file `.Rprofile`: this is run automatically when the project is opened, to ensure it uses the packages stored in renv/library.

Caution: the packages stored in renv/library and detailed in the lockfile are frozen in time and won't benefit from bug fixes. To update to the latest versions of packages call `renv::update()` periodically, and make sure the code still works before recording the new versions in the lockfile using `renv::snapshot()`. If the code doesn’t work with the new versions you can roll back to the versions in the lockfile using `renv::restore()` (for more info see [Introduction to renv](https://rstudio.github.io/renv/articles/renv.html)). 

## Resources

* [Introduction to renv](https://rstudio.github.io/renv/articles/renv.html)
* [Posit workshop for PHS on renv](https://positpbc.zoom.us/rec/play/n8-spO05R8p9vp8dqJ9GxH_Zr8mk7IMvsiX3menvnbXEXmJOXK5mOA-HPMxEFQPJvh6bTkvhaK6_oHWT.e--Z8hkQVR5coU-F?continueMode=true&pwd=MjxDT7xc_SQJM8HkKz4ffvPvm0mU4s74&_x_zm_rtaid=7GmfdwjkRvidhayMImvvYQ.1680787485091.7d8be92495688fceb3b55c4b0f603018&_x_zm_rhtaid=747)
* [PHS Reproducible Environments channel on MS Teams](https://teams.microsoft.com/l/channel/19%3Aa786ffd4a70d4941b87f023942d21b6a%40thread.tacv2/Reproducible%20Environments?groupId=ec4250f9-b70a-4f32-9372-a232ccb4f713&tenantId=)
