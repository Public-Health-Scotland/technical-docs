# Posit Environment Quick Start Guide

## 1. Overview

### Purpose
This Quick Start Guide provides essential information and step-by-step instructions to get you started with the Posit Environment on day one.  It is not a comprehensive guide; further documentation and guidance will continue to be added and updated on the [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/).

### Audience
This guide assumes some previous experience with the R programming language, the RStudio Integrated Development Environment (IDE), and perhaps an earlier version of Posit Workbench.

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
  - Ubuntu 24.04 LTS Noble Numbat
- **Applications and Versions**:
  - **Posit Workbench**: 2026.08.1+195.pro1, “Yellow Yarrow” (e0674ae6).
  - **Posit Package Manager**: v2026.08.0
  - **Posit Connect**: v2026.08.1
- **R and Python Versions**:
  - **R**: Default version is v4.6.1, with additional support for v4.5.3 and v4.4.3
  - **Python**: Default version is 3.14.7, with additional support for versions 3.13.14, 3.12.13 and 3.11.15
- **Supported IDEs**:
- RStudio Pro 2026.08.1 Build 195.pro1 with support for Quarto 1.10.18
  - Visual Studio Code 1.124.0
  - Positron Pro  2026.08.0 build 331

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

## 3. URLs for Posit Applications
- **Posit Workbench**: https://pwb-prod.publichealthscotland.org/
- **Posit Package Manager**: https://ppm-prod.publichealthscotland.org/
- **Posit Connect**: _Coming soon..._

## 4. Logging in and Starting a Session

Follow the link above to Posit Workbench environment and log in using your LDAP username and password.

