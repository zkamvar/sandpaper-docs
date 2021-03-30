---
title: "Editing a {sandpaper} lesson"
teaching: 5
exercises: 0
---

:::::::::::::::::::: questions

 - What is the folder structure of a lesson?
 - How do you download an existing {sandpaper} lesson?
 
:::::::::::::::::::::::::::::

:::::::::::::::::::: objectives

 - Understand how to clone an existing lesson from GitHub
 - Use `sandpaper::build_lesson()` to preview a lesson
 - Update the configuration for a lesson
 - Rearrange the order of episodes

:::::::::::::::::::::::::::::::


If you want to edit and preview your lesson using {sandpaper}, this is the
episode for you. If you want to create a new lesson, head back to the episode
for [Creating a New Lesson](introduction.html).

## Downloading a Lesson {#create-from-github}

If you are comfortable with git, use this command to clone this repository to
your working directory

```bash
cd ~/Documents/Lessons
git clone https://github.com/zkamvar/sandpaper-docs.git
cd sandpaper-docs
R
```

If you are NOT comfortable with git, you can download with R. First, open 
RStudio and think about where on your computer you want to work on lessons
(e.g. `~/Documents/Lessons`). Once you know this, you can open RStudio and type
in the R console:

```r
usethis::create_from_github("zkamvar/sandpaper-docs", destdir = "~/Documents/Lessons")
```

By default, this will clone the lesson to `~/Documents/Lessons/sandpaper-docs`
and open a new RStudio session inside of the lesson repository. In the next section, 
we will explore the folder structure of a lesson. 


:::::::::::::::::::::::::::: challenge

### Preview the Lesson

1. Open RStudio
2. Use the keyboard shortcut <kbd>ctrl + shift + b</kbd> 
   (<kbd>cmd + shift + b</kbd> on macOS) to build and preview this lesson. 
3. Open THIS file (`episodes/editing.Rmd`) and add step 4: preview the lesson again.

What do you notice?

::::::::: solution

What you should notice is that the only file updated when you re-render the
lesson is the file you changed (`episodes/editing.Rmd`). 

:::::::::::::::::
::::::::::::::::::::::::::::::::::::::

## Folder Structure

:::::::::::::::: callout

### :construction: This May Change :construction:

The exact folder structure still has the possibility to change based on user
testing for the front-end of the lesson website.

::::::::::::::::::::::::

The template folder structure will contain markdown files arranged so that they
match what we expect the menubar for the lesson should be. All folders and files
with an arrow `<-` are places in the lesson template you will be modifying:

```
|-- .gitignore         #  | Ignore everything in the site/ folder
|-- .github/           #  | Configuration for deployment
|-- episodes/          # <- PUT YOUR EPISODE MARKDOWN FILES IN THIS FOLDER
|-- instructors/       # <- Information for Instructors (e.g. guide.md)
|-- learners/          # <- Information for Learners (e.g. reference.md and setup.md)
|-- profiles/          # <- Learner and/or Instructor Profiles
|-- site/              #  | This is a "scratch" folder ignored by git and is where the rendered markdown files and static site will live
|-- config.yaml        # <- Use this to configure lesson metadata
|-- index.md           # <- The landing page of your site
|-- CONTRIBUTING.md    #  | Carpentries Rules for Contributions (REQUIRED)
|-- CODE_OF_CONDUCT.md #  | Carpentries Code of Conduct (REQUIRED)
|-- LICENSE.md         #  | Carpentries Licenses (REQUIRED)
`-- README.md          # <- Introduces folks how to use this lesson and where they can find more information.
```

This folder structure is heavily opinionated towards achieving our goals of
creating a lesson template that is fit for the purpose of delivering lesson
content for not only Carpentries instructors, but also for learners and
educators who are browsing the content after a workshop. It is not designed to
be a blog or commerce website. Read the following sections to understand the 
files and folders you will interact with most. 

All source files in {sandpaper} are written in [pandoc]-flavored markdown and
all require yaml header called `title`. Beyond that, you can put anything in
these markdown files. 

## `config.yaml`

This configuration file contains global information about the lesson. It is
purposefully designed to only include information that is editable and
relevant to the lesson itself and can be divided into two sections: information
and organization

### Information

These fields will be simple key-pair values of information used throughout the episode

carpentry
:    The code for the specific carpentry that the lesson belongs to (swc, dc, lc, cp)

title
:    The main title of the lesson

life_cycle
:    What life cycle is the lesson in? (pre-alpha, alpha, beta, stable)

license
:    The license the lesson is registered under (defaults to CC-BY 4.0)

source
:    The github source of the lesson

branch
:    The default branch

contact
:    Who should be contacted if there is a problem with the lesson

### Organization

These fields match the folder names in the repository and the values are a list of
file names in the order they should be displayed. By default, each of these fields
is blank, indicating that the default alphabetical order is used. To list items,
add a new line with a hyphen and a space preceding the item name (`- `). For
example, if I wanted to have the episodes called "one.md", "two.Rmd", "three.md",
and "four.md" in numerical order, I would use:

```yaml
episodes:
- one.md
- two.Rmd
- three.md
- four.md
```

Below are the four possible fields {sandpaper} will recognize:

episodes
:    The names of the episodes (main content)

instructors
:    Instructor-specific resources (e.g. outline, etc)

learners
:    Resources for learners (e.g. Glossary terms)

profiles
:    Learner profile pages 


::::::::::::::::::::::::::::::: challenge

### Configuring Episode Order

Open `config.yaml` and change the order of the episodes. Preview the lesson
after you save the file. How did the schedule change?

::::::::::::::::: solution

The episodes appear in the same order as the configuration file and the timings
have rearranged themselves to reflect that.

::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::

## `episodes/`

This is the folder where all the action is. It contains all of the episodes, 
figures, and data files needed for the lesson. By default, it will contain an
episode called 01-introduction.Rmd. You can edit this file to use as your
introduction. To create a new episode, use the folowing function:


```r
sandpaper::create_episode("episode-name")
```

This will template a {sandpaper} episode called `02-episode-name.Rmd` in the
`episodes/` directory of your lesson and pre-populate it with objectives,
questions, and keypoints. 

After you add your draft of the episode, you need to add it to the `episodes`
section of `config.yaml`. This will be your table of contents. By default, all
of the episodes are rendered in alphabetical order, and the `config.yaml` can
allow you to work on episodes that are not yet ready for production.

## `instructors/`

This folder contains information used for instructors only. Downloads of code
outlines, aggregated figures, and slides would live in this folder. 

## `learners/`

All the extras the learner would need, mostly a setup guide and glossary would
live here.

## `profiles/`

Learner profiles would live in this folder and target learners, instructors, and
maintainers alike to give a focus on the lesson.

## `index.md`

This is the landing page for the lesson. The schedule is appended at the bottom
of this page and this will be the first page that anyone sees.

## `README.md`

This page gives information to maintainers about what to expect inside of th
repository and how to contribute. 


::::::::::::::::::::: keypoints

- `usethis::create_from_github()` will download a github repository to your computer
- `sandpaper::build_lesson()` renders the site and rebuilds any sources that have changed. 
- RStudio shortcuts are <kbd>cmd + shift + B</kbd> and <kbd>cmd + shift + K</kbd>
- To edit a lesson, you only need to know Markdown and/or R Markdown
- The folder structure is designed with maintainers in mind
   
 - New episodes can be added with `sandpaper::create_episode()`

:::::::::::::::::::::::::::::::
