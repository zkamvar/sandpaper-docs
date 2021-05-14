---
title: "Introduction to the New Template"
teaching: 10
exercises: 2
---

:::::::::::: questions

 - How do I get started?

::::::::::::::::::::::

::::::::::: objectives

- Create new lesson from scratch
- Identify the main command to preview the template
- Understand the basic structure of the new template

::::::::::::::::::::::


## Quickstart: Create a New Lesson

Let's say you have a set of R Markdown files that you used for a class website
that you want to convert into a Carpentries Lesson. To go from zero to a new 
lesson website that auto-renders R Markdown documents to a functional website is
three steps with `{sandpaper}`:

1. Create a site
2. Push to GitHub
3. Add your files

That's it. After that, if you know how to write in Markdown, you are good to go.

:::::::::::::::::: callout

### Takeaway message

Contributors should only be expected to know basic markdown and *very* minimal
yaml syntax in order to work on lessons.

:::::::::::::::::::::::::::

::::::::::::::::: challenge

### Try it yourself!

Follow these steps to create a brand new lesson on your Desktop called
"buoyant-barnacle".

1. Follow the [setup instructions](setup.html)
2. Open RStudio (or your preferred interface to R)
3. Use the following code:

```r
library("fs") # file system package for cross-platform paths
library("sandpaper")

# Create a brand new lesson on your desktop called "buoyant-barnacle"
bb <- path_home("Desktop/buoyant-barnacle")
print(bb) # print the new path to your screen
create_lesson(bb) # create a new lesson in that path
```

:::::::::::::::::::::::::::

If everything went correctly, you will now have a new RStudio window open to
your new project called "buoyant-barnacle" on your Desktop (if you did not use
RStudio, your working directory should have changed, you can check it via the
`getwd()` command). 

Your lesson will be initialized with a brand new git repository with the initial
commit message being `Initial commit [via {sandpaper}]`. 

:::::::::::::::::::::: callout

## :ladybug: Known Quirk

If you are using RStudio, then an RStudio project file (`*.Rproj`) is
automatically created to help anchor your project. You might notice changes to
this file at first as RStudio applies your global user settings to the file.
This is perfectly normal and we will fix this in a future iteration of
{sandpaper}.

::::::::::::::::::::::::::::::

## Previewing Your New Lesson

After you created your lesson, you will want to preview it locally. First, make
sure that you are in your newly-created repository and then use the following
command:

```r
sandpaper::build_lesson()
```

:::::::::::::::: discussion

### What's with the `::` syntax?

This is a syntax that clearly states what package a particular function comes 
from. In this case, `sandpaper::build_lesson()` tells R to use the 
`build_lesson()` function from the `sandpaper` package. These commands can be 
run without first calling `library(<packagename>)`, so they are more portable. 
I will be using this syntax for the rest of the lesson.

:::::::::::::::::::::::::::

:::::::::::::: callout

### DID YOU KNOW? Keyboard Shortcuts are Available

If you are using RStudio, did you know you can use keyboard shortcuts to render
the lesson as you are working on the episodes?

Render and preview the whole lesson
:    <kbd>ctrl + shift + B</kbd>

Render and preview an episode
:    <kbd>ctrl + shift + K</kbd>
::::::::::::::::::::::

The first time you run this function, you might see A LOT of output on your
screen and then your browser will open the preview. If you run the command 
again, you will see much less output. If you like to would like to know how
everything works under the hood, you can check out the [{sandpaper} generator
chapter](sandpaper.html).

::::::::::::::::::::::::::::::::::::: discussion

### How do I determine the order of files displayed on the website?

The `config.yaml` file contains four fields that correspond to the folders in
your repository: `episodes`, `instructors`, `learners`, `profiles`. By default,
they are displayed in alphabetical order, but if you want to customize exactly
what content is published on the website, you can add a yaml list of the
filenames to determine order. 