The homepage in Posit Workbench has been redesigned with a focus on [project-based workflows](https://www.tidyverse.org/blog/2017/12/workflow-vs-script/):

![Screenshot of the new Posit Workbench homepage](https://github.com/user-attachments/assets/a7ce10d7-2486-4571-91d4-4044e2f8b9d6)


After logging in, the Posit Workbench home page contains two sections (tabs) for projects/sessions, and job management:

- Projects tab contains a table of projects and their sessions.
- Jobs tab contains a table of Workbench Jobs and/or Audited Jobs

On first requesting a new session, you are given a choice of the three available IDEs, including Positron Pro.  Note that the previously available functionality of Jupyter Notebook and JupyterLab has now been replaced by equivalent functionality in Positron Pro.

![Screenshot of new Posit Workbench IDEs](https://github.com/user-attachments/assets/806dce23-e2fd-4c0c-afd3-0e629184da8e)

As before, you need to enter the number of CPUs and Memory you need for your session.

![Screenshot of the new Posit Workbench session options](https://github.com/user-attachments/assets/ec1065c4-4a35-4521-856d-e58319dfa22b)

**Remember to select the minimum number of CPUs and amount of memory required for the work you intend to do.**  In most cases, you only require more than 1 CPU if you are knowingly going to be running code using multiple threads or parallel processing.  The amount of memory you require is primarily dependent on the size of the dataset you will be working with.  There is further guidance available on the PHS Data Science Knowledge Base at https://public-health-scotland.github.io/knowledge-base/docs/Posit%20Infrastructure?doc=Memory%20Usage%20in%20SMR01.md

**Important Note: normally sessions will take just a few seconds to start, but if the Kubernetes cluster needs to scale up to accommodate your session, it can take several minutes for your session to start.  This is normal and expected behaviour.**

Once you click the "Start Session" button, the session will be listed on the Posit Workbench homepage as "PENDING" during this process:

![RStudio Pro Session Pending](https://github.com/user-attachments/assets/f9d72a48-9e87-4462-be1c-ecde1416f70e)

If the "Auto-join" checkbox was ticked in the "New Session" dialog window, the session will automatically load in your browser.  Alternatively, once the session shows as "ACTIVE" on the Posit Workbench homepage, you can click the session to open it:

![RStudio Pro Session Active](https://github.com/user-attachments/assets/6265e78d-1715-4901-ad2f-efe8456b1536)

**Important Note: RStudio Pro sessions will default to R v4.6.1. If you need to use R v4.5.3, please select this in the dropdown at the top-right of the RStudio IDE interface.**

## 5. Configuring your RStudio Pro environment

### Global Options

- Once your RStudio Pro session has started, please ensure that you configure your settings as follows:
  - Access the RStudio Global Options menu by going to _Tools > Global Options..._
  - In the General menu, be sure that the settings match those in the screenshot below:

![Screenshot of Global Options dialog on the General tab](https://github.com/user-attachments/assets/0f9c74dc-2d69-41c4-8151-11795f5f8de2)

  - _Optional, but recommended:_ On the Appearance menu, change the editor font to "Cascadia Code", or any other font that you have installed that has support for ligatures.  These map multiple characters to single glyphs e.g. rendering "<-" as a single arrow glyph.

![Screenshot of the Global Options dialog on the Appearance tab with the Cascadia Code editor font selected](https://github.com/user-attachments/assets/ea6be994-02f9-41cc-b6f3-d929851c935c)

If the "Cascadia Code" font is not listed, this is because the font is not installed on your laptop.  You can download the font from Microsoft's GitHub repo at https://github.com/microsoft/cascadia-code?tab=readme-ov-file  The direct link to download the zip is https://github.com/microsoft/cascadia-code/releases/download/v2407.24/CascadiaCode-2407.24.zip

Unzip this file, then navigate to `CascadiaCode-2407.24 -> ttf`.  Right click on the file `CascadiaCode.ttf` and click `Install`.  This will install the font for your user only.  Administrative rights are not required to install the font.

Make sure to close all of your open RStudio sessions.  Next time you open an RStudio session, you will have the option to select the "Cascadia Code" font.

Other font suggestions that work well in RStudio that use ligatures are:

- [Fira Code](https://fonts.google.com/specimen/Fira+Code?query=fira+code)
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/)

### Installing Packages and recording installed packages
You will need to install the R packages that you need.  These will not transfer over from the old Posit environment.  **Before the upgrade**, you can run the following R code to write out a CSV file listing the packages you had installed.  This might be helpful for re-installing the packages you need:

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

R has been configured to install binary versions of packages by default from the PHS Posit Package Manager.  This significantly reduces the installation time for packages.

You can further speed up package installation time by requesting more than 1 CPU for your session and running the following code before installing your packages:

```r
install.packages("parallelly")
available_cores <- as.numeric(parallelly::availableCores())
options(Ncpus = available_cores)
Sys.setenv(MAKEFLAGS = paste("-j", as.character(available_cores), sep = ""))
```

This will force the R packages to install in parallel, if possible, and any packages that do not have a pre-compiled binary will have their source code compiled in parallel (i.e. faster).

On day one, if you need to install our PHS R packages (`{phsopendata}`, `{phstemplates}`, `{phsstyles}`, `{phsverse}` and `{slfhelper}`), you will have to install these directly from GitHub using `remotes::install_github()`. For example:

```r
remotes::install_github("Public-Health-Scotland/phsopendata")
remotes::install_github("Public-Health-Scotland/phsstyles")
```

Over the course of the next few weeks, the Data Science Team will be working with Jumping Rivers to set up the PHS Posit Package Manager with pre-built binaries for these packages.

Please note that `{phsmethods}` is available on CRAN and can be installed using `install.packages()`, just like most other packages.

### Restoring `{renv}` environments

It is likely that RStudio projects that use `{renv}` will open and restore successfully without making any changes, however you may have to select R v4.5.3 or v4.4.3 from within the RStudio Pro IDE if your project is incompatible with R v4.6.1.

## 6. Night Sessions

All sessions, both active and idle, will be automatically removed (or "killed") at **7.15pm** each day.

If you need your session to continue running beyond 7.15pm, you must include the word **NIGHT** at the start of your session's name e.g.

![Screenshot of Posit Workbench session name](https://github.com/user-attachments/assets/33595233-d9bc-4281-877b-a4e584c30a4e)

---
## 7. Configure Git and GitHub

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
## 8. Getting Support

The support process for the Posit Environment is as follows:

1. All requests for support and to report issues with the Posit Environment must be made via the form at https://forms.office.com/e/pqmmNMkhT6

These requests for support will first reach the Data Science Team, who will provide first-line support where possible.  If the Data Science Team cannot resolve the issue, it is passed to second-line support.

2. Second-line support for the Posit Environment will be provided by Jumping Rivers.  An Engineer or Data Scientist at Jumping Rivers may contact you directly about the issue you are experiencing.

3. NSS DaS will only become involved in exceptional circumstances, such as a network outage, or if a significant change is required in the Microsoft Azure cloud computing environment.  The Data Science Team will coordinate the communication between Jumping Rivers and NSS DaS in these instances.

**Important Notes**

- You must complete the form linked above to receive support relating to the Posit Environment.
- Do not contact Jumping Rivers, unless they request further information from you directly.
- Do not raise a request or incident in Halo, unless directed to do so by the Data Science Team.

---

## 9. FAQs
### What if I encounter a problem?
- Contact the Data Science Team for support using the form at <https://forms.office.com/e/pqmmNMkhT6>
### How can I get access to Posit Connect?
- Posit Connect has been deployed into the new Posit environment along with Posit Workbench and Posit Package Manager.  Work continues to further test the capabilities of Posit Connect and assess how we can best make use of this application in PHS.  If you would like to get involved in this testing, please contact Ross Elder at [Ross.Elder@phs.scot](mailto:Ross.Elder@phs.scot).

---

### Useful Links
- [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/)
- [PHS Data and Intelligence Forum](https://teams.microsoft.com/l/team/19%3Ae9f55a12b7d94ef49877ff455a07f035%40thread.tacv2/conversations?groupId=ec4250f9-b70a-4f32-9372-a232ccb4f713&tenantId=10efe0bd-a030-4bca-809c-b5e6745e499a)

---


