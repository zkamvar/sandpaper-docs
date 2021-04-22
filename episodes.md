---
title: "Episode Structure"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions

- How do you create a new episode? 
- What syntax do you need to know to contribute to a lesson with the new template?
- How do you write challenge blocks?
- What syntax do you use to write links?
- How do you include images?
- How do you include math?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives 

- Practice creating a new episode with R
- Understand the required elements for each episode
- Understand pandoc-flavored markdown
- Demonstrate how to include pieces of code, figures, and nested challenge blocks

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

As we will cover in the [next episode](editing.html), all of the episodes live
inside the `episodes/` directory at the top of the lesson folder. Their order is
dictated by the `episodes:` element in the `config.yaml` file (but defaults to 
alphabetical). The other folders (`learners/`, `instructors/`, and `profiles/`)
are similarly configured. This episode will briefly explain how to edit markdown
content in the lessons. 

:::::: prereq

### Buoyant Barnacle

The exercises in this episode correspond to the Buoyant Barnacle repository you
created in [the Introduction](introduction.html)

:::::::::::::

There are three things you should be comfortable with in order to contribute to
a lesson [^Do not worry if you aren't comfortable yet, that's what we will show
you in this episode!]

1. Writing [basic][basic-syntax] and [extended][extended-syntax] markdown syntax
2. Writing [Fenced div elements][fenced-divs] to create callouts and exercise
   blocks
2. Writing simple yaml lists

## Creating A New Episode

To create a new episode, you should open your lesson (`buoyant-barnacle`) in
your RStudio or your favorite text editor and in the R console type:

```r
sandpaper::create_episode("next-episode")
```

This will create a new episode in the episodes folder called "02-next-episode".
If you already have your episode schedule set in `config.yaml`, then this 
episode will not be rendered in the template and will remain a draft until you
add it to the schedule. Next, we will show how you can add a title and other
elements to your episode.

## Required Elements

To keep with our active learning principals, we want to be mindful about the 
content we present to the learners. We need to give them a clear title, 
questions and objectives, and an estimate of how long it will take to navigate
the episode (though this latter point has shown to be demoralizing). Finally, at
the end of the episode, we should reinforce the learners progress with a summary
of key points.

### YAML metadata

The YAML syntax of an episode contains three elements of metadata associated
with the episode at the very top of the file: 

```yaml
---
title: "Using RMarkdown For Automated Reports" # Episode title
teaching: 5   # teaching time in minutes
exercises: 10 # exercise time in minutes
---

## First Episode Section
```

:::::::::::::::: challenge

### Create a Title

Your new episode needs a title! 

1. Open the new episode in your editor
2. edit the title
3. add the episode to the `config.yaml`
4. preview it with `sandpaper::build_lesson()`/<kbd>ctrl + shift + k</kbd>.

Did the new title show up?

::::::::::::::::::::::::::

### Questions, Objectives, Keypoints

These are three blocks that live at the top and bottom of the episodes. 

1. `questions` are displayed at the beginning of the episode to prime the
learner for the content
2. `objectives` are the learning objectives for an episode and are
displayed along with the questions
3. `keypoints` are displayed at the end of the episode to reinforce the
objectives

They are formatted as [pandoc fenced div sections][fenced-divs], which we will
explain in the next section:

```markdown
---
title:
teaching:
exercises:
---

:::::: questions
 - question 1
 - question 2
::::::

:::::: objectives
 - objective 1
 - objective 2
::::::

<!-- EPISODE CONTENT HERE -->

:::::: keypoints
 - keypoint 1
 - keypoint 2
:::::::
```


## Editing an episode: Callout blocks

One of the key elements of our lessons are our callout blocks that give learners
and instructors a bold visual cue to stop and consider a caveat or exercise. To
create these blocks, we use [pandoc fenced-divs][fenced-divs]. These are similar
to code fences in which they start with at least three colons and end with at
least three colons. For example, to create a callout block, we would do this:

```markdown
::: callout
This is a callout block. It contains three colons
:::
```

::: callout
This is a callout block. It contains three colons
:::

However, it may be difficult sometimes to keep track of a section if it's only
delimited by three colons. To alleviate this, we recommend creating blocks with
enough colons that can easily distinguish a section from a heading or code block:

```markdown
::::::::::::::::::::::::::::::::::::::::::::::: testimonial
I'm **really excited** for the _new template_ when it arrives :grin:.

--- Toby Hodges
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
```

::::::::::::::::::::::::::::::::::::::::::::::: testimonial
I'm **really excited** for the _new template_ when it arrives :grin:.

--- Toby Hodges
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::: callout

That's right, we can use emojis in the new template! :100: :tada:

:::::::::::::::::::::::::::::::::::::::::::::::::::::::

## Exercises/Challenges

