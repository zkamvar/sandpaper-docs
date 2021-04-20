---
title: "Lesson Deployment"
teaching: 5
exercises: 0
---

::::::::::::::::::::::::::::: questions

 - What is the two-step model of deployment?
 - How do we use the two-step model to provide PR audits?

:::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::: objectives

 - Understand the two-step model for lesson deployment
 - Understand the Pull Request Preview for generated lesson content

::::::::::::::::::::::::::::::::::::::::

## How we got here

Since 2016, [we have supported using RMarkdown in lessons][rmd-blog]. The 
benefits have been that authors no longer need to manually copy and paste 
output and graphs into their documents. We were even able to use continuous
integration to build the RMarkdown documents to markdown so that they would be
then deployed using Jekyll.

The downside to this model was that the maintainers would occasionally encounter
unexpected outputs from new contributions because there was either a syntax
error or [the R ecosystem had changed paradigms][r4-migration]. Moreover, people
would often edit the generated markdown file instead of the source RMarkdown
file, which would result in progress being lost because of a regenerated file.

## The two-step model of deployment

To alleviate the downsides of working with generated content, the new template
employs a two-step model of deployment when you run `sandpaper::build_lesson()`

1. Take any source files with content that needs to be interpreted (e.g. 
   RMarkdown and in the future Jupyter Notebooks) and **render them to markdown**
   in a staging area ignored by git. 
2. Apply the HTML style to the markdown files in the staging area to create the
   lesson website.

![Diagram showing the two-step model of lesson deployment](https://zkamvar.github.io/stunning-barnacle/img/local-flow.dot.svg)

All of the generated content lives in the `site/` folder, and importantly: it
is all cached and ignored by git. Ignoring generated content locally means that
the source of truth for these files is no longer dependent on the maintainer's
local setup. 

The reason we have this model is also for portability. It's because markdown
output is a lot easier to audit than HTML when something goes wrong, rendered
markdown can be transferred to other contexts (e.g. books or blogposts), and we
can swap out the generators without needing to rewrite the entire pipeline.

:::::::::::::: callout

### Did you know?

When the lesson is pushed to GitHub, all of the generated content IS stored in
separate branches so that we can provide a way for you to audit changes from 
pull requests. 

::::::::::::::::::::::

## On GitHub

On GitHub, we store generated content in two orphan branches called
`md-outputs` and `gh-pages` for the generated markdown and html, respectively. 
We use [GitHub Actions Workflows][gh-workflow] to build, validate, and deploy
our lessons on GitHub pages. If you use pure markdown lessons, you should notice
no significant changes to your workflow. 

These workflows are the source of truth for the lessons and will keep your 
lesson up-to-date with the latest version of the HTML template. 

If you use RMarkdown lessons, you will notice that for every pull request, a
GitHub bot comments on your pull requests informing you about what content has
changed and gives you a link to the differences between the current state of
the `md-outputs` branch and the proposed changes. 

The controls for these actions live in the `.github/` folder of your repository
and are currently maintained at 
<https://github.com/zkamvar/actions/tree/main/workflows#readme>. 

::::::::::::: callout

### Risk Management

Accepting generated content into lessons from anyone runs the risk of a security
breach by exposing secrets. To mitigate this risk, GitHub limits the scope of
what is possible inside a pull request so that we can check and render the 
content without risk of exploitation. Through this, we render and check the 
lesson inside the pull request with no privileges, check that the pull request
is valid (not malicious), and then create a temporary branch for an exploratory
preview, allowing the maintainer to audit the generated content before it gets
adopted into the curriculum. 

If the PR is invalid (e.g. the contributor spoofed a separate, valid PR, or
modified one of the github actions files), then the maintainer is alerted that
the PR is potentially risky.


![Workflow diagram for a pull request](https://raw.githubusercontent.com/zkamvar/stunning-barnacle/main/img/pr-flow.dot.svg)

::::::::::::::::::::

## Updating Your Workflows

The workflows are one of the few points in the new template where it needs to
be updated manually.

:::::::::::::::::: callout

### :crystal_ball: In the future

In the future, we will make this process easier by creating bots that will 
periodically provide pull requests that update these workflows. 

::::::::::::::::::::::::::::

  To update your workflows, you can use the following command in your
lesson:

```r
sandpaper::fetch_github_workflows()
```

After that, you can add and commit your changes and then push them to GitHub. 


:::::::::::::::::::::::::::::: keypoints

 - Lessons are built using a two-step process of caching markdown outputs and then building HTML from that cache
 - We use GitHub Actions to deploy and audit generated lesson content to their websites

::::::::::::::::::::::::::::::::::::::::


[rmd-blog]: https://software-carpentry.org/blog/2016/07/rmarkdown-new-template.html
[r4-migration]: https://carpentries.org/blog/2020/08/r-4-migration/
[gh-workflows]: https://docs.github.com/en/actions/ 
