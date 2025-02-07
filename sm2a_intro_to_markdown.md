STAT 540 - Seminar 2a: Introduction to R Markdown
================

- [Before you begin](#before-you-begin)
- [Attributions](#attributions)
- [Learning Objectives](#learning-objectives)
- [Part 1: What is R Markdown?](#part-1-what-is-r-markdown)
- [Part 2: Nuts and bolts of R Markdown (contains excerpts from Ch. 19
  of Happy Git and GitHub for the
  useR)](#part-2-nuts-and-bolts-of-r-markdown-contains-excerpts-from-ch-19-of-happy-git-and-github-for-the-user)
- [Header 1](#header-1)
- [Part 3: Sharing is caring on GitHub (contains excerpts from Ch. 19 of
  Happy Git and GitHub for the
  useR)](#part-3-sharing-is-caring-on-github-contains-excerpts-from-ch-19-of-happy-git-and-github-for-the-user)
- [Part 4: Final notes and some additional
  resources](#part-4-final-notes-and-some-additional-resources)
- [Part 5: Deliverable](#part-5-deliverable)

# Before you begin

Before you begin, you should accept the `seminar-02a` assignment through
invite link on Canvas, and follow the steps you learned in Seminar 1 to
clone the repo to your computer.

# Attributions

This seminar was originally developed by [Eric
Chu](https://github.com/echu113) with materials adapted from [Happy Git
and GitHub for the useR](http://happygitwithr.com/) by [Dr. Jenny
Bryan](https://github.com/jennybc) and [The Official Documentation on R
Markdown](http://rmarkdown.rstudio.com/). It was modified by Keegan
Korthauer.

# Learning Objectives

By the end of this seminar, you should

- Have a conceptual understanding of what R Markdown is and how it can
  be used to render an analysis presentation in various formats
  including GitHub Markdown
- Know the basics of the R Markdown syntax for the generation of
  headers, paragraphs, lists, links, and code chunks
- Be able to compose R Markdown documents displaying simple tables and
  graphs
- Be able to render an R Markdown document as GitHub Markdown and to
  push it to GitHub

# Part 1: What is R Markdown?

A very high level, abstract way to describe a markdown language is the
marriage between coding and word processing. It is simply a way to
present text and figures without the cumbersome copying, pasting,
dragging, and resizing routines required by a word processor (I’m
looking at you, Microsoft Word).

Fun fact: all of the seminars in this course were created using R
Markdown :D.

Specifically, R Markdown is a language that allows you to embed R code
directly into a document to present text, equations, data tables,
figures, and images. This way, you can seamlessly integrate presentation
with analyses, saving countless hours and lots of frustration.

An R Markdown file has the `.Rmd` file suffix. An .Rmd file is a
**source** file, and can be rendered into various **output** file types:
a PDF (.pdf), Microsoft Word (.doc), HTML (html), or GitHub Markdown
(.md) documents, and a range of other formats. I know, exciting. We will
primarily work with GitHub Markdown outputs.

Yet, unfortunately, as with anything in the world, the more powerful
something is, the deeper its learning curve will be. In this seminar, we
will go through the nuts and bolts of creating and rendering an R
Markdown file. We will go through the basic features such as rendering
text and simple data tables and graphs. Then we will demonstrate how R
Markdown can be used for presenting and sharing analyses on GitHub,
making it an incredibly powerful tool for practicing reproducible
science.

Watch this [introductory video](https://vimeo.com/178485416).

# Part 2: Nuts and bolts of R Markdown (contains excerpts from [Ch. 19 of Happy Git and GitHub for the useR](http://happygitwithr.com/rmd-test-drive.html))

## Create an .Rmd file

We will author an R Markdown document and render it to HTML.

We are modelling “walk before you run” here. It is best to increase
complexity in small increments. We test our system’s ability to render
the “hello world” of R Markdown documents before we muddy the waters
with our own, probably buggy, documents.

In RStudio, go to: File -\> New File -\> R Markdown…

- Give it an informative title. This will appear in the document but
  does not necessarily have anything to do with the file’s name. But
  ideally the title and filename should be related! Why confuse
  yourself? The title is for human eyeballs, so it can contain spaces
  and punctuation. The filename is for humans and computers, so it
  should have similar words in it but no spaces and no punctuation.
- Accept the default Author or edit if you wish.
- Accept the default output format of HTML (we can change this later).
- Click OK.

Save this document to a reasonable filename and location. The filename
should end in .Rmd or .rmd. Save in the top-level of this RStudio
project and Git repository, that is also current working directory.
Trust me on this and do this for a while.

You might want to commit here, so you can see what’s about to change…

Click the “Knit” button or do File -\> Knit Document. See screenshot.

<figure>
<img src="images/knit_button.png" alt="Knit button" />
<figcaption aria-hidden="true">Knit button</figcaption>
</figure>

You might get prompted to install dependencies. If so, agree and
continue.

RStudio should display a preview of the resulting HTML in the Viewer
pane. You can see that the auto generated .Rmd file contains a quick
demo of text, a data table, and a scatter plot.

<figure>
<img src="images/knitted_html.png" alt="Knitted html" />
<figcaption aria-hidden="true">Knitted html</figcaption>
</figure>

Also look at the file browser. You should see the R Markdown document,
i.e. `first-markdown.Rmd` (or whatever you named it) AND the resulting
HTML file `first-markdown.html`.

Congratulations, you’ve just made your first reproducible report with R
Markdown.

You might want to commit here.

## Content structure

Take a look at your auto-generated .Rmd file. An R Markdown file can
have three “types” of text in general.

### YAML

The first is the YAML section containing configurations for the file.
This section looks like this:

    ---
    title: "My First R Markdown File"
    author: "Jane Doe"
    date: "24/01/2022"
    output: html_document
    ---

Feel free to change the title and author names and see what results in
your rendered report. Quick tip: you can stamp the current time on your
report by doing so:

``` eval
date: "`r format(Sys.time(), '%d %B, %Y')`"
```

We will talk about the output option later, when we integrate with
GitHub. Briefly, this is how you can get R Markdown to render into
various different document formats.

### Code Chunks

R code can be directly embedded into an .Rmd file and will be executed
during rendering. The result of the code would be printed into resulting
report.

Code is embedded in “code chunks” like so:

    ```{r, eval=TRUE}
    summary(cars)
    ```

This is how that data table and plot in the demo .Rmd file was rendered
in the html!

### Text

Finally, any text that is outside of YAML or an R code chunk is rendered
as Markdown text. Mostly, this is plain text, but with special syntax
for headers, bold/italic font, displaying images, tables, etc. This is
discussed in the next section.

## Markdown syntax

Here we demo a few commonly used features of Markdown for rendering
text. These apply to Markdown documents (.md) as well as the text in R
Markdown documents (.Rmd). Try them out yourself.

### Headers

Rmd Input:

    # Header 1
    ## Header 2
    ### Header 3
    #### Header 4

Output:

# Header 1

## Header 2

### Header 3

#### Header 4

### Lists

Rmd Input:

    * Fruits
        * apples
        * bananas
        * grapes
    * Vegetables
        + carrots
        + broccoli

    scary

    1. ocelots
    1. bears
    1. tigers

    Not scary

    1. elephants
    2. monkeys
    3. rabbits

Output:

- Fruits
  - apples
  - bananas
  - grapes
- Vegetables
  - carrots
  - broccoli

scary

1.  ocelots
2.  bears
3.  tigers

not scary

1.  elephants
2.  monkeys
3.  rabbits

### Link

Rmd Input:

`[This is a link to GitHub](https://github.com/)`

Output:

[This is a link to GitHub](https://github.com/)

### Image

Rmd Input:

    ![This is an image of a puppy](https://raw.githubusercontent.com/STAT540-UBC/seminar-02a/refs/heads/main/images/gettyimages-991380826-612x612.jpg)

Output:

<figure>
<img
src="https://raw.githubusercontent.com/STAT540-UBC/seminar-02a/refs/heads/main/images/gettyimages-991380826-612x612.jpg"
alt="This is an image of a puppy" />
<figcaption aria-hidden="true">This is an image of a puppy</figcaption>
</figure>

## The cheatsheet

Now that you have some taste of what R Markdown can do… here is [The R
Markdown Cheat
Sheet](https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf)

This is a document that covers a variety of R Markdown use cases.
Hopefully, this is a valuable resource that will follow you for many
more years to come!

## Go crazy!

Go ahead and spend 10 minutes to explore the different features in R
Markdown. Keep knitting, early and often, to see your changes rendered.

# Part 3: Sharing is caring on GitHub (contains excerpts from [Ch. 19 of Happy Git and GitHub for the useR](http://happygitwithr.com/rmd-test-drive.html))

Remember the last seminar on Git? Remember how README.md was rendered on
GitHub? Notice its file suffix “.md”.

The magical process that turns your R Markdown to HTML is like so:
`first-markdown.Rmd` –\> `first-markdown.md` –\> `first-markdown.html`.
Note the intermediate markdown, `first-markdown.md`. By default RStudio
discards this, but you might want to hold on to that markdown.

Why? GitHub gives very special treatment to markdown files. They are
rendered in an almost HTML-like way. This is great because it preserves
all the charms of plain text but gives you a pseudo-webpage for free
when you visit the file in the browser. In contrast, HTML is rendered as
plain text on GitHub and you’ll have to take special measures to see it
the way you want.

In many cases (e.g. for assignments in this class), you only want the
markdown. In that case, we switch the output format to
`github_document`. This means render will be `first-markdown.Rmd` –\>
`first-markdown.md`, where `first-markdown.md` is GitHub-flavored
markdown. If you still want the HTML but also the intermediate markdown,
there’s a way to request that too.

Output format is one of the many things we can control in the YAML
frontmatter – the text at the top of your file between leading and
trailing lines of —.

You can make some changes via the RStudio IDE: click on the “gear” in
the top bar of the source editor, near the “Knit HTML” button. Select
“Output options” and go to the Advanced tab and check “Keep markdown
source file.” Your YAML should now look more like this:

    ---
    title: "My First R Markdown File"
    author: "Jane Doe"
    date: "24/01/2022"
        output:
          html_document:
            keep_md: true
    ---

You should have gained the line `keep_md: true`. You can also simply
edit the file yourself to achieve this.

In fact this hand-edit is necessary if you want to keep only markdown
and get GitHub-flavored markdown. In that case, make your YAML look like
this:

    ---
    title: "My First R Markdown File"
    author: "Jane Doe"
    date: "24/01/2022"
    output: github_document
    ---

This is how you should specify the output of your assignment Rmds. Save!

You might want to commit here.

Render via “Knit” button.

Now revisit the file browser. In addition to `first-markdown.Rmd`, you
should now see `first-markdown.md`. If there are R chunks that make
figures, the usage of markdown output formats will also cause those
figure files to be left behind in a sensibly named sub-directory,
`first-markdown_files`.

If you commit and push `first-markdown.md` and everything inside
`first-markdown_files`, then anyone with permission to view your GitHub
repo can see a decent-looking version of your report by viewing the .md
file on GitHub. Cool!

If your output format is html_document, you should still see
`first-markdown.html`. If your output format is github_document and you
see `first-markdown.html`, that’s leftover from earlier experiments.
Delete that. It will only confuse you later.

You might want to commit here.

Now, push the current state to GitHub.

Go visit it in the browser.

Do you see the modifications and new file(s)? Your Rmd should be
modified (the YAML frontmatter changed). And you should have gained at
least, the associated markdown file.

Visit the markdown file and compare to our previous HTML.

Do you see how the markdown is much more useful on GitHub? **Internalize
that**.

# Part 4: Final notes and some additional resources

Final recommendations (excerpt from [Ch. 19 of Happy Git and GitHub for
the useR](http://happygitwithr.com/rmd-test-drive.html)):

Make sure RStudio and the rmarkdown package (and its dependencies) are
up-to-date. In case of catastrophic failure to render R Markdown,
consider that your software may be too old. RStudio is actively
developed, so you’ll want a current version of RStudio to enjoy all the
latest features and conveniences.

Check your working directory. It’s going to break your heart as you
learn how often your mistakes are really mundane and basic. Ask me how I
know. When things go wrong consider: \* What is the working directory?
\* Is that file I want to read/write actually where I think it is?

Drop these commands into R chunks to check the above: \* getwd() will
display working directory at run time. If you monkeyed around with
working directory with, e.g., the mouse, maybe it’s set to one place for
your interactive development and another when “Knit HTML” takes over? \*
list.files() will list the files in working directory. Is the file you
want even there?

Here are some resources in case you want to learn more.

- [The Official Documentation on R
  Markdown](http://rmarkdown.rstudio.com/)
- [Ch. 19 of Happy Git and GitHub for the
  useR](http://happygitwithr.com/rmd-test-drive.html)
- [The R Markdown Cheat
  Sheet](https://raw.githubusercontent.com/rstudio/cheatsheets/main/rmarkdown-2.0.pdf)
- [Other cool HTML options to
  check](https://bookdown.org/yihui/rmarkdown/html-document.html)

# Part 5: Deliverable

**To submit for credit**: If you’ve been following along so far, and
have a successfully knitted Rmd and GitHub Markdown file, you’ve
completed the deliverable. Just make sure to commit & push the required
files before the deadline so your assignment can be marked!

To recap, here’s a summary of the steps required, starting from the top:

1.  After you accept the assignment and clone your `seminar-02a` repo,
    add an .Rmd file.
2.  Make modifications as you see fit, and try out some Rmd
    options/features! For example, add an image, some R code, a plot,
    some headers, text, etc.
3.  Knit your Rmd to a GitHub Markdown document.
4.  Follow the [Submission
    Instructions](https://stat540-ubc.github.io/submission_guide) to
    submit the Rmd, knitted GitHub Markdown file, and any figure out
    output files (save, commit, push to GitHub, submit repo URL on
    Canvas).
