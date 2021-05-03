---
title: "EXAMPLE: Using RMarkdown"
teaching: 5
exercises: 2
---

:::::::::::::::: questions :::::::::::::::::::::

- How do you write a lesson using RMarkdown and `{sandpaper}`?

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: objectives ::::::::::::::::::::

- Explain how to use markdown with the new lesson template
- Demonstrate how to include pieces of code, figures, and nested challenge blocks

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

This is the new Carpentries template. It is written in [RMarkdown][r-markdown],
which is a variant of Markdown that allows you to render code inside the
lesson. Please refer to the [lesson
example](https://carpentries.github.io/lesson-example) for full documentation.

What you need to know is that there are three block quotes required for a valid
Carpentries lesson template:

 1. `questions` These are displayed at the beginning of the episode to prime the
    learner for the content.
 2. `objectives` These are the learning objectives for an episode
 3. `keypoints` These are displayed at the end of the episode to reinforce the
    objectives.

### Code fences

Code fences written in standard markdown format will be highlighted, but not
evaluated:

```bash
echo '47 + 2' | bc
echo '47 * 2' | bc
```

Code fences written using R Markdown chunk notation will be highlighted and 
executed:


```r
magic <- sprintf("47 plus 2 equals %d\n47 times 2 equals %d", 47 + 2, 47 * 2) 
cat(magic)
```

```{.output}
47 plus 2 equals 49
47 times 2 equals 94
```

It's magic!

::::::::::::::: challenge ::::::::::::::::::::::

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

You can also include figures:


```r
pie(
  c(Sky = 78, "Sunny side of pyramid" = 17, "Shady side of pyramid" = 5), 
  init.angle = 315, 
  col = c("pink", "yellow", "yellow3"), 
  border = FALSE
)
```

<img src="fig/example-rendered-pyramid-1.png" title="plot of chunk pyramid" alt="plot of chunk pyramid" style="display: block; margin: auto;" />


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
