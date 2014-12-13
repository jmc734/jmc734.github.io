---
layout: 	post
title:		"Adding [citation needed] to a LaTeX Document"
categories:	snippet
tags:		latex
published:  false
---

{% highlight latex linenos %}
\usepackage{ifthen}
\usepackage{color}

% Rename the default \cite command \ocite
\let\ocite = \cite

% If reference is ?, then either write [citation needed]
% Otherwise, call \ocite with the arguments
\renewcommand{\cite}[2][]{
	\ifthenelse{\equal{#2}{?}}{
		\textcolor{red}{[citation needed]}
	}{
		\ifthenelse{\equal{#1}{}}{\ocite{#2}}{\ocite[#1]{#2}}
	}
}
{% endhighlight %}