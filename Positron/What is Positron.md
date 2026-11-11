# What is Positron?

Positron is a data science Integrated development environment (IDE) built for Python and R, and it provides more streamlined deployment options and deeper integration with both R and Python environments. It will look familiar to both users of RStudio and Visual Studio Code, but it provides more interactive features for examining variables, datasets and plots.

It further allows users to work with tools such as Shiny and Quarto, and to publish work directly to Posit Connect and Posit Connect Cloud within the same application.

Compared to RStudio, the IDE is more customisable and more extensions are provided.

## Do I need to stop using RStudio?

**No. RStudio and Positron can be used alongside each other.**

You can choose whichever is most appropriate for the work you are doing.

-   Positron may be preferable if you regularly work across R and Python *in the same project*, want to run multiple R/Python sessions, or want greater customisation through extensions.

## Why might I use it instead of RStudio?

-   Easy access to multiple R versions and multiple concurrent R and Python interpreters.

-   Data science workflows in R and Python, both as 'first-class' languages.

-   Support for other languages beyond R and Python via built-in language intelligence or extensions.

-   Ability to install extensions that add new features, functionality and customisation to Positron.

-   An integrated Data Explorer for dataframes in your active sessions and for a variety of files types (CSV, Parquet, etc.).

## How much memory does Positron need in Posit Workbench?

Positron typically requires more memory than RStudio, particularly when using multiple interpreters or extensions. It is recommended to request a session with at least **4 GB** for a basic or simple project.

**Note** that you may have to request a different Kubernetes Profile that permits requesting a greater amount of memory for your sessions.  The form at https://forms.office.com/e/VEutAJ8p9Y allows you to submit a request for a change to your Posit Workbench Kubernetes Profile, or a request on behalf of someone else.

## Can I open projects created with RStudio, VS Code, or JupyterLab in Positron?

**Yes. Projects created in RStudio, VS Code, or JupyterLab can typically be opened** **and used in Positron.**

For the best compatibility, check the R or Python version and the project's package environment. For R projects, ensure the renv environment and package versions are compatible with the R version being used. For Python projects, an existing venv may need to be recreated when moving to a different Python version. This is particularly important when moving between different Posit Workbench versions.

## What replaces RStudio Projects?

**RStudio: Project → Positron: Workspace (Folder)**

Positron doesn't use .Rproj files. Instead, you open the project folder itself as a workspace. In Positron, a workspace is simply a folder opened in its own window and is used as the project's working directory, so it is important to open the correct project folder before running scripts. You can check your current working directory using getwd() in the R Console. Alternatively, use pwd in the terminal tab for a more general, language-independent check.

Existing .Rproj files can remain in the folder, particularly if you still use the project in RStudio.

Positron can also create and manage project-specific package environments using renv for R and venv for Python, with pip or the faster uv package manager for managing Python packages. To create a new workspace, go to New \> New Folder from Template, where you can select from folder types including Python, R, Jupyter and Empty.

## Do RStudio shortcuts still work?

**Many familiar RStudio shortcuts, including Ctrl + Enter, still work in Positron by default.** Helpfully, you can also now use Ctrl + Enter to run Python code chunks.

You can also enable a fuller set of RStudio-style shortcuts:

-   Open the Command Palette (Ctrl + Shift + P).
-   Search for 'Preferences: Open Settings (UI)'.
-   Go to the Remote tab in Settings
-   Search the settings for rstudioKeybindings.
-   Turn it on and reload Positron by typing 'Developer: Reload Window' in the Command Palette.

**NB.** If you change the default keyboard shortcuts then some of the suggested shortcuts in this guide will not work. In particular, reload window (Positron: Ctrl + Shift + 0. RStudio: Ctrl + Shift + F10) and go to terminal (Positron: Ctrl + `. RStudio: Ctrl + ').