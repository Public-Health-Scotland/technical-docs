# How to Publish (Deploy) a Shiny App

At PHS, we currently use a server hosted on [shinyapps.io](http://shinyapps.io) to host Shiny apps. The server is located outside of the UK and hosted by Posit, which means that we can only host public-facing apps with no confidential data. If you have doubts about this for your app, you should contact the PHS Stats Gov (phs.statsgov@phs.scot) team to assess. 

> [!NOTE]
> There is work underway to provide a platform to host Shiny apps that use confidential data and allow for greater control over who and what can be viewed. This will use the Posit Connect software and is being managed by the Posit Programme.

## Deploying an App

Once you have an app that you want to deploy, you will need to get in touch with one of [PHS’ Shiny server administrators](#shiny-server-administrators). and they will send you the details needed to deploy on the server. The details shared should never be shared more widely, this includes committing to git.  

The process to upload an app is very straightforward and requires only to: 

1. Fill in this form for each app instance. As this is a shared service, we need to know which apps belong to PHS, so we can contact app authors if there are any changes on the shiny.io server, and to allow for organisational oversight of our published content.
    - As the shiny.io server is used by different public sector organisations we follow a naming convention to make things clearer, so your app will need to be named following this format: "phs-descriptive-name".
2. Run the "deploying_app" script you can find in the files section of this channel.

### Adding Authentication to Apps

It is possible to password-protect Shiny apps. To align with governance and data protection, the current agreement is that any protection should only be done only for a limited amount of time before publication for _testing_, _quality assurance_ and _pre-release access_ purposes. Password protection can be set up by the app author using the package `{shinymanager}`. The steps are: 

1. Add the package `{shinymanager}` to your global script.
   - e.g. `library(shinymanager)`
2. Add a function called [`secure_app()`](https://search.r-project.org/CRAN/refmans/shinymanager/html/secure-app.html) at the beginning of the ui script, this must encapsulate the UI.
   - e.g. `ui <- secure_app(...)`
3. Create a credentials dataframe and save as an RDS file.
   - e.g.
     ```
     dir.create("shiny_app/admin/")

     credentials_df <- data.frame(
         user = c("user1"),
         password = c("password1"),
         stringsAsFactors = FALSE)

     saveRDS(credentials_df, "shiny_app/admin/credentials.rds")
     ```
4. Add code to the server code to set up authentication.
   - e.g.
     ```
     # Import authentication credentials
     credentials <- readRDS("admin/credentials.rds")

     # Apply shinymanager authentication
     res_auth <- secure_server(check_credentials = check_credentials(credentials))
     ``` 
5. On publication day you then need to upload the app without the password protection.

> [!NOTE]
> Before deploying an app, check that it works locally and that everything the app needs is in the app folder as through the upload process this is all that is uploaded to the server and therefore accessible to the deployed version.
> All file paths need to be relative rather than absolute as well, as the app in the server won't have access to PHS' file structure.  

If something doesn’t work when your app is already on the server (but works locally) you can check the app logs using the command:  

`rsconnect::showLogs(appName = "<app name>")`

It is sometimes tricky to spot the issue but the admins or other Shiny users would be happy to help. 

When you have uploaded an app to the server you will have a stand-alone website, but if you want to embed it in the PHS site then you will need to speak with the publications team (phs.statspublications@phs.scot) to arrange it.  

### Shiny Server Administrators

[REDACTED]
