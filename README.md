# Computational Linguistics journal R Markdown template
_Jayden Macklin-Cordes_  
_Last update: 18 May 2018_

This is an R package for authoring *Computational Linguistics* journal articles in R Markdown. It provides an R Markdown template for producing complete manuscripts in the *Computational Linguistics* style. Enjoy the full functionality and readability of R Markdown while authoring your manuscript, and knit directly into a properly-formatted, submission-ready document.

The LaTeX class and bst files are up-to-date as of 18 May 2018. I'll endeavour to keep it up-to-date but no promises.

Please keep in mind this package is unofficial and not associated or endorsed in any way by the Association for Computational Linguistics. It is purely my own project for making *Computational Linguistics* articles easier to write in R Markdown. Anyone using this template for their own work takes full responsibility conforming with the journal submission format and guidelines.

# Installation

Download the package `devtools`, if you don't have it already.

Install the package in the R console with `devtools::install_github("JaydenM-C/CLtemplate")`

When opening a new R Markdown document in RStudio via `New file > R Markdown...`, the regular dialogue box will pop up. Navigate to `From template`, and you should see the option to select a template called `Computational Linguistics journal`. If you've just installed the package, you may need to restart RStudio before it will appear in the list.

# Usage

The Association for Computational Linguistics supplies a `CLV3` LaTeX document class, plus a bst file for styling references using the natbib package. This R Markdown template contains a range of variables listed in the YAML header specific to the CLV3 class. Most variables are optional and can be left blank or removed from the YAML header if preferred, although at least the name of at least one author must be specified. If and how each variable value is displayed in the document will depend on the particular class option (for example, the document header doesn't always display).

For a description of each variable, see the [CLV3 Class File Manual](http://cljournal.org/Docs/COLI-manual3.pdf). Of particular note is the first variable, `CL_style`. This is where class options for the CLV3 optionally can be specified. It can be left blank for a standard article style. Other options are *bookreview, brief, discussion, pubrec, shortpaper* and *manuscript*. *manuscript* can be used in conjunction with the others, for example `shortpaper,manuscript`. Again, see the [manual](http://cljournal.org/Docs/COLI-manual3.pdf) for a full description of these options.

One additional step is to specify the path to a bibliography file in .bib format. Note that the .bib extension must be included in the YAML header (unlike the LaTeX command `\bibliography{}` where the extension is optional). So `bibliography: references.bib` will work, but `bibliography: references` will not.

After filling in the appropriate details in the YAML header, the main body of the document can be written up in the usual R Markdown way. Be sure to consult the *Computational Linguistics* [submission guidelines](http://cljournal.org/submissions.html) and [style guidelines](http://cljournal.org/style.html).

_One quirk:_ Currently, if you do not specify any `contact_details` for an author, the document should still compile successfully, but it will add an asterisk by the author's name and insert a blank footnote where the contact details would have gone. See [this issue](https://github.com/JaydenM-C/CLtemplate/issues/1) for details.

# Referencing and acknowledgements (important!)

The biggest difficulty I have found with producing CL style documents in R Markdown is accurate formatting of the acknowledgements and bibliography. This is because the body of *Computational Linguistics* articles is in a single column format, while the acknowledgements and references following the article are placed in a two-column section. Switching between single- and double-column sections in R Markdown is not quite as simple as perhaps it could be.

The most straightforward option would be to insert a raw LaTeX command `\starttwocolumn` in the body of the markdown document, before acknowledgements and references (this is the same command used in the TeX file for the [CLV3 Class File Manual](http://cljournal.org/Docs/COLI-manual3.pdf)). Unfortunately, this command isn't recognised by R Markdown for some reason. Manual insertion of `\starttwocolumn` in the TeX file produced by Pandoc after compiling seems to produce undesirable results as well.

An alternative is to use the `multicol` package to create a two-column environment in the R Markdown document, using `\begin{multicols}{2}` and `\end{mulitcols}`. However, anything inside this environment will be interpreted as raw LaTeX, so you won't be able to use any markdown commands nor specify the placement of your bibliography with the usual R Markdown workaround (inserting a line of raw HTML, `<div id="refs"></div>)`.

This leaves two options:

### Using natbib commands for in-text citations (recommended)

1. Leave the default YAML setting `natbib_citations: true`.
2. For all in-text citations, use the regular natbib commands (raw LaTeX). See the [natbib guide](https://www.cs.ox.ac.uk/people/gary.mirams/BibTex/natbib.pdf) for details.
3. Optionally, fill in any acknowledgements in the YAML `acknowledgements` field at the start of the document.
4. No need to put `# Acknowledgements` or `# References` headers in the R Markdown document. Knit the document and this is all taken care of.
5. You should now have a document with references and (optionally) acknowledgements all placed appropriately in a two-column format.

### Using regular markdown in-text citations

If you're really keen to use regular R Markdown-style commands for in-text citations, there is a workaround.

1. Set `natbib_citations: false`
2. Use regular R Markdown for all your in-text citations. Do not use any raw LaTeX commands for in-text citations.
3. Add `# Acknowledgements{-}` and `# References` headers to the bottom of the R Markdown document (the `{-}` leaves a section unnumbered. References sections are automatically unnumbered). Insert any acknowledgements here, in the body of the document, *not* in the YAML header (leave the YAML field blank).
4. You now have two choices:
   1. Easy but incorrect formatting (might be suitable for a draft, for example): Just insert the raw LaTeX command `\twocolumn` on its own line, above the Acknowledgements header. This will produce acknowledgements and references in a two column format, however it will also insert a page break between the end of the article and start of the acknowlegements---this looks fine enough, but it is not the correct *Computational Linguistics* style.
   2. Hacky but correct formatting: Knit the document as-is. Then, open up the resulting .tex file in your text editor of choice. Find the acknowledgements and references sections and insert a line containing `\begin{multicols}{2}` above and a line containing `\end{mulitcols}` after these sections. Finally, recompile the .tex file in your TeX compiler of choice (ShareLaTeX, TeXworks, etc.).

If you have a better solution, please open an 'issue' and propose it!

# In the event of problems

I expect this template will work great until it doesn't. If you get stuck, you can post an issue, but your best bet may be the following:

1. Fork this repository to create your own copy of the package, using the fork button on the top right of this page.
2. Dig into the file `cl-template.tex` and see if you can modify it in a way that suits your needs. You may wish to modify the name of the template in the `template.yaml` file.

For an overview of R Markdown templates, see [https://rmarkdown.rstudio.com/developer_document_templates.html]. I also found [this tutorial](http://ismayc.github.io/ecots2k16/template_pkg/) helpful. [This section](http://pandoc.org/MANUAL.html#using-variables-in-templates) of the Pandoc manual was also helpful for getting my head around how LaTeX templates for Pandoc work.
