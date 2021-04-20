---
title: Setting Up a Personal Access Token via R
---

## I use SSH, Why should I use HTTPS?

GitHub has announced that [passwords will no longer be used for authentication
from the command line starting in August 2021](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/).
While you may or may not be comfortable with SSH, here a few things that may
motivate you:

1. HTTPS is recommended by both GitHub and RStudio for people starting with R,
   so switching to HTTPS will help you empathize and demonstrate the ropes to 
   learners in the long run.
2. HTTPS gives you more fine-grained control over what access each token gives.
3. [RStudio Cloud](https://rstudio.cloud) is a really good platform that can
   connect to your GitHub account if you need to work on lesson development
   when you don't have your computer handy. You cannot use SSH with that service,
   but it is possible to access it via HTTPS. 
4. You can connect to the GitHub API with a higher rate limit, which means that
   you can auto-create remote repositories and analyze GitHub data without a
   web browser.

## Verifying Your Git Situation

To confirm that your Git session is correctly configured, open RStudio, and run
the following line to check if your HTTPS credentials are set up properly:

```r
library("usethis")
git_sitrep() # git situation report
```

Pay attention to the **GitHub** report. What does it look like?


### GitHub connected via PAT

```output
Git config (global)
● Name: 'Zhian N. Kamvar'
● Email: 'zkamvar@gmail.com'
● Vaccinated: FALSE
ℹ See `?git_vaccinate` to learn more
● Default Git protocol: 'ssh'
GitHub
● Default GitHub host: 'https://github.com'
● Personal access token for 'https://github.com': '<discovered>'
● GitHub user: 'zkamvar'
● Token scopes: 'gist, repo, user, workflow'
● Email(s): 'zkamvar@gmail.com (primary)', ...
Git repo for current project
ℹ No active usethis project
```

If your output looks like this, then you are properly set up and you are good to
go! If not, read on!

## Creating a New GitHub Personal Access Token

If you see errors associated with your GitHub token (see below, e.g. 'Token is
invalid' or 'Can't retrieve registered email address(es)'), then you should
create a new one. Dr. Jenny Bryan wrote [an excellent resource for creating and
caching your GitHub credentials on your computer
](https://happygitwithr.com/credential-caching.html#how-to-manage-a-pat) that
will walk you through the process of generating a PAT, and storing it in a
secure location. Here are the steps briefly via R:

1. Create a GitHub PAT via R with `usethis::create_github_token()` (this will
   open a page in your browser pre-populated with the appropriate scopes. If
   this does not work, [use this link to generate a new token for
   R][token-scope].)
2. Copy and store the token in a password manager (Lastpass, 1Password)
3. Back in R, use `gitcreds::gitcreds_set()` to register your token with git.
4. Check your credentials again with `usethis::git_sitrep()`

At this point, you should have things set up properly. If you are still having
problems, you can try the following two steps (after you have your PAT):

1. in R, use `credentials::git_credentials_forget()` to clear the cache
2. use `credentials::set_github_pat()` and paste your token. 

::::::::: discussion

### Common Token Errors

There are a few possible errors you might see, but the remedy is always the same:
get a new token and register it in your credentials keychain.

#### Invalid Personal Access Token

Invalid tokens can come from old tokens that were deleted from your GitHub
account. 

```output
Git config (global)
● Name: 'Zhian N. Kamvar'
● Email: 'zkamvar@gmail.com'
● Vaccinated: FALSE
ℹ See `?git_vaccinate` to learn more
● Default Git protocol: 'ssh'
GitHub
● Default GitHub host: 'https://github.com'
● Personal access token for 'https://github.com': '<discovered>'
✖ Token is invalid
✖ Can't retrieve registered email address(es)
  If you are troubleshooting, check GitHub host, token, and token scopes
Git repo for current project
ℹ No active usethis projectw
```

#### Password as Token

This error often means that you have your password stored in your keychain
instead of your token. This seems like a weird error until you realize that
GitHub will stop allowing password authentication from the command line in 
August 2021.

```output
Git config (global)
● Name: 'Zhian N. Kamvar'
● Email: 'zkamvar@gmail.com'
● Vaccinated: FALSE
ℹ See `?git_vaccinate` to learn more
● Default Git protocol: 'ssh'
GitHub
● Default GitHub host: 'https://github.com'
Error: GitHub PAT must have one of these forms:
  * 40 hexadecimal digits (older PATs)
  * A 'ghp_' prefix followed by 36 to 251 more characters (newer PATs)
Type .Last.error.trace to see where the error occured
```

#### No Personal Access Token Detected

This means you have not registered a Personal Access Token with git and are good
to start fresh!

```output
● Name: 'Zhian N. Kamvar'
● Email: 'zkamvar@gmail.com'
● Vaccinated: FALSE
ℹ See `?git_vaccinate` to learn more
● Default Git protocol: 'ssh'
GitHub
● Default GitHub host: 'https://github.com'
● Personal access token for 'https://github.com': <unset>
✖ Call `gh_token_help()` for help configuring a token
Git repo for current project
ℹ No active usethis project
```

::::::::::::::::::::::::



[R]: https://cran.rstudio.org/
[token-scope]: https://github.com/settings/tokens/new?scopes=repo,user,gist,workflow&description=R:GITHUB_PAT
[pandoc]: https://pandoc.org/
[RStudio]: https://rstudio.com/products/rstudio/download/#download
