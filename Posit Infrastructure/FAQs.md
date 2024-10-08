# Posit Infrastructure - Frequently Asked Questions

## Purpose

This document aims to answer frequently asked questions from users in relation to the use of Posit Team applications. This is split into the 3 Posit applications:
* [Posit Workbench](#posit-workbench)
* [Posit Package Manager](#posit-package-manager)
* [Posit Connect](#posit-connect)

## Posit Workbench

* [Accessing Posit Workbench](#accessing-posit-workbench)
  * [What web browser should I use?](#what-web-browser-should-i-use-for-posit-workbench)
  * [Do I need to be connected to the VPN?](#do-i-need-to-be-connected-to-the-vpn)
  * [How do I prevent my browser from causing my session to go to sleep?](#how-do-I-prevent-my-browser-from-causing-my-session-to-go-to-sleep)
* [Sessions](#sessions)
  * [How do I find my session ID?](#how-do-i-find-my-session-id)
  * [Why do I get Status code 502/504 errors when starting a session and what can I do about it?](#sessions-502-504)
* [Installing Packages](#installing-packages)
  * [What do I do if I cannot install any packages?](#what-do-i-do-if-i-cannot-install-any-packages)
  * [How do I install the `{hablar}` package?](#how-do-i-install-the-hablar-package)
  * [How do I install the `{ranger}` package?](#how-do-i-install-the-ranger-package)
  * [What do I do if a package requires `{rJava}`?](#what-do-i-do-if-a-package-requires-rjava)
  * [What should I do if I encounter a 'failed to lock directory' error?](#what-should-i-do-if-i-encounter-a-failed-to-lock-directory-error)
  * [Why can't I install the `{xlsx}` package in Posit Workbench?](#why-cant-i-install-the-xlsx-package-in-posit-workbench)
  * [Why does the `{rmapshaper}` package not install?](#why-does-the-rmapshaper-package-not-install)
* [Projects](#projects)
  * [What is a project (in Posit Workbench)?](#what-is-a-project-in-posit-workbench)
  * [How do I open or switch to another project?](#how-do-i-open-or-switch-to-another-project)
* [Accessing files and databases](#accessing-files-and-databases)
  * [Can a folder on the stats area be accessed from the server?](#can-a-folder-on-the-stats-area-be-accessed-from-the-server)
  * [Why can't I access any databases?](#why-cant-i-access-any-databases) 
* [Scheduling tasks](#scheduling-tasks)
  * [How can I schedule R scripts with cron in Posit Workbench?](#how-can-i-schedule-r-scripts-with-cron-in-posit-workbench)
* [Troubleshooting packages](#troubleshooting-packages)
  * [How do I stop `{shiny}` apps timing out so quickly?](#how-do-i-stop-shiny-apps-timing-out-so-quickly)

### Accessing Posit Workbench

#### What web browser should I use for Posit Workbench?

Microsoft Edge is the recommended, and supported, web browser for accessing Posit Workbench.

#### Do I need to be connected to the VPN?

If you are working remotely, yes: ensure that when you login to Windows that you first connect to the VPN by selecting "vpn1.nss.scot" or "vpn2.nss.scot".  If these VPN servers are not available to you, please raise a call to have this rectified in [ServiceNow](https://nhsnss.service-now.com/phs/).

#### How do I prevent my browser from causing my session to go to sleep?

Microsoft Edge puts your tabs to sleep when you're not using them. Tabs are put to sleep after 1 hour of inactivity by default. This can cause your session to pause / go to sleep.

1.  Open Microsoft Edge.
2.  Click/tap on the Settings and more (3 dots) button, and click/tap on Settings.
3.  Click/tap on System and performance in the left pane.
4.  Click/tap on the "Add" button under Never put these sites to sleep. Add the Posit Workbench homepage URL  (https://pwb.publichealthscotland.org/) to the dialogue box that appears then click the "Add" button.

### Sessions

#### How do I find my session ID?

##### Background

When a Posit Workbench session is requested by the user, it is assigned a session ID. This is a long string of letters and numbers that uniquely identifies the session. The session ID corresponds to metrics and logs that are produced by the Posit Workbench application and collected for onward analysis and debugging of issues.

##### Steps to find out the session ID of your Posit Workbench session

1. If you have not already done so, log into Posit Workbench and start a session (refer to the [guidance on the Knowledge base here](https://public-health-scotland.github.io/knowledge-base/docs/Posit%20Infrastructure?doc=How%20to%20Access%20Posit%20Workbench.md#logging-in) if necessary).

2. After the session has started, navigate to the [Posit Workbench homepage](https://pwb.publichealthscotland.org) and identify the session for which you would like to obtain the session ID in the list of sessions, as circled in red below:
<img width="434" alt="image" src="https://github.com/Public-Health-Scotland/technical-docs/assets/45657289/9496f0a2-1eb2-4466-bf35-5d56e2088f1f">

3. Click the "Info" button of the session (highlighted in yellow above) to bring up a dialog box containing further information about the session:
<img width="517" alt="image" src="https://github.com/Public-Health-Scotland/technical-docs/assets/45657289/6fa50075-7552-4cc0-a9e1-3aa8f0eaca2f">

4. Click on "Launcher Diagnostics" (highlighted in yellow above) to view a tab with further details:
<img width="515" alt="image" src="https://github.com/Public-Health-Scotland/technical-docs/assets/45657289/c4e2839a-ed4d-413b-9a16-204b994a7947">

5. The session ID of the session is highlighted in yellow above - it is a long string of letters and numbers.

6. To close the dialog box, click the "Close" button, circled in red above.

##### Alternative method

The session ID can also be found in the URL (i.e. web address) when a session is open. This method can be useful to capture the session ID of a session that has crashed or failed to launch successfully. In the address bar of your web browser, you will see a URL like the one below:

```
https://pwb.publichealthscotland.org/s/bd664cfc78a31605322d7/?launcher=1
```

The long string of letters and numbers (in this case <code>bd664cfc78a31605322d7</code>) is the session ID.

#### <a name="sessions-502-504">Why do I get _Status code 502/504_ errors when starting a session and what can I do about it?</a>

_Status code 502/504_ errors are produced when the Posit Workbench application is unable to connect to your RStudio IDE session.  This will most often happen when you are starting a session, especially when you have requested a large session as these take longer to start.

Posit Workbench will report a _Status code 502/504_ error after 2 minutes of not being able to connect to your session:

![Dialog box containing the text Status code 504 returned by RStudio Server when executing 'client_init'](https://github.com/Public-Health-Scotland/technical-docs/assets/45657289/91e22863-31eb-4920-8c2d-f398ea2dcc67)

After you click the "OK" button in the dialog box, the page in your web browser will likely turn grey, rather than connect to your session.  To resolve this, click the refresh button in your web browser.  This will reload the Posit Workbench application in your web browser.  If your session has successfully started, you should at this point be presented with the RStudio IDE as normal.  If your session is still starting, you will be presented with messages saying that the session is starting up.

If clicking the refresh button in your web browser had no effect, return to the Posit Workbench homepage by navigating to the URL [https://pwb.publichealthscotland.org/](https://pwb.publichealthscotland.org/).

### Installing Packages

#### What do I do if I cannot install any packages?

If you cannot install any packages **and** have an error message saying your home directory is not writeable or the directory is not correctly mounted then you should raise a call in [Service Now](https://nhsnss.service-now.com/phs/) and ask to have your cache cleared. Only raise a service call if you are getting these error messages.

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

#### What should I do if I encounter a 'failed to lock directory' error?

If you are trying to install an R package and see an error message in the console regarding locked directories (e.g. something like `00LOCK` or `failed to lock directory`), try using the `--no-lock` option with `install.packages()` as follows:

```R
install.packages("<pkg>", INSTALL_opts = "--no-lock")
```

#### Why can't I install the `{xlsx}` package in Posit Workbench?

This package relies on Java, which is not supported in Posit Workbench (please see [the FAQ above](https://github.com/Public-Health-Scotland/technical-docs/blob/main/Posit%20Infrastructure/FAQs.md#what-do-i-do-if-a-package-requires-rjava)). The `{openxlsx}` package is an excellent alternative. 

#### Why does the `{rmapshaper}` package not install?

`{rmapshaper}` has the dependencies `{V8}` and `{geojsonio}`, neither of which can be installed successfully on the CentOS 7 container image that Posit Workbench runs in. As these dependencies cannot be installed, {rmapshaper} also fails to install. As it stands, there is no immediate solution to resolve this.

### Projects

#### What is a project (in Posit Workbench)?

Projects in Posit Workbench allow you to divide your work into different working directories, each with their own workspace, history, and source code files.  A project directory will, as a minimum, contain a single file with a .Rproj extension.  This file will often have the same name as the parent directory.  It's this .Rproj file that tells Posit Workbench that this directory and all of its contents belong to a single project.

#### How do I open or switch to another project?

Posit Workbench provides several ways to open or switch to another project, but there is one way that tends to produce fewer errors.  Please ensure that you always follow these steps to open a project:

1. Open a "project opener" session with 0.2 CPU and 200 MB:  
   ![](https://user-images.githubusercontent.com/46680486/279127344-10a70bdc-963c-48f2-b83f-e10e95fe9a13.png)
   
   These sessions are small because no data processing is supposed to be done on them. Having a small session helps to save resources as Posit Workbench works on a pay-as-you-go policy.

2. After agreeing to the Usage Policy, click on the open new session icon ![](https://user-images.githubusercontent.com/46680486/279127331-4967eda2-f52a-4acd-a04b-5adf6e1e6b92.png) in the top right corner:  
   ![](https://user-images.githubusercontent.com/46680486/279127337-94f82693-97d0-492d-b4ca-12c4bf4a44a5.png)

3. In the pop-up window, select "Start within: Project", and click on the "Browse..." button:  
   ![](https://user-images.githubusercontent.com/46680486/279127346-705fc95b-1f32-4b5c-84ce-bcc2fe9073ab.png)

4. Navigate to your project folder and double-click on the `.Rproj` file:  
   ![](https://user-images.githubusercontent.com/46680486/279127342-b78bf898-5950-419c-834d-3b02799e6c2e.png)

5. Input the CPU and Memory according to your project requirements (please refer to the [Knowledge Base guidance here](https://public-health-scotland.github.io/knowledge-base/docs/Posit%20Infrastructure?doc=How%20to%20Use%20RStudio%20for%20Measuring%20Your%20Memory%20Usage.md)), and click on "Start":  
   ![](https://user-images.githubusercontent.com/46680486/279127341-8212b1ce-b297-44d9-ab33-fa2bd838b09c.png)
   
   To use the default CPU and memory resources, you can erase the text on these input boxes.

6. The new session will be open in a new tab. Wait until the new session has successfully opened your project. Then **do not forget** to come back to the previous tab to close the "project opener" session if you do not intend to use it anymore.

This procedure for opening projects should save time in case errors are raised when opening projects because your "project opener" session does not close automatically when opening the new project. However, if you forget to close that session, once the project is successfully open, we will be spending money on idle sessions.

!!! IMPORTANT !!!

**If you get a 502 or 504 error**, do not close that window. Please refer to [Why do I get Status code 502/504 errors when starting a session and what can I do about it?](#sessions-502-504)

!!! FURTHERMORE !!!

Please do not attempt to switch to another project using the 'Project' drop down menu at the top-right of the Posit Workbench interface:

![Project dropdown menu in RStudio](https://user-images.githubusercontent.com/45657289/215759371-64028dc2-a02e-4779-91c9-6bacf1369244.png)

Similarly, using the option File  > Recent Projects drop down from the main menu at the top-left of the Posit Workbench interface:

![File recent projects from the main menu in Posit Workbench](https://github.com/Public-Health-Scotland/technical-docs/assets/109799428/c644de6f-0b09-4d07-a53b-b71f714679f5)

Doing so may result in Posit Workbench crashing or certain error messages such as:

![Launch session error](https://user-images.githubusercontent.com/45657289/215759609-fa3ecbd3-36fc-4985-8abe-bd05af07bba4.png)

This is a [known issue](https://github.com/rstudio/rstudio/issues/11914) in older versions of Posit Workbench which will likely be fixed when the Posit Workbench environment is next updated.

### Accessing files and databases

#### Can a folder on the stats area be accessed from the server?

All folders on the "stats" or "confidential" area can potentially be mapped so the server can see them. If you cannot see the particular folder that you want, raise a call in [Service Now](https://nhsnss.service-now.com/phs/) to have this done.

#### Why can't I access any databases?

If you can't access any databases from Posit Workbench, you should work through the following troubleshooting steps in the first instance:

1. **Ensure that you have the appropriate access to the databases you require:** For new access to SMRA analysis views, please e-mail [phs.dmt@phs.scot](mailto:phs.dmt@phs.scot) specifying the required dataset(s).
   Please copy in your line manager to the e-mail to show that they have authorised your request. You will receive an auto-generated e-mail 30 days prior to the expiry date of any SMRA access. Upon receipt of this
   e-mail, please agree with your line manager that access should be renewed, then forward the notification e-mail to one of the PHS administrators named; copy in your line manager to show the request is authorised.

2. **Check your version of the `{odbc}` package:** A bug was previously reported in v1.4.0 of the `{odbc}` package that prevented users from accessing databases. If you have this package version installed, please
   upgrade to v1.4.1. If you do not yet have the `{odbc}` package installed, you will need this to access SMRA views from Posit Workbench.

If you have all appropriate access permissions in place and have worked through the steps above, please raise a call in [Service Now](https://nhsnss.service-now.com/phs/) to have this investigated further. 

### Scheduling tasks

#### How can I schedule R scripts with cron in Posit Workbench?

Cron is not supported in the Posit Workbench environment. The Data Science team are currently testing an alternative scheduling solution, and in the future, Posit Connect will also provide scheduling functionality.

### Troubleshooting packages

#### How do I stop `{shiny}` apps timing out so quickly?

If your `{shiny}` apps are timing out after just a few seconds when run locally, you can add the workaround code below to the app's server.R script to prevent this:

```{r}
auto_invalidate <- reactiveTimer(10000)

observe({
    auto_invalidate()
    cat(".")})
```
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
