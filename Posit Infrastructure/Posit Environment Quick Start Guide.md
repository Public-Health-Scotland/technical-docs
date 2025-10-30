# Posit Environment Quick Start Guide

## 1. Overview

### Purpose
This Quick Start Guide provides essential information and step-by-step instructions to get you started with the Posit Environment on day one.  It is not a comprehensive guide; further documentation and guidance will continue to be added and updated on the [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/).

### Audience
This guide assumes some previous experience with the R programming language, the RStudio Integrated Development Environment (IDE), and perhaps a earlier version of Posit Workbench.

### Scope
This guide covers:
- A high-level overview of the Posit Environment's specifications and features.
- Step-by-step instructions to get you started with logging in and setting up your environment.
- Details on how to get help.
- Links to other useful information and resources.

---

## 2. Environment Specifications

### Operating System and Application Specifications

- **Operating System**
  - Ubuntu 22.04.5 LTS Jammy Jellyfish
- **Applications and Versions**:
  - **Posit Workbench**: 2025.09.1+401.pro2, “Cucumberleaf Sunflower” (59cf440a).
  - **Posit Package Manager**: v2025.09.0-7
  - **Posit Connect**: _Coming soon..._
- **R and Python Versions**:
  - **R**: Default version is v4.5.1, with additional support for v4.4.2 
  - **Python**: Default version is 3.13.8, with additional support for versions 3.12.11 and 3.10.12
- **Supported IDEs**:
  - RStudio Pro 2025.09.1 Build 401.pro2 with support for Quarto 1.8.25
  - Jupyter Notebook 7.2.3
  - JupyterLab 4.2.7
  - Visual Studio Code 1.102.0
  - Positron Pro 2025.08.1 build 11 (for evaluation purposes only)

---

