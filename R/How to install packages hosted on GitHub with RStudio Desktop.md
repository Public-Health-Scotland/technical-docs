# How to install packages hosted on GitHub in RStudio Desktop

## Background
R has recently been upgraded to version 4.4.1 due to a security vulnerability, which has required a newer version of RStudio Desktop to be installed for users at Public Health Scotland. This newer version features slightly different configuration options to the older version it has replaced. While initial issues with installing R packages from CRAN have now been resolved, it is currently still necessary to use a workaround to install packages that are only hosted on GitHub. This process is described below.

## Prerequisites
This workaround assumes that you have access via your web browser to the public GitHub repository hosting the package you wish to install. You must already be using R 4.4.1 in the latest version of RStudio Desktop provided by NSS DaS with rtools44 installed (this should be included with the installation). The {devtools} package must also be installed from CRAN before working through these instructions.

## Instructions
These instructions use screenshots from the {RDCOMClient} package repository on GitHub to illustrate examples as this package is used by many teams at Public Health Scotland. In practice, all package repositories on GitHub will appear similar to this one. Work through the steps below to install a package from GitHub in RStudio Desktop.

#### 1. Find the repository on GitHub
In your web browser, navigate to the GitHub repository for the package you wish to install. Ensure that you are on the 'main' or 'master' branch for the most current version of the repository. The repository should look like the example below, although the names of folders may vary:

![image](https://github.com/user-attachments/assets/477c7bc5-ae7d-499d-bba1-8d3916deb28f)

No releases have been published for the {RDCOMClient} package used as an example here, so the 'master' branch will be used. However, if releases have been published for the package you wish to install, select the desired release under 'Tags' in the 'Switch branches/tags' dropdown menu:

![image](https://github.com/user-attachments/assets/ea5217ed-ef04-469c-a1a4-df7747ed6841)

#### 2. Download a zipped copy
Click on the green 'Code' button and select 'Download ZIP' as shown below:

![image](https://github.com/user-attachments/assets/acf08cf0-c3fd-47b1-a429-9fe13072f481)

#### 3. Extract all files
Open your local 'Downloads' folder in Windows Explorer. Right-click on the zipped folder and select 'Extract All' from the menu, then 'Extract' on the subsequent popout window. This will unzip the folder into 'Downloads'.

#### 4. Install the package in RStudio Desktop
Open RStudio Desktop and run the following code, replacing 'ldap_username' with your own LDAP username and 'folder_name' (2x) with the name of the unzipped folder in Downloads:

```devtools::install("C:/Users/ldap_username/Downloads/folder_name/folder_name")```

The package will then be installed to the R library, and a message in the console will confirm this. The zipped and unzipped folders in 'Downloads' can then be deleted. To update or reinstall the package at any point in the future, these steps will need to be repeated.
