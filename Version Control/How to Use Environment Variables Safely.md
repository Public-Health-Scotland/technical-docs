# How to Use Environment Variables Safely

## Purpose

This guide explains how to keep small pieces of sensitive information, such as API keys or passwords, out of code that is shared with git. It focuses on R projects, because R can read environment variables from a `.Renviron` file and retrieve them with `Sys.getenv()`.

Environment variables are useful when code can be shared but one or two values should stay private. They should not be used for patient-identifiable data or large confidential files.

## What environment variables are

An environment variable is a named value that is available to your R session. For example, instead of writing an API key directly in a script, you can store it outside the script:

```text
MY_API_KEY=replace-this-with-the-real-key
```

Your R code can then read the value when it runs:

```r
api_key <- Sys.getenv("MY_API_KEY")
```

The code can be committed and shared because it only contains the name of the environment variable, not the private value.

## When to use this approach

Use environment variables for small values such as:

- API keys
- access tokens
- passwords
- usernames
- server names that should not be public
- file paths that differ between users

Do not use environment variables for:

- patient-identifiable data
- files or extracts
- values that should be managed through an approved corporate password or secrets-management process
- anything where Information Governance advice says a different storage method is required

If the value is a shared team credential, agree where it should be stored and rotated before adding code that depends on it.

## Choose where to store the variable

There are two common places to store environment variables for R:

- User-level `.Renviron`: stored in your home area and available across your R projects.
- Project-level `.Renviron`: stored in one project folder and available when that project is opened.

For personal credentials, prefer a user-level `.Renviron`. This reduces the chance that a private value is accidentally copied into a project repository.

For a project-specific setting, a project-level `.Renviron` can be useful. If it contains any sensitive value, add `.Renviron` to the project's `.gitignore` before committing.

If a project-level `.Renviron` file exists, it may take priority over your user-level `.Renviron` for that project. If a variable works in one project but not another, check whether the project has its own `.Renviron`.

## Set up a user-level `.Renviron`

1. Open RStudio.
2. Run:

   ```r
   usethis::edit_r_environ()
   ```

3. Add one variable per line:

   ```text
   MY_API_KEY=replace-this-with-the-real-key
   ```

   Do not put spaces around the `=` sign.

4. Save the file.
5. Restart your R session.
6. Check that R can read the value:

   ```r
   Sys.getenv("MY_API_KEY")
   ```

If this prints the value you saved, your script can now use `Sys.getenv("MY_API_KEY")`.

## Set up a project-level `.Renviron`

Only use a project-level `.Renviron` when the variable is specific to that project.

1. Open the project in RStudio.
2. Run:

   ```r
   usethis::edit_r_environ(scope = "project")
   ```

3. Add the variable:

   ```text
   MY_API_KEY=replace-this-with-the-real-key
   ```

   Do not put spaces around the `=` sign.

4. Add `.Renviron` to the project's `.gitignore` file:

   ```text
   .Renviron
   ```

5. Save both files.
6. Restart your R session.
7. Check that R can read the value:

   ```r
   Sys.getenv("MY_API_KEY")
   ```

8. Before committing, check that `.Renviron` is not listed as a file to be committed:

   ```bash
   git status
   ```

## Share the variable name without sharing the secret

If colleagues need to know which environment variables your code expects, create an example file without real values. For example, commit a file called `.Renviron.example`:

```text
MY_API_KEY=
DATABASE_HOST=
```

Then explain in the project `README.md` that users should copy the variable names into their own `.Renviron` and fill in the values locally.

The example file can be committed because it contains names only, not the private values.

## Use the variable in R code

Avoid writing this:

```r
api_key <- "abc123-real-key"
```

Use this instead:

```r
api_key <- Sys.getenv("MY_API_KEY")
```

It is also helpful to stop early if the variable has not been set:

```r
api_key <- Sys.getenv("MY_API_KEY")

if (api_key == "") {
  stop("MY_API_KEY is not set. Add it to your .Renviron file and restart R.")
}
```

This makes the problem clear for the next person running the code.

## Check before committing

Before committing work, check that no secrets have been staged:

```bash
git status
git diff --cached
```

If the project uses a `.gitignore`, check that it includes common local files such as:

```text
.Renviron
.Rhistory
.RData
.httr-oauth
```

The `{usethis}` package can also help keep common local files out of git:

```r
usethis::git_vaccinate()
```

This is a useful safety net, but it does not replace checking the files you commit.

## Consider `{keyring}` for higher-risk secrets

Environment variables in `.Renviron` are stored as plain text on disk. For higher-risk personal credentials, consider the `{keyring}` package, which stores secrets in the operating system credential store.

Set the secret once:

```r
keyring::key_set("my-service")
```

Read it in your code:

```r
api_key <- keyring::key_get("my-service")
```

This avoids keeping the secret in a project file. Check local PHS guidance before using `{keyring}` for shared or operational credentials.

## If a secret has already been committed

Do not assume that deleting the value in a new commit is enough. Git keeps previous versions in the repository history.

If a username, password, API key, token, or other confidential value has been committed:

1. Follow the usual Information Governance process.
2. Rotate or revoke the affected credential where possible.
3. Remove the value from git history, not only from the latest file.
4. Review the [security section of the PHS GitHub guidance](/Version%20Control/GitHub%20Guidance.md#security).
5. Follow GitHub's guidance on [removing sensitive data from a repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository).

## Resources

- [Posit documentation on `.Renviron`](https://docs.posit.co/ide/user/ide/guide/environments/r/managing-r.html#renviron)
- [R documentation for `Sys.getenv()`](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Sys.getenv.html)
- [`{keyring}` documentation](https://keyring.r-lib.org/)
- [`usethis::edit_r_environ()` documentation](https://usethis.r-lib.org/reference/edit.html)
- [`usethis::git_vaccinate()` documentation](https://usethis.r-lib.org/reference/git_vaccinate.html)
