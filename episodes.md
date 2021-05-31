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

- Practise creating a new episode with R
- Understand the required elements for each episode
- Understand pandoc-flavored markdown
- Demonstrate how to include pieces of code, figures, and nested challenge blocks

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

An episode[^episodes] is an individual unit of a lesson that focuses on a
single topic with clear questions, objectives, and key points. If a lesson goal
is to teach you about using git, an individual episode would teach you how to
inspect the status of a git repsitory. The idea behind the name "episode" is
the thought that each one should last about as long as an episode for an
television series.

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
a lesson [^worry]

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

This will create a new episode in the episodes folder called
"02-next-episode.Rmd".  If you already have your episode schedule set in
`config.yaml`, then this episode will not be rendered in the template and will
remain a draft until you add it to the schedule. Next, we will show how you can
add a title and other elements to your episode.

:::::::::::::::::::::::::::::::: callout

### What is the `.Rmd` extension?

You might notice that the new episode has the extension of `.Rmd` instead of 
`.md`. This is R Markdown, an extension of markdown that allows us to insert
special code fences that can execute R code and automatically produce output
chunks with controls of how the output and input are rendered in the document. 

For example, this markdown code fence will not produce any output, but it is
valid for both Markdown and R Markdown. 

````
```r
print("hello world!")
```
````

```r
print("hello world!")
```

But when I open the fence with ```` ```{r} ```` then it becomes an R Markdown
code fence and will execute the code inside the fence:

````
```{r}
print("hello world!")
```
````


```r
print("hello world!")
```

```{.output}
[1] "hello world!"
```

Note that it is completely optional to use these special code fences! 

:::::::::::::::::::::::::::::::::::::::::

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

They are formatted as [pandoc fenced divisions][fenced-divs], which we will
explain in [the next section](#callout-blocks):

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
::::::
```


## Editing an episode: Callout blocks {#callout-blocks}

One of the key elements of our lessons are our callout blocks that give learners
and instructors a **bold visual cue** to stop and consider a caveat or exercise.
To create these blocks, we use [**pandoc fenced divisions, aka
_'fenced-divs'_**][fenced-divs], which are colon-delimited sections similar to 
code fences that can instruct the markdown interpreter how the content should be
styled. 

For example, to create a `callout` block, we would use *at least three colons*
followed by the `callout` tag (the tag designates an open fence), add our
content after a new line, and then close the fence with *at least three colons*
and no tag (which designates a closed fence):

```markdown
::: callout
This is a callout block. It contains at least three colons
:::
```

::: callout
This is a callout block. It contains at least three colons
:::

However, it may be difficult sometimes to keep track of a section if it's only
delimited by three colons. Because [the specification for fenced-divs require
*at least* three colons][fenced-divs], it's possible to include more to really
differentiate between these and headers or code fences:

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

Even better, you do not have to worry about counting colons! It doesn't matter
how many colons you put for the opening and closing fences, all that matters is
you can visually see that the fences match. 

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


Now, here's a real challenge for you

:::::::::::::::::::::::::::::::::::::: challenge

Is the following fenced-div valid? Why?

```markdown
::::::::::::::::::::: my-class
This is a block of my class
:::
```

::::::::::::::::::::::: solution

Yes! It is a valid fenced div for the following reasons:

1. The opening fence has &ge;3 colons
2. The opening fence has a class designation
3. The closing fence is on its own line and has &ge;3 colons

:::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::::::


## Figures

To include figures, place them in the `episodes/fig` folder and reference them 
directly like so using standard markdown format, with one twist: add an `alt`
attribute at the end to make it accessible like this: 
`![caption](image){alt='alt text'}`.


```markdown
![Hex sticker for The Carpentries](fig/carpentries-hex-blue.svg){alt="blue
hexagon with The Carpentries logo in white and text: 'The Carpentries'"}
```

![Hex sticker for The Carpentries](fig/carpentries-hex-blue.svg){alt="blue
hexagon with The Carpentries logo in white and text: 'The Carpentries'"}

:::::::::::::::::::::::::::: discussion

### Accessibility Point: Alternative Text (aka alt-text)

Alternative text (alt text) is a very important tool for making lessons
accessible. If you are unfamiliar with alt text for images, [this primer on alt
text gives a good rundown of what alt text is and why it matters][alt-text]. In
short, alt text provides a short description of an image that can take the place
of an image if it is missing or the user is unable to see it.

::::::::::::::::::::::::::::::::::::::

If your lesson uses R, some images will be auto-generated from evaluated code
chunks and linked. You can use `fig.alt` to include alt text. [This blogpost has
more information about including alt text in RMarkdown 
documents](https://blog.rstudio.com/2021/04/20/knitr-fig-alt/). In addition, you
can also use `fig.cap` to provide a caption that puts the picture into context
(but take care to not be redundant; screen readers will read both fields). 


```r
pie(
  c(Sky = 78, "Sunny side of pyramid" = 17, "Shady side of pyramid" = 5), 
  init.angle = 315, 
  col = c("deepskyblue", "yellow", "yellow3"),
  border = FALSE
)
```

<div class="figure" style="text-align: center">
<img src="fig/episodes-rendered-pyramid-1.png" alt="pie chart illusion of a pyramid"  />
<p class="caption">Sun arise each and every morning</p>
</div>

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

[pandoc-md]: https://pandoc.org/MANUAL#pandocs-markdown
[fenced-divs]: https://pandoc.org/MANUAL#divs-and-spans
[basic-syntax]: https://www.markdownguide.org/basic-syntax
[extended-syntax]: https://www.markdownguide.org/extended-syntax/
[alt-text]: https://axesslab.com/alt-texts/
[^episodes]: The designation of "episode" will likely change. Throught UX
  testing, it's clear that calling these lesson units "episodes" is confusing,
  even for people who have been in The Carpentries for several years. The
  current working proposal is to call these "chapters". 
[^worry]: Do not worry if you aren't comfortable yet, that's what we will show
  you in this episode!

