---
title: Setup
---

## Overview

The lesson infrastructure is built on Git, [R], and [pandoc]. It consists of 
four components:

1. The source content (plain markdown or RMarkdown files organized into folders
   with a configuration yaml file)
2. The engine (R package [{sandpaper}])to orchestrate building the content from
   markdown to HTML
3. The validator (R package [{pegboard}]) to parse the source files and
   highlight common errors[^tinkr]
4. The style (R package [{varnish}]) HTML, CSS, and JavaScript styling elements
   for the final website

[Details of how these tools work together are explained in the Lesson 
Deployment](deployment.md) chapter. In short, you can expect to interact with
the source content and {sandpaper} to author and preview your lesson.

### Required Software {#required}

This setup document will walk you through the process of installing or upgrading
the required software in the following order.

1. **Git** (&ge; 2.28 recommended)
2. **R** (&ge; 3.6)
3. **pandoc** (&ge; 2.11)
4. The lesson infrastructure R packages
   i. **[{sandpaper}]** (development version)
   ii. **[{varnish}]** (development version)
   iii. **[{pegboard}]** (development version)
   iiii. **[{tinkr}]** (markdown parser required by {pegboard}, development version)

### Recommended Software {#recommend}

If you are using R or pandoc for the first time, we recommend using [the RStudio
IDE][RStudio] for the following reasons:

1. It comes with [pandoc] pre-installed.
2. Works consistently across all major platforms.
3. A dedicated BASH console so you can easily switch between R and Git
   operations.
4. Convenient keyboard shortcuts to preview lessons.
5. On Windows, it will automatically detect your R installation without you
   needing to edit your `PATH`.

If you do not want to use RStudio, that's perfectly okay and expected! We want
to be able to meet you where you are to work with the new template. If you feel
comfortable using a different tool (e.g. the command line or VSCode), then you
should install R and pandoc separately and make sure that they are in your path.


### Installation 

