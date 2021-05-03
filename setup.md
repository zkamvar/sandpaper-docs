---
title: Setup
---

The {sandpaper} template requires [R] and [pandoc] to be installed, both of 
which are bundled in the [RStudio] IDE. 

## Foundational software

There are three programs that the template works with: Git, RStudio, and pandoc.
They can be installed from the following resources:

 - **Git** (>= 2.28) https://carpentries.github.io/workshop-template/#git
 - **R** (>= 3.6) https://carpentries.github.io/workshop-template/#r[^linux-r]
 - **pandoc** (>= 2.11) we recommend installing this by [installing the RStudio
   IDE][RStudio][^linux-rstudio], but you can also install it [via pandoc's
   website](https://pandoc.org/installing) or [via anaconda
   ](https://carpentries.github.io/workshop-template/#python)

::::: solution

### What if I don't want to use RStudio?

That's perfectly okay and expected! 

We recommend using RStudio because it wraps an R console, a text editor, 
git management, and a file browser in one program. This provides a lot of
convenience of being able to work consistently across platforms and reduces the
barrier for entry.

We want to be able to meet you where you are to work with the new template. If
you feel comfortable using a different tool (e.g. the command line or VSCode),
then you should install R and pandoc separately and make sure that they are in
your path.

If you are using Windows, setting up your PATH variables can sometimes be
tricky. The pandoc installer will automatically add itself to your PATH, but R
will not. [Here are some instructions on setting up your PATH on Windows using
both the GUI and CLI](https://www.maketecheasier.com/what-is-the-windows-path/).
Note that R will normally install at something like 
`c:\Program Files\R\R-4.0.0\bin\x64`, but if you are not admin, it will install
in your documents folder. 

:::::::::


## Starting R

Throughout the lesson, I will ask you to **open R or RStudio**. If you are using
RStudio, you can open it by double-clicking on the RStudio icon in your
application launcher. You do not have to open R separately for this.

If you are using R, you can open it in your terminal application by typing `R`.
Your prompt will be replaced by a `>`, which indicates that you are in R's 
interactive [REPL](https://glosario.carpentries.org/en/#repl). 


You can exit R by typing `q()` in the R console. 

::::::::: prereq

### Setting up your R workspace

When you set up R, it's important to make sure you set it up to always start R
with a clean slate[^workspace]: never save your workspace on exit and never
load a previously saved workspace on startup.  

#### Via RStudio 

If you are using RStudio, you can [follow the instructions in this forum 
post](https://community.rstudio.com/t/first-line-of-every-r-script/799/12?u=zkamvar):

1. From the menu, select <cmd>Tools<cmd> > <cmd>Global Options</cmd>
2. Under **Workspace Options**, de-select "Restore .RData into workspace at
   startup" and set "Save workspace to .RData on exit" to "Never"

#### Via Command Line Interface

The flags `--no-restore` and `--no-save` will set these defaults, so you can 
create an alias for R in the `.bashrc` file in your home directory:

```bash
alias R='R --no-restore --no-save'
```

::::::::::::::::::

:::::::::::::::::::::: callout

### There are many ways to set up R to work with the lesson template

For example, Zhian Kamvar uses Vim with the NVim-R plugin  and 
[radian](https://github.com/randy3k/radian#readme) on macOS and Linux. There is 
no one right way!

:::::::::::::::::::::::::::::::

## Lesson Template Modules (R packages)

The template is divided into three R packages, which are designed to be modular
and upgradable on the fly. Because these are still in developement, please use
the following to install (*and update*) the packages:

First, **open R or RStudio** and then follow the instructions based on your
operating system:

::::::::::: solution

### MacOS/Windows

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.github.io/drat/",
  ropensci = "https://ropensci.r-universe.dev/",
  CRAN = "https://cran.rstudio.com/"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard", "tinkr"))
```

::::::::::::::::::::


::::::::::: solution

### Linux

Linux packages normally need to be compiled by your system, which can take a 
long time the first time it happens. RStudio provides a package manager that
pre-compiles Linux binaries. Note that you do not have to be using RStudio to
take advantage of these binaries. The one we are using is set up for Ubuntu 
20.04 (focal). 

:::: callout

### What if I have a different version of Linux?

If you have a different version of linux, you can visit 
https://packagemanager.rstudio.com/client/#/repos/1/overview, select your
system where it says "Use this URL to work with the latest binary packages for
Ubuntu 20.04 (Focal) **change**", and replace the packagemanager URL below.

::::

```r
options(repos = c(
  carpentries = "https://carpentries.github.io/drat/",
  ropensci = "https://ropensci.r-universe.dev/",
  CRAN = "https://packagemanager.rstudio.com/all/__linux__/focal/latest"
))

install.packages(c("sandpaper", "varnish", "pegboard", "tinkr"))
```

If you run into errors (non-zero exit status), it probably means that you were
missing a C library dependency that needs to be installed via your package 
manager. To resolve these issues, scroll back in the log and you might find
messages that looks similar to this:

```output
* installing *source* package ‘xslt’ ...
** using staged installation
Package libexslt was not found in the pkg-config search path.
Perhaps you should add the directory containing `libexslt.pc'
to the PKG_CONFIG_PATH environment variable
No package 'libexslt' found
Using PKG_CFLAGS=-I/usr/include/libxml2
Using PKG_LIBS=-lexslt -lxslt -lxml2
-----------------------------[ ANTICONF ]-------------------------------
Configuration failed to find libexslt library. Try installing:
 * deb: libxslt1-dev (Debian, Ubuntu, etc)
 * rpm: libxslt-devel (Fedora, CentOS, RHEL)
 * csw: libxslt_dev (Solaris)
If libexslt is already installed, check that 'pkg-config' is in your
PATH and PKG_CONFIG_PATH contains a libexslt.pc file. If pkg-config
is unavailable you can set INCLUDE_DIR and LIB_DIR manually via:
R CMD INSTALL --configure-vars='INCLUDE_DIR=... LIB_DIR=...'
---------------------------[ ERROR MESSAGE ]----------------------------
<stdin>:1:10: fatal error: libxslt/xslt.h: No such file or directory
compilation terminated.
------------------------------------------------------------------------
```

Use the instructions in these logs to install the correct package from your
terminal and then open R or RStudio and retry installing the packages. 

::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

### Your R library 

When you install R packages, the first message you will see will probably be 
something like (on Windows):

```
Installing packages into ‘c:/Users/USER/Documents/R/win-library/4.0’
(as ‘lib’ is unspecified)
```

This folder is where all of the R packages you install via `install.packages()`
will live. If you ever need to look this up, you can use the `.libPaths()`
function.

Sometimes, your R session will throw a warning that says a folder is not
writeable and asks if you would like to use a personal library instead. In this
case, select "yes". 

::::::::::::::::::::::::::::::::::::::::::::::::::


## Connect to GitHub

You will need to make sure your git session is connected to GitHub. To do so, 
you will need to use an SSH or HTTPS protocol. If you already know how to push
and pull from GitHub using the command line, you do not need to worry about 
setting this up. 

If you do not have this set up, you should [choose a protocol
](https://docs.github.com/en/github/getting-started-with-github/about-remote-repositories) 
and then set them up according to the instructions from GitHub. 

:::::::::::::::: callout

### Is GitHub's Documentation Confusing?

If you are like me, you may find GitHub's documentation slightly confusing 
and/or lacking. I've found the following resources to be extremely helpful for
setting up authentication credentials for your account:

[Remotes in GitHub (Software Carpentry)](http://swcarpentry.github.io/git-novice/07-github)
: A walkthrough of creating a repository on GitHub and pushing to it via the 
  command line.

[Connect to GitHub (Happy Git With R)](https://happygitwithr.com/push-pull-github.html)
: A walkthrough of creating a throwaway repository that gives you a good idea 
  for the mechanics of working with GitHub. 

[Cache credentials for HTTPS (Happy Git With R)](https://happygitwithr.com/credential-caching.html)
: Clear explanation on how to set up a Personal Access Token and the benefits of
  using HTTPS. This explains how to do this in both the shell and R.

[Set up keys for SSH (Happy Git With R)](https://happygitwithr.com/ssh-keys.html)
: Clear explanation on what SSH key pairs are and how to set up and connect them
  with GitHub. This has recommendations using both the shell and RStudio. 

::::::::::::::::::::::::

[R]: https://cran.rstudio.org/
[pandoc]: https://pandoc.org/
[RStudio]: https://rstudio.com/products/rstudio/download/#download
[^workspace]: By default, R will ask if you want to save your workspace to a hidden file
called `.RData`. This is loaded when you start R, restoring your environment
with all of the packages and objects you had previously loaded. This default
behavior is not good for reproducibility and makes updating packages very
very difficult. In 2017 Jenny Bryan wrote a very good article about the benefits
of having a project-based workflow, starting from a clean slate: 
https://www.tidyverse.org/blog/2017/12/workflow-vs-script/
[^linux-r]: Linux installation may be a bit tricky. Official instructions for 
various flavours of linux can be found at 
<https://cran.r-project.org/bin/linux/>
[^linux-rstudio]: When installing RStudio for Linux, your distribution may not
be shown on the landing p age (e.g. Ubuntu 20.04). In this case, choose the 
most recent version and download it to your Downloads folder or install it 
directly. If you download it, you can [verify the
download](https://www.rstudio.com/code-signing/) before installing. To start
RStudio, you can type `rstudio &` to launch RStudio and let the process run in
the background. 