the method of creating callout blocks with fences can help us create solution
blocks nested within challenge blocks. Much like a [toast
sandwich](https://en.wikipedia.org/wiki/Toast_sandwich), we can layer blocks
inside blocks by adding more layers. For example, here's how I would create a
single challenge and a single solution:

```markdown
::::::::::::::::::::::::::::::::::::: challenge

## Chemistry Joke

Q: If you aren't part of the solution, then what are you?

:::::::::::::::: solution

A: part of the precipitate

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::
```

::::::::::::::::::::::::::::::::::::: challenge

## Chemistry Joke

Q: If you aren't part of the solution, then what are you?

:::::::::::::::: solution

A: part of the precipitate

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

To add more solutions, you close the first solution and add more text:

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Can you do it?

What is the output of this command?


```r
paste("This", "new", "template", "looks", "good")
```

:::::::::::::::::::::::: solution 

## Output
 

```{.output}
[1] "This new template looks good"
```

:::::::::::::::::::::::::::::::::


## Challenge 2: how do you nest solutions within challenge blocks?

:::::::::::::::::::::::: solution 

You can add a line with at least three colons and a `solution` tag.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::



## Figures

To include figures, place them in the `episodes/fig` folder and reference them 
directly like so:

```markdown
![Hex sticker for The Carpentries](fig/carpentries-hex-blue.svg)
```
![Hex sticker for The Carpentries](fig/carpentries-hex-blue.svg)

If your lesson uses R, they will be auto-generated and linked. You can use
`fig.alt` to include alt text


```r
pie(
  c(Sky = 78, "Sunny side of pyramid" = 17, "Shady side of pyramid" = 5), 
  init.angle = 315, 
  col = c("deepskyblue", "yellow", "yellow3"),
  border = FALSE
)
```

<img src="fig/episodes-rendered-pyramid-1.png" title="pie chart illusion of a pyramid" alt="pie chart illusion of a pyramid" style="display: block; margin: auto;" />


## Math

One of our episodes contains $\LaTeX$ equations when describing how to create
dynamic reports with {knitr}, so we now use mathjax to describe this:

`$\alpha = \dfrac{1}{(1 - \beta)^2}$` becomes: $\alpha = \dfrac{1}{(1 - \beta)^2}$

Cool, right?

:::::::::::::::: keypoints :::::::::::::::::::::

- Use `.Rmd` files for lessons even if you don't need to generate any code
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[pandoc-md]: https://pandoc.org/MANUAL#pandocs-markdown
[fenced-divs]: https://pandoc.org/MANUAL#divs-and-spans
[basic-syntax]: https://www.markdownguide.org/basic-syntax
[extended-syntax]: https://www.markdownguide.org/extended-syntax/

<!-- Please do not delete anything below this line -->


[cc-by-human]: https://creativecommons.org/licenses/by/4.0/
[cc-by-legal]: https://creativecommons.org/licenses/by/4.0/legalcode
[ci]: https://communityin.org/
[coc-reporting]: https://docs.carpentries.org/topic_folders/policies/incident-reporting.html
[coc]: https://docs.carpentries.org/topic_folders/policies/code-of-conduct.html
[concept-maps]: https://carpentries.github.io/instructor-training/05-memory/
[contrib-covenant]: https://contributor-covenant.org/
[contributing]: {{ repo_url }}/blob/{{ source_branch }}/CONTRIBUTING.md
[cran-checkpoint]: https://cran.r-project.org/package=checkpoint
[cran-knitr]: https://cran.r-project.org/package=knitr
[cran-stringr]: https://cran.r-project.org/package=stringr
[dc-lessons]: https://datacarpentry.org/lessons/
[email]: mailto:team@carpentries.org
[github-importer]: https://github.com/new/import
[jekyll-collection]: https://jekyllrb.com/docs/collections/
[jekyll-install]: https://jekyllrb.com/docs/installation/
[jekyll-windows]: https://jekyll-windows.juthilo.com/
[jekyll]: https://jekyllrb.com/
[jupyter]: https://jupyter.org/
[kramdown]: https://kramdown.gettalong.org/
[lc-lessons]: https://librarycarpentry.org/lessons/
[lesson-aio]: {{ relative_root_path }}{% link aio.md %}
[lesson-coc]: {{ relative_root_path }}{% link CODE_OF_CONDUCT.md %}
[lesson-example]: https://carpentries.github.io/lesson-example/
[lesson-license]: {{ relative_root_path }}{% link LICENSE.md %}
[lesson-mainpage]: {{ relative_root_path }}{% link index.md %}
[lesson-reference]: {{ relative_root_path }}{% link reference.md %}
[lesson-setup]: {{ relative_root_path }}{% link setup.md %}
[mit-license]: https://opensource.org/licenses/mit-license.html
[morea]: https://morea-framework.github.io/
[numfocus]: https://numfocus.org/
[osi]: https://opensource.org
[pandoc]: https://pandoc.org/
[paper-now]: https://github.com/PeerJ/paper-now
[python-gapminder]: https://swcarpentry.github.io/python-novice-gapminder/
[pyyaml]: https://pypi.python.org/pypi/PyYAML
[r-markdown]: https://rmarkdown.rstudio.com/
[rstudio]: https://www.rstudio.com/
[ruby-install-guide]: https://www.ruby-lang.org/en/downloads/
[ruby-installer]: https://rubyinstaller.org/
[rubygems]: https://rubygems.org/pages/download/
[styles]: https://github.com/carpentries/styles/
[swc-lessons]: https://software-carpentry.org/lessons/
[swc-releases]: https://github.com/swcarpentry/swc-releases
[training]: https://carpentries.github.io/instructor-training/
[workshop-repo]: {{ site.workshop_repo }}
[yaml]: https://yaml.org/

