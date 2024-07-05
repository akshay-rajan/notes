# LaTeX 

LaTeX is a typesetting system used for creating documents.
It is widely used for scientific and technical documents.
LaTeX is based on the TeX typesetting system developed by Donald Knuth.

#### 1. Document Structure
```latex
\documentclass{article}  % Defines the document class
\usepackage{package}     % Loads packages
\title{Title}            % Document title
\author{Author}          % Document author
\date{\today}            % Date (use \today for current date)
\begin{document}
\maketitle              % Creates the title
\tableofcontents        % Generates table of contents
\section{Section Title} % Section heading
\subsection{Subsection Title} % Subsection heading
\subsubsection{Subsubsection Title} % Subsubsection heading
\end{document}
```

#### 2. Text Formatting
```latex
\textbf{Bold text}        % Bold text
\textit{Italic text}      % Italic text
\underline{Underlined text} % Underlined text
\texttt{Typewriter text}  % Typewriter font
\emph{Emphasized text}    % Emphasized text (usually italic)
```

#### 3. Font Sizes
```latex
\tiny{Tiny text}          % Tiny text
\scriptsize{Script size text} % Script size text
\footnotesize{Footnote size text} % Footnote size text
\small{Small text}        % Small text
\normalsize{Normal size text} % Normal size text (default)
\large{Large text}        % Large text
\Large{Larger text}       % Larger text
\LARGE{Even larger text}  % Even larger text
\huge{Huge text}          % Huge text
\Huge{Huger text}         % Huger text
```

#### 4. Lists
- Unordered List
```latex
\begin{itemize}
  \item First item
  \item Second item
\end{itemize}
```
- Ordered List
```latex
\begin{enumerate}
  \item First item
  \item Second item
\end{enumerate}
```
- Description List
```latex
\begin{description}
  \item[Term] Description
\end{description}
```

#### 5. Mathematical Typesetting
- Inline Math
```latex
This is inline math: \( a^2 + b^2 = c^2 \).
```
- Display Math
```latex
\[ a^2 + b^2 = c^2 \]
```
- Equations
```latex
\begin{equation}
  E = mc^2
\end{equation}
```
- Fractions, Exponents, and Indices
```latex
\frac{a}{b}        % Fraction a/b
a^2                % a squared
a_i                % a subscript i
```

#### 6. Including Graphics
```latex
\usepackage{graphicx}       % Include this in the preamble
\begin{figure}[h]
  \centering
  \includegraphics[width=0.5\textwidth]{filename}
  \caption{Caption text}
  \label{fig:label}
\end{figure}
```

#### 7. Tables
```latex
\begin{table}[h]
  \centering
  \begin{tabular}{|c|c|}
    \hline
    Header1 & Header2 \\
    \hline
    Row1Col1 & Row1Col2 \\
    Row2Col1 & Row2Col2 \\
    \hline
  \end{tabular}
  \caption{Table caption}
  \label{tab:label}
\end{table}
```

#### 8. Cross-Referencing
```latex
\label{sec:label}      % Set a label for a section, figure, table, etc.
\ref{sec:label}        % Reference a label
\pageref{sec:label}    % Reference a page number of a label
```

#### 9. Citations and Bibliographies
- Using BibTeX
```latex
\bibliographystyle{plain}   % Bibliography style
\bibliography{bibliography} % Bibliography file
```
- Inline Citation
```latex
\cite{citationkey}          % Cite a reference
```

#### 10. Customizing Page Layout
- Margins
```latex
\usepackage[margin=1in]{geometry}  % Set margins
```
- Headers and Footers
```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\fancyhead[L]{Left Header}    % Left header
\fancyhead[C]{Center Header}  % Center header
\fancyhead[R]{Right Header}   % Right header
\fancyfoot[L]{Left Footer}    % Left footer
\fancyfoot[C]{Center Footer}  % Center footer
\fancyfoot[R]{Right Footer}   % Right footer
```

#### 11. Including Code
```latex
\usepackage{listings}       % Include this in the preamble
\begin{lstlisting}
  % Your code here
\end{lstlisting}
```

#### 12. Creating Presentations (Beamer)
```latex
\documentclass{beamer}
\begin{document}
\begin{frame}
  \frametitle{Frame Title}
  Content goes here.
\end{frame}
\end{document}
```

#### 13. Common Commands and Environments
- Comments
```latex
% This is a comment
```
- Newline and Paragraph
```latex
\\ % Newline
\newline % Newline
\par % Start a new paragraph
```
- Horizontal Line
```latex
\hrulefill
```

### Example Document
```latex
\documentclass{article}
\usepackage{graphicx}
\usepackage{fancyhdr}
\usepackage{geometry}
\usepackage{amsmath}
\geometry{margin=1in}
\title{Sample Document}
\author{Author Name}
\date{\today}

\begin{document}
\maketitle
\tableofcontents
\newpage

\section{Introduction}
This is an introduction.

\section{Math Example}
Here is an inline math example: \( a^2 + b^2 = c^2 \). And a display math:
\[ E = mc^2 \]

\section{Figures}
\begin{figure}[h]
  \centering
  \includegraphics[width=0.5\textwidth]{example-image}
  \caption{Example Image}
  \label{fig:example}
\end{figure}

\section{Tables}
\begin{table}[h]
  \centering
  \begin{tabular}{|c|c|}
    \hline
    Column1 & Column2 \\
    \hline
    Data1 & Data2 \\
    Data3 & Data4 \\
    \hline
  \end{tabular}
  \caption{Example Table}
  \label{tab:example}
\end{table}

\end{document}
```
