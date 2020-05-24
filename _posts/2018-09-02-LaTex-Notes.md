---
title: LaTeX Notes
date: 2018-09-02 12:28:12 -0500
categories: [Tools]
tags: [latex]
---

## Learning Notes
Most of the latex notes are referenced in the book [LATEX Tutorials: A PRIMER](https://raw.githubusercontent.com/yuyang-yy/materials/master/ltxprimer-1.0.pdf)


## Error Log
1. Use \\\\ in a seperate line, and error appears. Do not use two backslashes in one single line.

## Notes
- There seems to be some difference between \\ and **enter**.

- Insert python code with highlighting.
Use the following to before `\begin{document}`.
	```latex
	% settings for python code
	\usepackage[utf8]{inputenc}
	\DeclareFixedFont{\ttb}{T1}{txtt}{bx}{n}{10} % for bold
	\DeclareFixedFont{\ttm}{T1}{txtt}{m}{n}{10}  % for normal
	\usepackage{color}
	\definecolor{deepblue}{rgb}{0,0,0.5}
	\definecolor{deepred}{rgb}{0.6,0,0}
	\definecolor{deepgreen}{rgb}{0,0.5,0}
	\usepackage{listings}
	\lstdefinestyle(PythonStyle){
		language=Python,
         	basicstyle=\ttm,
	     	otherkeywords={self},             % Add keywords here
          	keywordstyle=\ttb\color{deepblue},
          	emph={MyClass,__init__},          % Custom highlighting
          	emphstyle=\ttb\color{deepred},    % Custom highlighting style
          	stringstyle=\color{deepgreen},
          	frame=tb,                         % Any extra options here
          	showstringspaces=false            % 
  	}
	```
- Insert figures. [reference](https://www.latex-tutorial.com/tutorials/figures/)
	```latex
	\documentclass{article}
	\usepackage{graphix}
	\usepackage{subcaption}

	\begin{document}

		% insert one figure
		\begin{figure}[h!] % h means insert figures right here
			\includegraphics[width=\linewidth]{figures/rating_per_claim.jpg}
			\caption{Rating Per Claim}
			\label{fig:rating_per_claim}
		\end{figure}

		% insert two figures
		\begin{figure}[h!]
			\centering
			\begin{subfigure}[b]{0.4\linewidth}
				\includegraphics[width=\linewidth]{figures/age_kernel.png}
				\caption{Age of driver}
				\label{fig:age_kernel}
			\end{subfigure}
			\begin{subfigure}[b]{0.4\linewidth}
				\includegraphics[width=\linewidth]{figures/age_kernel.png}
				\caption{Annual Income}
				\label{fig:annual_income_kernel}
			\end{subfigure}
			\caption{Kernel density curves}
			\label{fig:kernel1}
		\end{figure}
	\end{document}
	```

- Insert tables.
	```
	\begin{table}[h!]
		\begin{center}
			\caption{New Feature Performace Boost}
			\label{tab:performance_boost}
			\begin{tabular}{|c|c|} 
				\hline
				\textbf{Feature} & \textbf{Performance Boost}\\
				\hline
				Latitude and longitude & 0.001\\
				Rating Per Claim & 0.0017 \\
				Interest Rate & 0.0007\\
				Count of missing values & 0.0004\\
				\hline
			\end{tabular}
		\end{center}
	\end{table}
	```

- Insert a new page.
	```
	\newpage  % it will be ignored in between float figures and tables.

	\clearpage % if this new page is in between float figures and tables, then use this command.
	```

- Add appendix.
	```
	\usepackage[toc,page]{appendix}

	\begin{appendices}
		\section{Figures}
		
		\section{Tables}

		\section{Codes}
	\end{appendices}
	```

- Insert an algorithm.
	```
	\usepackage{algpseudocode}
	\usepackage{algorithm}

	\begin{algorithm}	
		\caption{Algorithm for Optimal threshold}
		\label{alg:threshold}
		\begin{algorithmic}
			\For {threshold $\in$ threshold list}
				\For {seed $\in$ seed list}
				\State Step 1: split train data into training part and validation part according to the seed.
				\State Step 2: train model on the training part and calculate the cost on the validation part.			
				\EndFor 
				\State Step 3: calculate the average cost for this threshold.
			\EndFor
			\State Final Step: Choose the threshold that corresponds to the smallest average cost.
		\end{algorithmic}
	\end{algorithm}

	```


- Literature reference.
	```
	% use \ref to refer to figures, tables, appendices, and etc.
	% use \cite to refer to literatures.

	% add the next two lines at the end of the document
	\bibliographystyle{plain}
	\bibliography{stat8051.bib}
	```

- Add hyperlink as footnotes.
	```
	\usepackage{hyperref}

	% add the following line at the place you want to refer to a hyperlink
	\footnote{\label{interest rate}Interest rate is obtained from \hyperref[interest rate]{''https://finance.yahoo.com/quote/\%5EGSPC/''} }
	```


- Settings of the paper size.
	```
	\usepackage[a4paper,bindingoffset=0.2in,%
	left=1in,right=1in,top=1in,bottom=1in,%
	footskip=.25in]{geometry}
	```


- Titles, authors and abstract.
	```
	\title{Travelers Claim Fraud Detection Project Report}
	\author{Yu Yang}

	\begin{document}

	\maketitle  % don't forget this line!

	\begin{abstract}

	\end{abstract}

	\end{document}
	```