For example, if you had three episodes called "introduction.md", "part_two.Rmd",
and "in_progress.md" and you wanted to only show introduction and part_two, you
would edit `config.yaml` to list those two files under `episodes:`:

```yaml
episodes:
- introduction.md
- part_two.Rmd
```

::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::: challenge

### Set the schedule (optional)

Render the lesson again. It should run more quickly this time, but you might
notice a warning at the end of the rendering:

:::::::::::::: solution

### Warning Message

```{.warning}
Warning message:
In warn_schedule() :
  No schedule set, using Rmd files in `episodes/` directory.
To remove this warning, define your schedule in `config.yaml` or use `set_episodes()` to generate it.
```

::::::::::::::


This is informing you that the order of episodes in your lesson is defined via
alphabetical order of all markdown files in the `episodes/` directory unless you
set the `episodes:` field in your configuration file (`config.yaml`).

1. Open `config.yaml` in a text editor
2. On line 46, you should see the `episodes:` field.
3. Add `- 01-Introduction.Rmd` to the line below.
4. Save the file and re-render. You should notice that the warning has
   disappeared. 

::::::::::::::::::::::::::::::::::::::::::::::::


## Push to GitHub

The lesson you just created lives local on your computer, but still needs to go
to GitHub. At this point, we assume that you have successfully [linked your 
computer to GitHub](setup.html#connect-to-github-1).

1. visit <https://github.com/new/>
2. enter `buoyant-barnacle` as the repository name
3. Press the green "Create Repository" button at the bottom of the page
4. Follow the instructions on the page to push an existing repository from the
   command line. 

:::::::::::: callout

### Alternative: One-step R solution

If you use R and use an HTTPS protocol, this can be done in a single step from
inside RStudio with the {usethis} package:

```r
usethis::use_github()
```

This function will set up a new repository under your personal account called
`buoyant-barnacle`, add that remote to your `git remotes`, and automatically
push your repository to GitHub. 

If you don't use the HTTPS protocol, and want to find out how to set it in R,
we have [a walkthrough to set your credentials in the learners section
](github-pat.html).

::::::::::::::::::::

A few minutes after you pushed your repository, the GitHub workflows would have
validated your lesson and created deployment branches. You can track the
progress at `https://github.com/<USERNAME>/buoyant-barnacle/actions/`. Once you
have a green check mark, you can [set up GitHub
Pages](https://docs.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
by going to `https://github.com/<USERNAME>/buoyant-barnacle/settings/pages` and
choosing `gh-pages` from the dropdown menu as shown in the image below:

![screencapture of the initial view of the GitHub Pages section of the settings tab](fig/github-pages-none.png){.image-with-shadow}

Click on the "select branch" button and select "gh-pages":

![screencapture of expanded "select branch" button with "gh-pages" selected](fig/github-pages-gh-pages.png){.image-with-shadow}

::::::::::::: callout

### :hourglass: Be Patient

GitHub needs to start up a new virtual machine the first time you use this, so
it may take up to 30 minutes for things to get started: 15 minutes for the
workflow to spin up and then another 15 minutes for the machine to bootstrap
and cache. 

:::::::::::::::: 

## Tools

As described in [the setup document](setup.html), the lesson template now only
requires R and [pandoc] to be installed. The tooling from the current lesson
template has been split up into three R packages:

1. [{varnish}] contains the HTML, CSS, and JavaScript elements
1. [{pegboard}] is a validator for the markdown documents
1. [{sandpaper}] is the engine that puts everything together. 

::::::::::::: keypoints

- Lessons can be created with `create_lesson()`
- Preview lessons with `build_lesson()`
- The toolchain is designed to be modular.

:::::::::::::::::::::::


[{varnish}]: https://github.com/carpentries/varnish/ 
[{pegboard}]: https://carpentries.github.io/pegboard/
[{sandpaper}]: https://carpentries.github.io/sandpaper/
[pandoc]: https://pandoc.org/
