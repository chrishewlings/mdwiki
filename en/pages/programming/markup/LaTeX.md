# LaTeX cheatsheet

## Bootstrapping

The following sets up a document with a title page, imports math functions, uses Arabic numeral page numbers:

```
\documentclass{article}

\usepackage{amsmath}
\usepackage[margin=0.75in]{geometry}

\title{<NAME>}
\date{<DATE>}


\begin{document}
	\pagenumbering{gobble}
	\maketitle
	\newpage
	\pagenumbering{arabic}
```

## Page size, orientation, margins, etc.

- `\usepackage[letterpaper, landscape, margin=2in]{geometry}` makes a landscape oriented 14"x8.5" with 2" margins. 
	+ 

## Sections

- `\section`, `\subsection`, `\subsubsection`, etc.
- Using `\tableofcontents` will create a TOC of the `\section`s of the document. 

## Content types

### Lists

|List type|LaTeX operator|
|---------|--------------|
|Bulleted list|`\begin{itemize}`|
|Numbered list|`\begin{enumerate}`|
|Labelled list|`\begin{description}`|

- Use `\item{}` for each entry. 

### Links & media

#### Pictures
- Requires `\usepackage{graphicx}`
- `\includegraphics[width=\linewidth]{boat.jpg}` will include an image called `boat.jpg` in the rendered output. 

#### Links

- `\href{...url...}{Link text}`

### Quotes

`\quote{<CONTENT>}`

## Inline Math

- Encapsulating a single formula in text:
	`This formula is $f(x) = x^2$`
- Writing an equation with equation reference numbers:
- ```
\begin{equation}
	1 + 2 = 3
\end{equation}
```

- Writing an equation with no reference number:
- ```
\begin{equation*}
	1 = 3 - 2
\end{equation*}
```

### Aligning equations

```
\begin{align*}
	1 + 2 &= 3\\
	1 &= 3 - 2
\end{align}
```
- Equations will be lined up to the `&`. The `\\` splits them with a newline.

### Operators, symbols, and variables



|Operator|LaTeX|
|--------|-----|
|x²|`x^{2}`|
|x₂|`x_{2}`|
|1/x|`\frac{1}{x}`|
|∫(1/3)x³|`\int^a_b \frac{1}{3}x^3`|
|√x|`\sqrt{x}`|
|∛x|`\sqrt[3]{x}`|
|∑nk=1|`$\sum_{k=1}^n$`|


|Symbol|LaTeX|
|------|-----|
| ≤ |`$\leq$`|
| ≥ |`$\geq$`|
| ≠ |`$\neq$`|
| ≈ |`$\approx$`|
| × |`$\times$`|
| ÷ |`$\div$`|
| ± |`$\pm$`|
| ′ |`$\prime$`
| ∞ |`$\inf$`|
| ¬ |`$\neg$`|
| ∧ |`$\wedge$`|
| ∨ |`$\vee$`|
| ⊃ |`$\supset$`|
| ⊂ |`$\subset$`|
| ∪ |`$\cup$`|
| ∩ |`$\cap$`|
| ∀ |`$\forall$`|
| ∃ |`$exists$`|
| ∈ |`$\in$`|
| → |`$\rightarrow$`|
| ⇒ |`$\Rightarrow$`|
| ⇔ |`$Leftrightarrow$`

|Variables|LaTeX|
|---------|-----|
|α|`$\alpha$`|
|β|`$\beta$`|
|γ|`$\gamma$`|
|δ|`$\delta$`|
|ϵ|`$\epsilon$`|
|ζ|`$\zeta$`|
|η|`$\eta$`|
|ε|`$\varepsilon$`|
|θ|`$\theta$`|
|ι|`$\iota$`|
|κ|`$\kappa$`|
|ϑ|`$\vartheta$`|
|λ|`$\lambda$`|
|μ|`$\mu$`|
|ν|`$\nu$`|
|ξ|`$\xi$`|
|π|`$\pi$`|
|ρ|`$\rho$`|
|σ|`$\sigma$`|
|τ|`$\tau$`|
|υ|`$\upsilon$`|
|ϕ|`$\phi$`|
|χ|`$\chi$`|
|ψ|`$\psi$`|
|ω|`$\omega$`|
|Γ|`$\Gamma$`|
|Δ|`$\Delta$`|
|Θ|`$\Theta$`|
|Λ|`$\Lambda$`|
|Ξ|`$\Xi$`|
|Π|`$\Pi$`|
|Σ|`$\Sigma$`|
|Υ|`$\Upsilon$`|
|Φ|`$\Phi$`|
|Ψ|`$\Psi$`|
|Ω|`$\Omega$`|




### Matrices

```
\left[
	\begin{matrix}
		1 & 0\\
		0 & 1
	\end{matrix}
\right]
```
- You can write a matrix without the `\left[` and `\right]`, but the brackets will not be scaled.
	+ Note: This also works for parentheses. 

## Tables 
```
\begin{table}[h!]
	\centering 
	\caption{Caption for the table.}
	\label{tab:table1}
	
	\begin{tabular}{l|c|r}
		1 & 2 & 3\\
    	\hline
    	a & b & c\\
	\end{tabular}
	
\end{table}
```
- `&` are used as field separators
- `\hline` is used to create a row separator. 
- `l|c|r` is to align the content left, centre, or right, respectively. 

## Footnotes
`\footnote{\label{<LABEL>}Hello world}`
- will make a footnote with the text `Hello World`, number it automatically, label it with `<LABEL>`
- `<LABEL>` above is important, beause you can later use the `\ref{<LABEL>}` command to refer back to them. 

## Code blocks and highlighting
- Basic code blocks can be written 'verbatim', using operator `\verb||`.

```
\usepackage{listings}
\usepackage{color}

\renewcommand\lstlistingname{Quelltext}

\lstset{ % General setup for the package
	language=Perl,
	basicstyle=\small\sffamily,
	numbers=left,
 	numberstyle=\tiny,
	frame=tb,
	tabsize=4,
	columns=fixed,
	showstringspaces=false,
	showtabs=false,
	keepspaces,
	commentstyle=\color{red},
	keywordstyle=\color{blue}
}

\begin{lstlisting}
	#!/usr/bin/perl
	use strict;
	use warnings;
	
	printf("%s", "Hello world");
\end{lstlisting}
```

- Use the `\lstlinputlisting{FILENAME}` command to read the content of source files directly into a lstlistings environment.

## Fancy stuff

- [Import CSV to tables](https://www.latex-tutorial.com/tutorials/advanced/latex-pgfplotstable/)
- [Plotting data to graphs](https://www.latex-tutorial.com/tutorials/advanced/latex-pgfplots/)
- [Vector graphics in LaTeX](https://www.latex-tutorial.com/tutorials/advanced/latex-tikz/)


