---
title: Setup
---

The {sandpaper} template requires [R] and [pandoc] to be installed, both of 
which are bundled in the [RStudio] IDE. 

## Foundational software

There are three programs that the template works with: Git, RStudio, and pandoc.
They can be installed from the following resources:

 - **Git** https://carpentries.github.io/workshop-template/#git
 - **R** https://carpentries.github.io/workshop-template/#r
 - **pandoc** we recommend installing this by [installing the RStudio IDE][RStudio]

::::: solution

### What if I don't want to use RStudio?

That's perfectly okay! If you do not want to use RStudio, you can install pandoc
directly to your computer by following the directions on
https://pandoc.org/installing.html.  We recommend using RStudio because it is
tightly integrated with pandoc. 

:::::::::


::::::::: prereq

### Setting up your R workspace

When you set up R, it's important to make sure you set it up to never save your
workspace on exit and never load a previously saved workspace on startup. 

#### Via RStudio 

If you are using RStudio, you can [follow the instructions in this forum 
post](https://community.rstudio.com/t/first-line-of-every-r-script/799/12?u=zkamvar):

1. From the menu, select <cmd>Tools<cmd> > <cmd>Global Options</cmd>
2. Under **Workspace Options**, de-select "Restore .RData into workspace at startup" and set "Save workspace to .RData on exit" to "Never"

#### Via Command Line Interface

The flags `--no-restore` and `--no-save` will set these defaults, so you can 
create an alias for BASH:

```bash
alias R='R --no-restore --no-save'
```

::::::::::::::::::

:::::::::::::::::::::: callout

### There are many ways to set up R to work with the lesson template

For example, Zhian Kamvar uses Vim with the NVim-R plugin and 
[radian](https://github.com/randy3k/radian#readme). There is no one right way!

:::::::::::::::::::::::::::::::

## Lesson Template Modules (R packages)

The template is divided into three R pakages, which are designed to be modular
and upgradable on the fly. Because these are still in developement, please use
the following to install (*and update*) the packages:

First, **open R/RStudio** and then follow the instructions based on your
operating system:

::::::::::: solution

### MacOS/Windows

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.github.io/drat/",
  CRAN = "https://cran.rstudio.com/"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard"))
```

::::::::::::::::::::


::::::::::: solution

### Linux

Note: we are using the RStudio package manager. This is set up for Ubuntu 20.04,

:::: callout

### What if I have a different version of Linux?

If you have a different version of linux, you can visit https://packagemanager.rstudio.com/client/#/repos/1/overview, 
select your system where it says "Use this URL to work with the latest binary
packages for Ubuntu 20.04 (Focal) **change**", and replace the packagemanager
URL below.

::::

```r
options(repos = c(
  carpentries = "https://carpentries.github.io/drat/",
  CRAN = "https://packagemanager.rstudio.com/all/__linux__/focal/latest"
))

install.packages(c("sandpaper", "varnish", "pegboard"))
```
::::::::::::::::::::

## Connect to GitHub

If you are currently able to interact with GitHub via the command line without
having to provide your password, then it is very likely that you already have
your credentials set up. **If you feel very comfortable pushing to and pulling
from GitHub on the command line, then you may skip this section.** Otherwise, 
follow along to learn how to connect your git credentials via R (which will 
be available system-wide).

::::::::::::::: callout

### I use SSH credentials, why should I use HTTPS?

GitHub has announced that [passwords will no longer be used for authentication
from the command line starting in August 2021](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/).
While you may be comfortable with SSH, there are three things that may motivate
you:

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

::::::::::::::::::::::::

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
