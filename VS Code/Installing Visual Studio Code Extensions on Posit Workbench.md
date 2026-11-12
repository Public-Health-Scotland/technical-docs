# Installing Visual Studio Code Extensions on Posit Workbench

## Overview

Since PHS upgraded the Posit environment in Spring 2025, users are able to launch
VS Code sessions from Posit Workbench. Extensions in VS Code are one of its biggest
strengths - adding support for different languages (e.g. R, Python, Julia), debugging
tools and version control integration.

However, the default method of installing extensions through the VS Code UI in
Posit Workbench does not work, despite extensive testing and investigation by both
PHS and Jumping Rivers. Here, we offer a workaround to this issue.

---

## Current Limitations

* The VS Code UI extension installer does not work in Posit Workbench
due to unresolved technical constraints.
 
* Microsoft's Terms of Service strictly forbid using their Marketplace extensions
with third-party tools like code-server - see [here](https://github.com/coder/code-server/blob/main/docs/FAQ.md#why-cant-code-server-use-microsofts-extension-marketplace)
for more information.

---

## Terminal-Based Workaround

Users can install extensions using the Terminal built into VS Code:

1. Upon launching a VS Code session from Posit Workbench, if the Terminal is not open,
press `Ctrl` + `'`. 

1. Search for the required extension on [open-vsx.org (the open source extensions repository for VSCode)](https://open-vsx.org/),
right-click on the Download button, and copy the URL. Users must source extensions
exclusively from here.

2. Paste this URL into the `URL` variable below.

3. Copy and paste the following into the Terminal in VS Code and press `Enter`:

```
URL=https://open-vsx.org/api/REditorSupport/r/2.8.4/file/REditorSupport.r-2.8.4.vsix
SAVE_LOCATION=/tmp/$(basename $URL)
curl $URL -L -o $SAVE_LOCATION
/usr/lib/rstudio-server/bin/pwb-code-server/bin/code-server  --install-extension $SAVE_LOCATION

```

### Additional Information

* Extensions will install to `$HOME/.vscode-server/extensions/` and persist across
sessions.

* The Open VSX Registry now hosts over 2,800 extensions, including extensions
that support the use of Python and R from within Visual Studio Code.

---

## Getting Support

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


### Useful Links
- [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/)
- [PHS Data and Intelligence Forum](https://teams.microsoft.com/l/team/19%3Ae9f55a12b7d94ef49877ff455a07f035%40thread.tacv2/conversations?groupId=ec4250f9-b70a-4f32-9372-a232ccb4f713&tenantId=10efe0bd-a030-4bca-809c-b5e6745e499a)

---
