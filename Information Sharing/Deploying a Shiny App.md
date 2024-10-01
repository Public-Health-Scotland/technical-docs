# Deploying (Publishing) a Shiny App

At PHS, we currently use [shinyapps.io](http://shinyapps.io) to host Shiny apps. The server is located outside of the UK and hosted by Posit, which means that we can only host public-facing apps with no confidential data. If you have doubts about this for your app, you should contact the PHS Stats Gov [phs.statsgov@phs.scot](mailto:phs.statsgov@phs.scot) team to assess. General [dashboard development guidance](https://public-health-scotland.github.io/knowledge-base/docs/Information%20Sharing?doc=Dashboard%20development%20guidance.md) is available and should be followed when developing apps, prior to deployment.

> [!NOTE]
> There is work underway to provide a platform to host Shiny apps and another information products that may use confidential data and allow for greater control over who and what can be viewed. This will use the Posit Connect software and is being managed by the Posit Programme.

## General Guidance

There are some key points to consider before deploying an app:

* **Data**: Ensure that the data used in the app is not confidential and can be shared publicly. If you are unsure, contact the [PHS Stats Gov team](mailto:phs.statsgov@phs.scot).
* **Accessibility**: Ensure that the app is accessible to all users.
* **Testing**: Test the app locally before deploying it to the server, considering user experience and functionality, performance, and security.

Shiny apps should also be deployed with the following considerations in mind:

* Each app should have a specific purpose and be updated over time. This means that deployments should be minimised, with most apps requiring only 1 or 2 versions: a live version and a PRA version where required (some using a test version for limited periods).
* Follow naming conventions for apps, which should be named following the format `phs-descriptive-name`, noting the `phs-` prefix.
  * PRA versions should have a `-pra` suffix added, e.g. `phs-descriptive-name-pra`.
  * Test versions should have a `-test` suffix added, e.g. `phs-descriptive-name-test`.
  * This name is what will be noted in the URL for the app, e.g. `scotland.shinyapps.io/phs-descriptive-name`, it doesn't need to be the same as the app title, directory or .RProj file.
* PRA deployments should:
  * Be password-protected using `{shinymanager}`.
  * Have a disclaimer on the app with details of the purpose.
  * Have limited access to only those who need to see the app.
* Test deployments should include all restrictions as with PRA versions, but also:
  * Use only dummy or anonymised data.
* Live deployments should never have password protection and be updated (not deploying a separate app) as per the publication timetable or as required.

## Deploying a Shiny App

The process to deploy an app uses the `{rsconnect}` package, with the process outlined below:

1. Complete [this form](https://forms.office.com/e/shBeTxkvBD) for each new app to be deployed.
   _As shinyapps.io is a shared service, we need to know which apps belong to PHS. This allows organisational oversight of published content and clear contacts with app authors if there are any changes on the server._
   This will also send an automated message containing the deployment authentication details. These are general purpose and can be used for multiple deployments.
   > [!WARNING]
   > The details should be kept secure and not shared more widely, this includes committing to git.
2. Connect to the shinyapps.io server using the credentials from the previous step (this should only need to be done once):
   ```
   rsconnect::setAccountInfo(
      name = "scotland",
      token = "REDACTED",
      secret = "REDACTED"
      )
   ```
3. Deploy the app:
   ```
   rsconnect::deployApp(
      appDir = "path/to/app",
      appName = "phs-descriptive-name"
      )
   ```

### Adding Authentication to Apps

It is possible to password-protect Shiny apps. To align with governance and data protection, the current agreement is that any protection should only be done only for a limited amount of time before publication for _testing_, _quality assurance_ and _pre-release access_ purposes. Password protection can be set up by the app author using the package `{shinymanager}`. The steps are:

1. Add the package `{shinymanager}` to your global script.
   * e.g. `library(shinymanager)`
2. Add a function called [`secure_app()`](https://search.r-project.org/CRAN/refmans/shinymanager/html/secure-app.html) at the beginning of the ui script, this must encapsulate the UI.
   * e.g. `ui <- secure_app(...)`
3. Create a credentials dataframe and save as an RDS file.
   * e.g.
   ```
   dir.create("shiny_app/admin/")

   credentials_df <- data.frame(
      user = c("user1"),
      password = c("password1"),
      stringsAsFactors = FALSE
      )

   saveRDS(credentials_df, "shiny_app/admin/credentials.rds")
   ```
4. Add code to the server code to set up authentication.
   * e.g.
   ```
   # Import authentication credentials
   credentials <- readRDS("admin/credentials.rds")

   # Apply shinymanager authentication
   res_auth <- secure_server(check_credentials = check_credentials(credentials))
   ``` 
5. On publication day you then need to deploy the live app version, without the password protection.

> [!NOTE]
> Before deploying an app, check that it works locally and all data and other files are stored with the app or accessible to the general internet. Once deployed the app will be a stand-alone website and won't have access to PHS' systems and file structure.
> Similarly, all file paths need to be relative rather than absolute as well, as the app in the server won't have access to PHS' file structure.

If something doesn’t work when your app is already on the server (but works locally) you can check the app logs using the command:  

`rsconnect::showLogs(appName = "<app name>")`

It is sometimes tricky to spot the issue but other Shiny users across are very supportive, and there are a couple of Shiny Server Administrators who can check the server side for more details. To get help, you can post a message on the R Shiny channel on the Data & Intelligence Forum, tagging `@shinyadmin` to get the attention of the Shiny admins.

When you have uploaded an app to the server you will have a stand-alone website, but if you want to embed it in the PHS site then you will need to speak with the publications team (phs.statspublications@phs.scot) to arrange it.  