This will guide you through installing the foundational software and 
infrastructure packages on your computer. If you already have software
installed and are curious if you should update it to a newer version, the answer
is almost always, yes, update to a newer version, because often the [newer
versions will contain important bug fixes that are important to the secruity of
your computer](https://github.com/git/git/security/advisories/GHSA-8prw-h3cq-mghm).

Jump to the installation instructions for your system: [Windows](#windows),
[MacOS](#mac), or [Linux](#linux)

## Installing on Windows {#windows}

### Git

We recommend installing git via the Git for Windows installer at 
<https://gitforwindows.org/>. The installer is going to ask a lot of questions,
so we recommend [using The Carpentries checklist for workshop
participants](https://carpentries.github.io/workshop-template/#shell-windows).

#### Test your installation

To test that you have git installed, you can go to your taskbar at the bottom 
of your screen and type `cmd` to bring up the command prompt. From there, you
can type `git --version` to see the version of your git installation. You might
see something like this:

```bash
git --version
```

```output
git version 2.31.1.windows.1
```

If, however, you see this error, then you should try to install git again. 

```error
'git' is not recognised as an internal or external command,
operable program or batch file.
```


### R

You can install the latest [R] for Windows from 
<https://cran.r-project.org/bin/windows/base/>. There is also a video tutorial
up on [The Carpentries instructions for workshop
participants](https://carpentries.github.io/workshop-template/#rstats-windows)
that can be quite helpful for parsing the steps of installing R on Windows.

::::::::::::::::::::: callout

#### Optional: Want to add R to your PATH? {#winpath}

As we mention above, [we recommend using RStudio for your lesson](#recommend),
but if you want to be able to integrate the lesson infrastructure into your own
preferred workflow, you need to have R on your path. The catch is that R for
Windows does not automatically set your `PATH` variable. 

[Here are some instructions on setting up your PATH on Windows using both the
GUI and CLI](https://www.maketecheasier.com/what-is-the-windows-path/). Note
that R will normally install at something like 
`c:\Program Files\R\R-4.1.0\bin\x64`, but if you are not admin, it will install
in your Documents folder. 

To verify that R is installed in your `PATH`, you can go to your taskbar at the
bottom of your screen and type `cmd` to bring up the command prompt. From there,
you can type `R --version` at the prompt:

```bash
R --version
```
```output
R version 4.1.0 (2021-05-18) -- "Camp Pontanezen"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-mingw32/x64 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```

:::::::::::::::::::::::::::::

### pandoc

There are two ways to install pandoc:

#### Via RStudio (recommended)

Since pandoc comes bundled with RStudio, you can install it by installing the
latest version of RStudio. You can [download the installer from the RStudio 
website][RStudio].

#### Via the pandoc website

If you are comfortable adding R to your windows PATH (see [previous 
section](#winpath)), then you can install pandoc by using the binary provided on
its website at <https://pandoc.org/installing.html>

#### Test your installation

We will wait to test the pandoc installation after we install the
infrastructure packages, to make sure it's discoverable by R. 

### Infrastructure R packages

To install the R packages, you will need to **open RStudio** (or start R from
the command line if you did not install RStudio) and enter the following lines
into the console.

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  CRAN = "https://cran.rstudio.com/"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard", "tinkr"))
```

## Installing on MacOS {#mac}

### Git

You should have git pre-installed on your macOS, but it is likely that this is
an old version. We recommend installing [The latest version of Git for MacOS
from sourceforge](http://sourceforge.net/projects/git-osx-installer/files/) 
(**ignore the big green button** and choose the latest version from the list). 
For a video walkthrough and an explanation of what to expect, you can look at 
the [instructions for workshop 
participants](https://carpentries.github.io/workshop-template/#git-macos).

#### Test your installation

To test your installation of Git and confirm it works, open **Terminal.app** and
type the following:

```bash
git --version
```

```output
git version 2.31.0
```

If you have the default version of git, you might see this output, and that's
okay for the purposes of this template. 

```output
git version 2.24.3 (Apple Git-128)
```

### R

You can install the latest [R] release for MacOS from 
<https://cran.r-project.org/bin/MacOSX>. There is also a video tutorial
up on [The Carpentries instructions for workshop
participants](https://carpentries.github.io/workshop-template/#rstats-macos)
that can be quite helpful for parsing the steps of installing R on MacOS.

#### Test your installation

You can test your installation of R by opening **Terminal.app** and typing `R
--version` into the prompt:

```bash
R --version
```
```output
R version 4.1.0 (2021-05-18) -- "Camp Pontanezen"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-apple-darwin17.0 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```

### pandoc

There are two ways to install pandoc:

#### Via RStudio (recommended)

Since pandoc comes bundled with RStudio, you can install it by installing the
latest version of RStudio. You can [download the installer from the RStudio 
website][RStudio].

#### Via the pandoc website

If are more comfortable using R from the command line, then you can install
pandoc by clicking the "Download the latest installer for macOS" button at
<https://pandoc.org/installing.html>. This will save a file called 
`pandoc-X.XX-macOS.pkg` installer to your computer. Open the installer and
follow the instructions to install pandoc on your computer.

#### Test your installation

We will wait to test the pandoc installation after we install the
infrastructure packages, to make sure it's discoverable by R. 

### Infrastructure R packages

To install the R packages, you will need to **open RStudio** (or start R from
the command line if you did not install RStudio) and enter the following lines
into the console.

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  CRAN = "https://cran.rstudio.com/"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard", "tinkr"))
```

## Installing on Linux {#linux}

A lot of the documentation for Linux is nuanced because it assumes that if you
use Linux, then you automatically know how to install things by the command
line. I will be providing instructions as best I can for Ubuntu Linux and point
to resourced for other distributions. For Ubuntu/Debian, the default `apt`
repository is often out of date, so you will need to use a 
[Personal Package Archive aka PPA](https://itsfoss.com/ppa-guide/) to install
the latest version of a particular software, which I will include in these
instructions. 

### Git

You should have git pre-installed on your computer, but it will likely be 
outdated. It's okay if this is the case, but if you want to update via `apt`,
you can add the git-core ppa:

```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```

#### Test your installation

Test your git installation by opening the terminal and running

```bash
git --version
```
```output
git version 2.31.1
```

### R

To install R, you can visit <https://cran.r-project.org/bin/linux/> to check if
your platform is supported. For Ubuntu, there are detailed instructions at:
<https://cran.r-project.org/bin/linux/ubuntu/>. Here are the commands to register
the PPA on your machine and then install R:

```bash
# update indices
sudo apt update -qq
# install two helper packages we need
sudo apt install --no-install-recommends software-properties-common dirmngr
# import the signing key (by Michael Rutter) for these repo
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
# add the R 4.0 repo from CRAN -- adjust 'focal' to 'groovy' or 'bionic' as needed
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"

# Install R
apt install --no-install-recommends r-base
```

#### Test your installation

Test your R installation by opening your terminal and running:

```bash
R --version
```

```output
R version 4.1.0 (2021-05-18) -- "Camp Pontanezen"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.

```

### pandoc

There are two ways to install pandoc:

#### Via RStudio (recommended)

Since pandoc comes bundled with RStudio, you can install it by installing the
latest version of RStudio. You can [download the installer from the RStudio
website][RStudio]. When installing RStudio for Linux, your distribution may not
be shown on the landing page (e.g. Ubuntu 20.04). In this case, choose the most
recent version and download it to your Downloads folder or install it directly.

::::::::::: callout

##### Optional: verify the install

You can optionally verify the download before installing by following the
instructions at <https://www.rstudio.com/code-signing/>.

:::::::::::::::::::


#### Via the pandoc website

If are more comfortable using R from the command line, then you can install
pandoc by clicking the "Download the latest installer" button at
<https://pandoc.org/installing.html>. This will bring you to the release page 
on GitHub with a list of installers, and you should choose one of the ones that
says "linux" according to what chip architecture you have (AMD vs ARM).

#### Test your installation

We will wait to test the pandoc installation after we install the
infrastructure packages, to make sure it's discoverable by R. 

### Infrastructure R packages

Linux packages normally need to be compiled by your system, which can take a 
long time the first time it happens. RStudio provides a package manager that
pre-compiles Linux binaries. Note that you do not have to be using RStudio to
take advantage of these binaries. The one we are using is set up for Ubuntu 
20.04 (focal). 

:::: callout

#### What if I have a different version of Linux?

If you have a different version of linux, you can visit 
https://packagemanager.rstudio.com/client/#/repos/1/overview, select your
system where it says "Use this URL to work with the latest binary packages for
Ubuntu 20.04 (Focal) **change**", and replace the packagemanager URL below.

::::

To install the R packages, you will need to **open RStudio** (or start R from
the command line if you did not install RStudio) and enter the following lines
into the console.

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  CRAN = "https://packagemanager.rstudio.com/all/__linux__/focal/latest"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard", "tinkr"))
```

::::::::::::: callout

#### What if I get errors installing packages?

If you run into errors (non-zero exit status), it probably means that you were
missing a C library dependency that needs to be installed via your package 
manager (i.e. apt). To resolve these issues, scroll back in the log and you
might find messages that looks similar to this:

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

:::::::::::::::::::::

## Test your installation {#install-test}

Now that you have installed the lesson components, it is a good idea to run a
small test to verify that these components work together. To test your 
installation **open RStudio** (or launch R if you have not installed RStudio)
and enter the following commands to confirm everything works

```r
rmarkdown::pandoc_version()
tmp <- tempfile()
sandpaper::create_lesson(tmp, open = FALSE)
sandpaper::build_lesson(tmp, preview = FALSE, quiet = TRUE)
fs::dir_tree(tmp, recurse = 1)
```

```output
[1] ‘2.12’
[1] "/tmp/RtmpCjGtw3/fileac05502830cf"
Warning message:
In warn_schedule() :
  No schedule set, using Rmd files in `episodes/` directory.
To remove this warning, define your schedule in `config.yaml` or use `set_episodes()` to generate it.
/tmp/RtmpCjGtw3/fileac05502830cf
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE.md
├── README.md
├── config.yaml
├── episodes
│   ├── 01-introduction.Rmd
│   ├── data
│   ├── fig
│   └── files
├── index.md
├── instructors
│   └── instructor-notes.md
├── learners
│   └── Setup.md
├── profiles
│   └── learner-profiles.md
└── site
    ├── DESCRIPTION
    ├── README.md
    ├── _pkgdown.yaml
    ├── built
    └── docs
```

If the installation did not work, please [raise an issue on
GitHub](https://github.com/zkamvar/sandpaper-docs/issues/new) and I can help
troubleshoot. 

## Installation FAQ

### Why does it take 5 lines of code to install the infrastructure?

In the future, this will be ONE line of code!

Since we are currently in the alpha phase of testing, the infrastructure can
update at any moment. Normally, packages will come from 
[CRAN](https://glosario.carpentries.org/en/#cran), but our development packages
are not yet on CRAN, so the are stored in The Carpentries and rOpenSci
development repositories. 

### Do I really need to use RStudio?

No. We recommend using RStudio for [several reasons that pertain to ease of
use and standardisation across systems](#recommend), but we do not absolutely
require it. If you are able to get Git, R, and pandoc installed on your system,
then you do not need to use RStudio.

### What is an R Library?

An R library is a folder on your computer that stores R packages. When you
install R packages, the first message you will see will probably be something
like (on Windows):

```
Installing packages into ‘c:/Users/USER/Documents/R/win-library/4.0’
(as ‘lib’ is unspecified)
```

This folder is where all of the R packages you install via `install.packages()`
will live. If you ever need to look this up, you can use the `.libPaths()`
function.

Sometimes, your R session will issue a warning that says a folder is not
writeable and asks if you would like to use a personal library instead. In this
case, select "yes".

## Using the lesson engine

Throughout the lesson, I will ask you to **open R or RStudio**. If you are using
RStudio, you can open it by double-clicking on the RStudio icon in your
application launcher; you do not have to open R separately to use RStudio. 

If you are using R, you can open it in your terminal application by typing `R`.
Your prompt will be replaced by a `>`, which indicates that you are in R's 
interactive [REPL](https://glosario.carpentries.org/en/#repl). 

You can exit R or RStudio by typing `q()` in the R console. 

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
[{sandpaper}]: https://carpentries.github.io/sandpaper/
[{pegboard}]: https://carpentries.github.io/pegboard/
[{varnish}]: https://github.com/carpentries/varnish#readme
[{tinkr}]: https://docs.ropensci.org/tinkr/
[RStudio]: https://rstudio.com/products/rstudio/download/#download
[^workspace]: By default, R will ask if you want to save your workspace to a
  hidden file called `.RData`. This is loaded when you start R, restoring your
  environment with all of the packages and objects you had previously loaded.
  This default behavior is not good for reproducibility and makes updating
  packages very very difficult. In 2017 Jenny Bryan wrote a very good article
  about the benefits of having a project-based workflow, starting from a clean
  slate: <https://www.tidyverse.org/blog/2017/12/workflow-vs-script/>

[^tinkr]: Note: {pegboard} requires the [{tinkr}] package from rOpenSci. It 
  is still in development, so we will install this package explicitly. 
