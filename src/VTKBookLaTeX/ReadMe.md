# VTK TextBook

## Introduction

These LaTeX files generate the VTK textbook as a PDF. **lualatex** and **biber** are used to generate the PDF.

The master document is  `VTKTextBook.tex`.

The process is documented in these scripts:

- `MakeDocument.bash` and `MakeDocument.cmd`.
- `Clean.bash` and `Clean.cmd`.

If figures have changes or you want to synchronize with the test examples run `ImportFigures.py` before `MakeDocument.bash` or `MakeDocument.cmd`

Running `MakeDocument` will generate the PDF.

## Editors used

[TexStudio](https://www.texstudio.org/) is used to edit/build the document.

if setting up TexStudio, remember to go to  **Configure TeXstudio|Build** and change the **Default Compiler** to `LuaLaTeX` and the **Default Bibliography Tool** to `Biber`.

[JabRef](http://www.jabref.org/) is used to maintain the bibliography.

## Procedure for adding/editing chapters

1. When starting a chapter, copy the relevant figures across from `src/VTKBook/Figures` into `src/VTKLaTeX/Figures`. After that just add figures into `src/VTKLaTeX/Figures`.

2. Do the bibliography at the end of the chapter using JabRef (load the existing `Bibliography.bib` first) and then do the Bibliographic Notes section to confirm all references are correct.

3. Where examples exist in https://lorensen.github.io/VTKExamples/site/VTKBookFigures/ these are added to  `src/VTKLaTeX/Figures` and  `src/VTKLaTeX/ImportFigures.py` is updated with the figure name and the path to the testing image. Update the variable
 `figs` with the new information. Running this script will update all the figures that correspond to the test examples.

4. If there is no drawing or figure available th scrape it from the original pdf and place it in  `src/VTKLaTeX/Figures/Scraped`. When better images become available they are placed into  `src/VTKLaTeX/Figures` and the corresponding image in  `src/VTKLaTeX/Figures/Scraped` is removed.

5. For equations use Bernard's excellent work in `Equations.txt` with one minor change, instead of `\vec{v}` use `\overrightarrow{v\ }` to improve appearances. At the end of each equation you need to add the following line:

    ```
    \myequations{Description of the Equation}
    ```
    This means the equation listings will have a short description for each equation.

6. For code listings add a short description. See Chapter 12 for examples.

7. In doing the chapter you will find references to pages and sections in other chapters. As these occur, add the relevant labels into the other chapters. 

## Indexing
When indexing make sure all sections/subsections/subsubsections when indexed use a page range.

```
\section{some section}
\index{some section|(}
    ... lots of text ...
\index{some section|)}
```

Where an index is in a listing i.e in `\begin{lstlisting} ... \end{lstlisting}` it must be escaped so add `escapechar=\$`for **C++** and `escapechar=\%` for **Tcl**, then escape the `\index{...}` command as follows. For **C++**: `$\index{...}$` and for **Tcl**:  `%\index{...}%`


## ToDo

Here we list tasks that need to be done.

### General

 1. Create a script to copy and rename the VTKExamples test files into the Figures dub directory. See `src/VTKLaTeX/Figures/ReadMe.md` for a list of files chapter by chapter. This script will need to be callable from `Admin/ScrapeRepo` in the section **# Copy VTKBookLaTeX files**.

 2. Better versions of the files in `Figures/Scraped` will be needed for publication quality. When a new version is made it should go into `Figures` and the correspond one in `Fiugures/Scraped` removed.

 3. Figures will need adjustment.

 4. Figures in `Figures` will need to be reviewed and better versions provided.

 5. Improve layout.
