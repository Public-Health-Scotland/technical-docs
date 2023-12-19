# Posit Workbench - Frequently Asked Questions

## Purpose

This document aims to answer frequently asked questions from users in relation to the use of Posit Team applications. This is split into the 3 Posit applications:
* [Posit Workbench](#posit-workbench)
* [Posit Package Manager](#posit-package-manager)
* [Posit Connect](#posit-connect)

## Posit Workbench

* [Accessing Posit Workbench](#accessing-posit-workbench)
  * [What web browser should I use?](#what-web-browser-should-i-use-for-posit-workbench)
  * [Do I need to be connected to the VPN?](#do-i-need-to-be-connected-to-the-vpn)
* [Installing Packages](#installing-packages)
  * [How do I install the `{hablar}` package?](#how-do-i-install-the-hablar-package)
  * [How do I install the `{phsmethods}` package?](#how-do-i-install-the-phsmethods-package)
  * [How do I install the `{ranger}` package?](#how-do-i-install-the-ranger-package)
  * [What do I do if a package requires `{rJava}`?](#what-do-i-do-if-a-package-requires-rjava)
  * [Why does the `{rmapshaper}` package not install?](#why-does-the-rmapshaper-package-not-install)
* [Projects](#projects)
  * [What is a project (in Posit Workbench)?](#what-is-a-project-in-posit-workbench)
  * [How do I open or switch to another project?](#how-do-i-open-or-switch-to-another-project)
* [Troubleshooting packages](#troubleshooting-packages)
  * [How do I stop `{shiny}` apps timing out so quickly?](#how-do-i-stop-shiny-apps-timing-out-so-quickly)

### Accessing Posit Workbench

#### What web browser should I use for Posit Workbench?

Microsoft Edge is the recommended, and supported, web browser for accessing Posit Workbench.

#### Do I need to be connected to the VPN?

If you are working remotely, yes: ensure that when you login to Windows that you first connect to the VPN by selecting "vpn1.nss.scot" or "vpn2.nss.scot".  If these VPN servers are not available to you, please raise a call to have this rectified in [ServiceNow](https://nhsnss.service-now.com/phs/).

### Installing Packages

#### How do I install the `{hablar}` package?

The `{hablar}` package cannot be installed as a pre-compiled binary; attempting this gives an error.  Therefore, you need to force R to install the source version by specifying the URL for the source version of packages on Package Manager.  However, `{hablar}`'s dependencies can be installed as binaries first.

```{r}
# Get a list of dependencies and imports for {hablar}
available_pkgs <- available.packages()

deps <- tools::package_dependencies(
  packages = available_pkgs["hablar", "Package"],
  recursive = TRUE)[[1]]

# Install these dependencies as binaries
install.packages(
  pkgs = deps,
  repos = c(
    "https://ppm.publichealthscotland.org/all-r/__linux__/centos7/latest"))

# Compile and install the {hablar} package from source
install.packages(
  pkgs = "hablar",
  repos = c("https://ppm.publichealthscotland.org/all-r/latest"))

# Test if {hablar} can be loaded
library(hablar)
```

#### How do I install the `{phsmethods}` package?

The `{phsmethods}` package has a dependency on the `{gdata}` package.  The `{gdata}` package cannot be installed as a pre-compiled binary; attempting this gives an error.  Therefore, you need to force R to install the source version by specifying the URL for the source version of packages on Package Manager: 

```{r}
install.packages("gdata", repos = c("https://ppm.publichealthscotland.org/phs-cran/latest"))
```

You can then install the `{phsmethods}` package and all of its other dependencies as follows:

```{r}
install.packages("phsmethods")
```

#### How do I install the `{ranger}` package?

The default configurations in R do not allow the `{ranger}` package to compile and install successfully.  The developers of the `{ranger}` package switched the project to using C++14 in version 0.14.2 of the package.  R itself should default to C++14 from version 4.1.0 onwards (we have 4.1.2), unless the package specifies C++11.  It turns out the makevars for `{ranger}` specify C++11, even though it's meant to be compiled with C++14.  The fix is to add the line

```
CXX = g++ -std=gnu++14
```

to the file `~/.R/Makevars` which then overrides the C++11 that `{ranger}` specifies.

After amending the file as described above, you can install the `{ranger}` package as you would normally i.e.

```R
install.packages("ranger")
```

#### What do I do if a package requires `{rJava}`?

Some packages, e.g. `{xlsx}`, `{XLconnect}`, depend on an installation of [Java](https://en.wikipedia.org/wiki/Java_(software_platform)) in order to work.  There are no current or future plans to support Java on Posit Workbench.  Alternative packages such as `{openxlsx}` that do not rely on Java should be used instead.


#### Why does the `{rmapshaper}` package not install?

`{rmapshaper}` has the dependencies `{V8}` and `{geojsonio}`, neither of which can be installed successfully on the CentOS 7 container image that Posit Workbench runs in. As these dependencies cannot be installed, {rmapshaper} also fails to install. As it stands, there is no immediate solution to resolve this.

### Projects

#### What is a project (in Posit Workbench)?

Projects in Posit Workbench allow you to divide your work into different working directories, each with their own workspace, history, and source code files.  A project directory will, as a minimum, contain a single file with a .Rproj extension.  This file will often have the same name as the parent directory.  It's this .Rproj file that tells Posit Workbench that this directory and all of its contents belong to a single project.

#### How do I open or switch to another project?

Posit Workbench provides several ways to open or switch to another project, but there is one way that tends to produce fewer errors.  Please ensure that you always follow these steps to open a project:

1. Open a "project opener" session — 0.2 CPU and 200 MB:  
   ![](https://user-images.githubusercontent.com/46680486/279127344-10a70bdc-963c-48f2-b83f-e10e95fe9a13.png)
   
   These sessions are small because no data processing is supposed to be done on them. Having a small session helps to save resources as Posit Workbench works on a pay-as-you-go policy.

2. After agreeing to the Usage Policy, click on the open new session icon ![](https://user-images.githubusercontent.com/46680486/279127331-4967eda2-f52a-4acd-a04b-5adf6e1e6b92.png) in the top right corner:  
   ![](https://user-images.githubusercontent.com/46680486/279127337-94f82693-97d0-492d-b4ca-12c4bf4a44a5.png)

3. In the pop-up window, select "Start within: ⦿ Project", and click on the "Browse..." button:  
   ![](https://user-images.githubusercontent.com/46680486/279127346-705fc95b-1f32-4b5c-84ce-bcc2fe9073ab.png)

4. Navigate to your project folder and double-click on the `.Rproj` file:  
   ![](https://user-images.githubusercontent.com/46680486/279127342-b78bf898-5950-419c-834d-3b02799e6c2e.png)

5. Input the CPU and Memory according to your [project requirements]([PHS Data Science - Knowledge Base (public-health-scotland.github.io)](https://public-health-scotland.github.io/knowledge-base/docs/Posit%20Infrastructure?doc=How%20to%20Use%20RStudio%20for%20Measuring%20Your%20Memory%20Usage.md)), and click on "Start":  
   ![](https://user-images.githubusercontent.com/46680486/279127341-8212b1ce-b297-44d9-ab33-fa2bd838b09c.png)
   
   To use the default CPU and memory resources, you can erase the text on these input boxes.

6. The new session will be open in a new tab. Wait until the new session has successfully opened your project. Then **do not forget** to come back to the previous tab to close the "project opener" session if you do not intend to use it anymore.

This procedure for opening projects should save time in case errors are raised when opening projects because your "project opener" session does not close automatically when opening the new project. However, if you forget to close that session, once the project is successfully open, we will be spending money on idle sessions.

!!! IMPORTANT !!!

Please do not attempt to switch to another project using the 'Project' drop down menu at the top-right of the Posit Workbench interface:

![Project dropdown menu in RStudio](https://user-images.githubusercontent.com/45657289/215759371-64028dc2-a02e-4779-91c9-6bacf1369244.png)

Similarly, using the option File  > Recent Projects drop down from the main menu at the top-left of the Posit Workbench interface:

![File recent projects from the main menu in Posit Workbench](https://github.com/Public-Health-Scotland/technical-docs/assets/109799428/c644de6f-0b09-4d07-a53b-b71f714679f5)

Doing so may result in Posit Workbench crashing or certain error messages such as:

![Launch session error](https://user-images.githubusercontent.com/45657289/215759609-fa3ecbd3-36fc-4985-8abe-bd05af07bba4.png)

This is a [known issue](https://github.com/rstudio/rstudio/issues/11914) in older versions of Posit Workbench which will likely be fixed when the Posit Workbench environment is next updated.

## Posit Package Manager

* [Accessing Posit Package Manager](#accessing-posit-package-manager)
  * [What web browser should I use?](#what-web-browser-should-i-use-for-posit-package-manager)

### Accessing Posit Package Manager

#### What web browser should I use for Posit Package Manager?

Microsoft Edge is the recommended, and supported, web browser for accessing Posit Package Manager.

## Posit Connect

* [Accessing Posit Connect](#accessing-posit-connect)
  * [What web browser should I use?](#what-web-browser-should-i-use-for-posit-connect)

### Accessing Posit Connect

#### What web browser should I use for Posit Connect?

Microsoft Edge is the recommended, and supported, web browser for accessing Posit Connect.

### Troubleshooting packages

#### How do I stop `{shiny}` apps timing out so quickly?

If your `{shiny}` apps are timing out after just a few seconds when run locally, you can add the workaround code below to the app's server.R script to prevent this:

```{r}{auto_invalidate <- reactiveTimer(10000)
  observe({
    auto_invalidate()
    cat(".")
  })
}```
