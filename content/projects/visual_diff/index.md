+++
title = 'Visual Text Diff - An Experiment With Preact'
date = 2025-01-10
draft = false
+++
[[Link to the tool](/visual-diff)]
[[GitHub](https://github.com/mapang02/visual-diff)]

I created this tool after I found myself encountering situations where I needed to find small differences between two text snippets. There are a number of useful tools which can do this, but having the ability to quickly copy/paste text into a web interface can make comparing a large number of snippets faster. There also aren't as many tools to perform text comparison on mobile devices (and the ones I've found have ads and/or paywalled features).

The tool highlights which lines have changed, and further highlights the words or characters that were added/removed. The interface is inspired by GitHub's commit display and VS Code's file history.
{{<figure src="/images/visual_diff_ex.png">}}

Since this is meant to be a fairly simple tool, I wanted to experiment with using Preact, a framework similar to React but smaller. I found that for my project, the Preact code was almost the same as the equivalent React code. I quickly converted the Preact code to React code (which only required a few small changes) to compare the build sizes using the two libraries, and found that using Preact reduced the build size by about 80 percent! I think this shows that it is definitely worth considering Preact when you need to create a small and efficient website.

{{<figure src="/images/build_size_cmp.png" caption="The build size using Preact is 29.27 kB, whereas the build size using React is 158.76 kB">}}
