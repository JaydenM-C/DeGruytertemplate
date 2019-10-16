# De Gruyter R Markdown template
_Jayden Macklin-Cordes_  
_Last update: 14 October 2019_

This is an R package for authoring De Gruyter journal article and book manuscripts in R Markdown. It provides an R Markdown template for producing complete manuscripts in the De Gruyter style. Enjoy the full functionality and readability of R Markdown while authoring your manuscript, and knit directly into a properly-formatted, submission-ready document.

The LaTeX template files are up-to-date as of 14 October 2019. I'll endeavour to keep it up-to-date but no promises.

Please keep in mind this package is unofficial and not associated or endorsed in any way by De Gruyter. It is purely my own project for making *Linguistic Typology* journal articles easier to write in R Markdown. Anyone using this template for their own work takes full responsibility conforming with the journal submission format and guidelines.

# Latest news

16 Oct 2019: Note that this package is a work-in-progress. The book template has not been thoroughly tested. There is an outstanding issue with 'acknowledgement' and 'keywords' fields in the article template [see the issue here](https://github.com/JaydenM-C/DeGruytertemplate/issues/1). Please feel free to post an issue for any problems that arise and also help/propose solutions for existing issues.

# Installation

Download the package `devtools`, if you don't have it already.

Install the package in the R console with `devtools::install_github("JaydenM-C/DeGruytertemplate")`

When opening a new R Markdown document in RStudio via `New file > R Markdown...`, the regular dialogue box will pop up. Navigate to `From template`, and you should see the option to select a template called `De Gruyter article` or `De Gruyter book`. If you've just installed the package, you may need to load it with `library(DeGruytertemplate)` or restart RStudio before it will appear in the list.

# Usage

De Gruyter provides a LaTeX package for authoring manuscripts in De Gruyter style. The package can be downloaded at [https://www.degruyter.com/dg/page/production-for-authors]. And, actually, it's a very good idea to check out that page because it contains a good deal of other information on the De Gruyter house style.

There's also an Overleaf template for De Gruyter books and articles available at [https://www.overleaf.com/latex/templates/manuscript-template-for-walter-de-gruyter-books-and-journals].

When you create a new R Markdown file using one of the templates supplied by this package, you'll find it creates a directory containing essentially the same contents as the Overleaf template with a couple of differences. First, you'll only get the applicable LaTeX template file (either `article.tex` or `book.tex`), not both. Secondly, this template file is modified into a Pandoc template. Pandoc is the engine which converts your R Markdown file into LaTeX and then into a PDF, under the hood. This will be useful to know. Every R Markdown document you knit to PDF will go through one of these templates, but typically the template is quite hidden. With this package, the template is right there locally, so you can easily jump in and modify it for a particular document as the need arises. (This is a bit of a trade-off, since you'll have an extra file cluttering your working directory, but given how touchy large, complicated, academic documents can be, I think it's worthwhile)

One final note: It would be worth checking out [bookdown](https://bookdown.org/). This package enables easy stitching of multiple R markdown files so you can, for example, have one R markdown file per chapter and then stitch them all together into a book manuscript. The package also enables some missing functionality regarding crossreferences, which are likely to be useful even for single-document academic articles. [The documentation](https://bookdown.org/yihui/bookdown/) is really good (and would be beneficial to R Markdown novices, even if you don't end up using the bookdown package itself).

# In the event of problems

I expect this template will work great until it doesn't. If you get stuck, you can post an issue, but your best bet may be to dig into the `book.tex` or `article.tex` template files and see if you can work a solution.

If you're using [TinyTex](https://yihui.name/tinytex/) as your TeX distribution (which I recommend, by the way. Very easy, works well, and so much smaller than TeX Live). My experience is that some obscure LaTeX error messages end up just being the result of a missing package. Missing packages are meant to be installed automatically and normally are without issue but 🤷‍♂️. For example, I got an error message about fonts needing to be scalable, which, after some Googling, was fixed by installing the `cm-super` package (`tinytex::tlmgr_install("cm-super")`)

For an overview of R Markdown templates, see [https://rmarkdown.rstudio.com/developer_document_templates.html]. I also found [this tutorial](http://ismayc.github.io/ecots2k16/template_pkg/) helpful. [This section](http://pandoc.org/MANUAL.html#using-variables-in-templates) of the Pandoc manual was also helpful for getting my head around how LaTeX templates for Pandoc work.
