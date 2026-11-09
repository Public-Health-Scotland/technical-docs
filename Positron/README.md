# Positron

This guide is intended as a quick reference for existing RStudio users
moving to Positron, showing where familiar RStudio features can be found
and highlighting some of the main differences between the two IDEs.

For a more in-depth guide and a hands-on Positron walkthrough, see
[Migrate to Positron from RStudio --
Positron](https://positron.posit.co/tutorial-migrate-from-rstudio)

## Key things to know before you start

-   **Projects are folders** - Positron opens folders directly, rather than relying on .Rproj files, like RStudio. In order to continue working with functions like `here::here()`, Positron uses environments or a `.here` file placed in the root directory.

-   **The Command Palette (Ctrl+Shift+P) is your friend** - many actions
    that have menu options in RStudio can also be found here.

-   Positron can open projects created in RStudio, Positron, VS Code, and JupyterLab. If you're using Posit Workbench, **some settings and tools can be shared between different IDEs**, such as saved credentials, installed packages, and GitHub SSH configuration.

![Positron interface highlighting Command Palette in the top centre of the window](images/clipboard-452278570.png)
