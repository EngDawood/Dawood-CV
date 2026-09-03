# Awesome-CV command reference

Argument order matters. If in doubt, grep `awesome-cv.cls` for the macro definition — it's the authoritative source.

## Document setup

```latex
\documentclass[11pt, a4paper]{awesome-cv}    % or letterpaper
\geometry{left=1.4cm, top=.8cm, right=1.4cm, bottom=1.8cm, footskip=.5cm}
\colorlet{awesome}{awesome-red}               % emerald, skyblue, red, pink, orange,
                                              % nephritis, concrete, darknight
% or: \definecolor{awesome}{HTML}{3E6D9C}
\setbool{acvSectionColorHighlight}{true}
\renewcommand{\acvHeaderSocialSep}{\quad\textbar\quad}
```

## Header (personal info)

```latex
\photo[circle,edge,left]{./path/to/photo}   % optional; shape: circle|rectangle, edge|noedge, left|right
\name{First}{Last}
\position{Job Title{\enskip\cdotp\enskip}Second Title}
\address{Full postal address}
\mobile{(+xx) xxx-xxxx}
\email{you@example.com}
\homepage{www.example.com}
\github{handle}
\linkedin{handle}
\gitlab{handle}
\twitter{@handle}
\x{handle}
\stackoverflow{id}{name}
\googlescholar{id}{display-name}
\quote{``An optional quote."}
```

Only the lines you actually want to render need to appear — comment the rest out.

Then in the body:

```latex
\makecvheader[C]     % C, L, or R
\makecvfooter{left}{center}{right}
```

## Sections

Every content section starts with:

```latex
\cvsection{Section Title}
\cvsubsection{Optional Subsection}
```

### Work experience & education

```latex
\begin{cventries}
  \cventry
    {Job Title}
    {Organization}
    {Location}
    {Sep. 2023 - Mar. 2024}
    {
      \begin{cvitems}
        \item {Bullet one.}
        \item {Bullet two.}
      \end{cvitems}
    }
  % ...more \cventry blocks
\end{cventries}
```

The trailing `{}` block can be empty if there are no bullets.

### Skills

```latex
\begin{cvskills}
  \cvskill{Category}{Comma, separated, list}
  \cvskill{Languages}{English, Arabic, French}
\end{cvskills}
```

### Honors, awards, certificates

```latex
\begin{cvhonors}
  \cvhonor
    {Award}       % or certificate name
    {Event}       % or issuer
    {Location}    % or credential ID (may be empty)
    {Year}
\end{cvhonors}
```

### Summary / free prose

```latex
\begin{cvparagraph}
  Free-form prose. Escape LaTeX specials.
\end{cvparagraph}
```

### Cover letter

Header block (before `\begin{document}`):

```latex
\recipient
  {Team Name}
  {Company\\Street\\City, State ZIP}
\letterdate{\today}
\lettertitle{Job Application for X Role}
\letteropening{Dear Ms. Last,}
\letterclosing{Sincerely,}
\letterenclosure[Attached]{Curriculum Vitae}
```

Body:

```latex
\makelettertitle
\begin{cvletter}
  \lettersection{About Me}
  ...
  \lettersection{Why Company?}
  ...
  \lettersection{Why Me?}
  ...
\end{cvletter}
\makeletterclosing
```

## LaTeX characters that must be escaped

| Character | Escape       |
| --------- | ------------ |
| `%`       | `\%`         |
| `&`       | `\&`         |
| `#`       | `\#`         |
| `$`       | `\$`         |
| `_`       | `\_`         |
| `{`       | `\{`         |
| `}`       | `\}`         |
| `~`       | `\textasciitilde{}` |
| `^`       | `\textasciicircum{}` |
| `\`       | `\textbackslash{}` |

Curly quotes: use `` `` `` for opening double, `''` for closing double, `` ` `` and `'` for single.

Dashes: `-` hyphen, `--` en-dash (date ranges), `---` em-dash.

Line break inside a `\cventry` bullet: end the sentence with `\\`, not a bare newline.