### Infrastructure Specification
- The environment is hosted on [Microsoft Azure](https://azure.microsoft.com/en-gb).
- Posit Workbench sessions are launched on a [Kubernetes cluster](https://www.vmware.com/topics/kubernetes-cluster)
- There are two node pools in the Kubernetes cluster (nodepool and bigpool) which have different types of Virtual Machine (VM):
  - nodepool (default): Standard_E20as_v5 with 20 vCPUs and 160GiB RAM - scales up to 48 nodes
  - bigpool (BIG): Standard_E32as_v5 with 32 vCPUs and 256GiB RAM - scales up to 6 nodes
- You will only have access to the "bigpool" if you are a member of the `positwb_super_user` UNIX group.  You can request access to this group by emailing the [Data Science Team](phs.datascience@phs.scot).  You will also need Line Manager authorisation.
- The Kubernetes container image is based on **Ubuntu 22.04.5 LTS (Jammy Jellyfish)**, providing better support for Posit Workbench, R, Python, and associated packages.
- A reduced-size version of TeX has been installed in the container image to decrease its size and reduce session startup times.

---

## 3. URLs for New Posit Applications
- **Posit Workbench**: https://pwb-prod.publichealthscotland.org/
- **Posit Package Manager**: https://ppm-prod.publichealthscotland.org/
- **Posit Connect**: _Coming soon..._

## 4. Logging in and Starting a Session

- Follow the link above to the new production Posit Workbench environment and log in using your LDAP username and password.  These are the same credentials you have used for the old Posit Workbench environment.
- The "New Session" dialog window has changed slightly.  On first requesting a new session, you are given a choice of the four available IDEs:

![New Session Dialog 1](https://github.com/user-attachments/assets/000c2943-bd4b-4818-974a-679dbb8987a9)

- As before, you need to enter the number of CPUs and Memory you need for your session.  **Important Change: you must specify the amount of memory you require in gigabytes (GB)**:

![New Session Dialog 2](https://github.com/user-attachments/assets/bd593345-4b9a-49a4-a4c4-f52008524438)


**Remember to select the minimum number of CPUs and amount of memory required for the work you intend to do.**  In most cases, you only require more than 1 CPU if you are knowingly going to be running code using multiple threads or parallel processing.  The amount of memory you require is primarily dependent on the size of the dataset you will be working with.  There is further guidance available on the PHS Data Science Knowledge Base at https://public-health-scotland.github.io/knowledge-base/docs/Posit%20Infrastructure?doc=Memory%20Usage%20in%20SMR01.md

- Once you click the "Start Session" button, a further dialog will appear in the bottom-right of your browser window giving you updates on the progress of starting the session:

![Starting Session Dialog](https://github.com/user-attachments/assets/2966723d-9b0a-42e2-99cb-9b6a8c1aa6e7)


**Important Note: normally sessions will take just a few seconds to start, but if the Kubernetes cluster needs to scale up to accommodate your session, it can take up to 10 minutes for your session to start.  This is normal and expected behaviour.**

- The session will be listed on the Posit Workbench homepage as "PENDING" during this process:

![RStudio Pro Session Pending](https://github.com/user-attachments/assets/0713f025-c984-4a46-9c48-bbbf2fb1ea35)

- If the "Join session when ready" checkbox was ticked in the "New Session" dialog window, the session will automatically load in your browser.  Alternatively, once the session shows as "ACTIVE" on the Posit Workbench homepage, you can click the session to open it:

![RStudio Pro Session Active](https://github.com/user-attachments/assets/e7e81280-e71b-4d5e-9742-4ca2650bb9b3)


## 5. Configuring your RStudio Pro environment

### Global Options

- Once your RStudio Pro session has started, please ensure that you configure your settings as follows:
  - Access the RStudio Global Options menu by going to _Tools > Global Options..._
  - In the General menu, be sure that the settings match those in the screenshot below:

![Global Options](https://github.com/user-attachments/assets/c1441dba-b6af-4bec-b017-cc371bd14091)

  - _Optional, but recommended:_ On the Appearance menu, change the editor font to "Cascadia Code".  This font has support for ligatures that map multiple characters to single glyphs e.g. rendering "<-" as a single arrow glyph.

![Cascadia Code](https://github.com/user-attachments/assets/591ad6c5-4fad-4c25-9142-4ae0df288428)

If the "Cascadia Code" font is not listed, this is because the font is not installed on your laptop.  You can download the font from Microsoft's GitHub repo at https://github.com/microsoft/cascadia-code?tab=readme-ov-file  The direct link to download the zip is https://github.com/microsoft/cascadia-code/releases/download/v2407.24/CascadiaCode-2407.24.zip

Unzip this file, then navigate to `CascadiaCode-2407.24 -> ttf`.  Right click on the file `CascadiaCode.ttf` and click `Install`.  This will install the font for your user only.  Administrative rights are not required to install the font.

Make sure to close all of your open RStudio sessions.  Next time you open an RStudio session, you will have the option to select the "Cascadia Code" font.

Other font suggestions that work well in RStudio that use ligatures are:

- [Fira Code](https://fonts.google.com/specimen/Fira+Code?query=fira+code)
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/)

### Installing Packages

- You will need to install the R packages that you need.  These will not transfer over from the old Posit environment.  In the old Posit environment, you can run the following R code to write out a CSV file listing the packages you had installed.  This might be helpful for re-installing the packages you need:

```r
# Function to check and install rstudioapi if necessary
install_rstudioapi <- function() {
  if (!requireNamespace("rstudioapi", quietly = TRUE)) {
    cat("The 'rstudioapi' package is not installed. Installing it now...\n")
    install.packages("rstudioapi", quiet = TRUE)
    if (!requireNamespace("rstudioapi", quietly = TRUE)) {
      stop("Failed to install 'rstudioapi'. Please install it manually.")
    }
    cat("'rstudioapi' package has been successfully installed.\n")
  }
}

# Install rstudioapi if not present
install_rstudioapi()

# Get all installed packages
all_packages <- installed.packages()

# Get base packages (those installed with R by default)
base_packages <- rownames(installed.packages(priority = "base"))

# Filter out base packages
user_packages <- all_packages[!rownames(all_packages) %in% base_packages, ]

# Create a data frame with package names and versions
package_info <- data.frame(
  Package = rownames(user_packages),
  Version = user_packages[, "Version"],
  stringsAsFactors = FALSE
)

# Prompt user to select save location
save_path <- rstudioapi::selectFile(
  caption = "Select location to save CSV file",
  label = "Save",
  existing = FALSE,
  filter = "CSV files (*.csv)"
)

# Check if a file was selected
if (!is.null(save_path)) {
  # Ensure the file has a .csv extension
  if (!grepl("\\.csv$", save_path, ignore.case = TRUE)) {
    save_path <- paste0(save_path, ".csv")
  }
  
  # Write the data frame to the selected CSV file
  write.csv(package_info, file = save_path, row.names = FALSE)
  
  # Print a message to confirm the file has been created
  cat("CSV file has been saved to:", save_path, "\n")
} else {
  cat("File save cancelled.\n")
}
```

- R (in both RStudio Pro and Visual Studio Code) has been configured to install binary versions of packages by default from the PHS Posit Package Manager.  This significantly reduces the installation time for packages.
- You can further speed up package installation time by requesting more than 1 CPU for your session and running the following code before installing your packages:

```r
install.packages("parallelly")
available_cores <- as.numeric(parallelly::availableCores())
options(Ncpus = available_cores)
Sys.setenv(MAKEFLAGS = paste("-j", as.character(available_cores), sep = ""))
```

This will force the R packages to install in parallel, if possible, and any packages that do not have a pre-compiled binary will have their source code compiled in parallel (i.e. faster).

- On day one, if you need to install our PHS R packages (`{phsopendata}`, `{phstemplates}`, `{phsstyles}`, `{phsverse}` and `{slfhelper}`), you will have to install these directly from GitHub using `remotes::install_github()`. For example:

```r
remotes::install_github("Public-Health-Scotland/phsopendata")
remotes::install_github("Public-Health-Scotland/phsstyles")
```

In a few weeks, the Data Science Team will set up the PHS Posit Package Manager with pre-built binaries for these packages. Please note that `{phsmethods}` is available on CRAN and can be installed using `install.packages()`, just like most other packages.

### Restoring `{renv}` environments

It is likely that RStudio projects that use `{renv}` will not restore successfully without making some changes first.  This is due to

- the URLs for Posit Package Manager have changed;
- many older versions of packages do not support R v4.4.2.

To update your `{renv}` project environment to work in the new Posit environment, please follow these steps:

1. In a new RStudio Pro session, install the latest version of the `{renv}` package by running the following R command on the console:

```{r}
install.packages("renv")
```

**IMPORTANT - take a note of the version of {renv} that was installed.  As at 10th April 2025, this is likely to be v1.1.4**

2. In the same RStudio Pro session, open your project's .Rprofile file and delete the line:

```{r}
source("renv/activate.R")
```

Save the file.

3. Then, open the project's `renv.lock` file and make the following changes:

- Update the version of R by changing the old version

```{json}
    "Version": "4.1.2",
```

to R version 4.4.2

```{json}
    "Version": "4.4.2",
```

- Update the list of repositories (where R packages are installed from) to point to the new Production Posit Package Manager:

```{json}
    "Repositories": [
      {
        "Name": "RSPM",
        "URL": "https://ppm.publichealthscotland.org/all-r/latest"
      }
    ]
```

to 

```{json}
    "Repositories": [
      {
        "Name": "CRAN",
        "URL": "https://ppm-prod.publichealthscotland.org/cran/__linux__/jammy/latest"
      }
    ]
```

- If you have any PHS R packages hosted on GitHub in the `{renv}` environment, then make sure to add a further repository to the list as follows:

```{json}
    "Repositories": [
      {
        "Name": "CRAN",
        "URL": "https://ppm-prod.publichealthscotland.org/cran/__linux__/jammy/latest"
      },
      {
        "Name": "PHSGITHUB",
        "URL": "https://ppm-prod.publichealthscotland.org/phs-github/latest"
      }
    ]
```

- Go through the rest of the renv.lock file and replace where it says "Repository": "RSPM" with "Repository": "CRAN". If the R package is a PHS R package (e.g. {phsstyles}) then replace "Repository": "RSPM" with "Repository": "PHSGITHUB".

Make sure to change the version to the version of `{renv}` you installed in step 1 above e.g.

```{json}
    "renv": {
      "Package": "renv",
      "Version": "1.1.4",
      "Source": "Repository",
      "Repository": "CRAN",
      "Requirements": [
        "utils"
      ],
      "Hash": "41b847654f567341725473431dd0d5ab"
    }
```
Note that the packages listed below have been found to cause issues. It may save you some time to go through the renv.lock file at this stage and change the versions for each package to the versions listed here (or newer):
```
lattice  - 0.22-6
MASS     - 7.3-61
Matrix   - 1.7-1
mgcv     - 1.9-1
nlme     - 3.1-166
jsonlite - 1.8.9
haven    - 2.5.4
```
4. Save and close all the open files, and the RStudio session.
5. Open a new RStudio Pro session
6. Open the RStudio project with the `{renv}` environment you want to restore.
7. On the R console, re-initialise the {renv} environment, but without installing any packages:

```{r}
renv::init(bare = TRUE)
```

8. Now you can restore the `{renv}` environment using the contents of the `renv.lock` file. To do this, run the following R command on the console:

```{r}
renv::restore()
```

All the R packages your project requires should be installed successfully without error. If not, move on to step 9 below:

9. It may be necessary to install the latest versions of all the packages listed in your `{renv}` environment's lockfile in order to successfully restore the environment.  Follow these steps to do so:

- With your `{renv}` project opened in an RStudio Pro session, get a list of all the required packages from your project's lockfile:

```{r}
lockfile <- renv::lockfile_read("renv.lock")
```

- Install the latest versions of the packages required:

```{r}
renv::install(names(lockfile$Packages))
```

This could take a while to complete...time for :coffee:

- Update the `{renv}` lockfile by snapshotting all packages installed in the project's library: 

```{r}
renv::snapshot(type = "all")
```

---

## 5. Night Sessions

**Important Change - please read carefully**

All sessions, both active and idle, will be automatically removed (or "killed") at **7.15pm** each day.

If you need your session to continue running beyond 7.15pm, you must include the word **NIGHT** at the start of your session's name e.g.

![New NIGHT Session Dialog](https://github.com/user-attachments/assets/bbdc6139-8b6e-4cbd-8697-507074e063a1)

### Automatically close an RStudio Pro session

If you want your script to end your RStudio Pro session automatically when it completes all of its tasks, then the following code snippet will reliably close the session, even if you have closed your web browser.  Be sure to include this at the end of your NIGHT session script so that it closes when it is complete.

```r
# Get the Process ID of the R session
ppid <- system(paste("ps -o ppid= -p", Sys.getpid()), intern = TRUE)
# Gracefully terminate the R session
system(paste("kill -15", ppid))
```

On the Posit Workbench homepage, the RStudio Pro session will report that the session is `Executing` whilst R code continues to run:

![NIGHT session executing](https://github.com/user-attachments/assets/b50c0dab-3950-4c83-9b8a-ea76f7faef43)

On completion, and once the session has closed successfully, the session will be reported as having `Finished`:

![NIGHT session finished](https://github.com/user-attachments/assets/0ef26b7f-cf91-4887-b43c-35691aff1cc0)

---
## 6. Configure Git and GitHub

The following is only relevant if you/your team use Git in your work (i.e. collaborative work using repositories hosted on Github):

### Configure Git

Add your name and email to Git by running the following commands in the terminal:

```
git config --global user.email <your email address>
git config --global user.name <Your full name>
```

### Create an SSH key
In the **Git/SVN** tab, hit *Create RSA Key* (A). 
In the window that appears, hit the *Create* button (B). 
Close this window.

Click, *View public key* (C), and copy the displayed public key (D).
![](https://github.com/SurgicalInformatics/healthyr_book/blob/8da2d63f5ac55e1734b2ca9afdc800d17c5401cb/images/chapter14/1.png)

### Add the SSH key to GitHub
On GitHub, log in, open the account settings page and go to the [SSH keys tab](https://github.com/settings/keys) (A). 
Click *Add SSH key* and paste the public key you copied from RStudio (B).

![](https://github.com/SurgicalInformatics/healthyr_book/blob/8da2d63f5ac55e1734b2ca9afdc800d17c5401cb/images/chapter14/2.png)

---
## 7. Getting Support

**Important Change - please read carefully**

There is a new support process for the new Posit environment as follows:

1. All requests for support and to report issues with the new Posit environment must be made via the form at https://forms.office.com/e/pqmmNMkhT6

These requests for support will first reach the Data Science Team, who will provide first-line support where possible.  If the Data Science Team cannot resolve the issue, it is passed to second-line support.

2. Second-line support for the new Posit environment will be provided by Jumping Rivers.  An Engineer or Data Scientist at Jumping Rivers may contact you directly about the issue you are experiencing.

3. NSS DaS will only become involved in exceptional circumstances, such as a network outage, or if a significant change is required in the Microsoft Azure cloud computing environment.  The Data Science Team will coordinate the communication between Jumping Rivers and NSS DaS in these instances.

**Important Notes**

- You must complete the form linked above to receive support relating to the new Posit environment.
- Do not contact Jumping Rivers, unless they request further information from you directly.
- Do not raise a request or incident in Service Now, unless directed to do so by the Data Science Team.

---

## 8. FAQs
### What if I encounter a problem?
- Contact the Data Science Team for support using the form at [https://forms.office.com/e/pqmmNMkhT6]
### How can I get access to Posit Connect?
- Posit Connect has been deployed into the new Posit environment along with Posit Workbench and Posit Package Manager.  Work continues to further test the capabilities of Posit Connect and assess how we can best make use of this application in PHS.  If you would like to get involved in this testing, please contact Ross Elder at [Ross.Elder@phs.scot](mailto:Ross.Elder@phs.scot).
### Where are all my files?
- Any files you had saved in your home directory on the old Posit environment will not be migrated to the new Posit environment.  The home directory should only be used for the installation of R and Python packages.  Anything else should be saved in an area on Stats.

---

### Useful Links
- [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/)
- [PHS Data and Intelligence Forum](https://teams.microsoft.com/l/team/19%3Ae9f55a12b7d94ef49877ff455a07f035%40thread.tacv2/conversations?groupId=ec4250f9-b70a-4f32-9372-a232ccb4f713&tenantId=10efe0bd-a030-4bca-809c-b5e6745e499a)

---


