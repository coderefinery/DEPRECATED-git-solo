Clone the repository of an example project from 
[here](https://github.com/coderefinery/word-count) 
(we will also use this project in later lessons):
```shell
$ git clone https://github.com/coderefinery/word-count
$ cd word-count
```
At any moment we can inspect individual commits with `git show`. 
Let's first find the earliest commits to this repository:
```shell
$ git log --reverse
commit c4a32caae2f0ddc4d85481f5adf61360198edc2f
Author: Kjartan Thor Wikfeldt <ktwikfeldt@gmail.com>
Date:   Tue May 8 15:15:48 2018 +0200
    initial commit
commit a0cc9e1d0ef853464cd0019479f6ac4eb4ba88c7
Author: Kjartan Thor Wikfeldt <ktwikfeldt@gmail.com>
Date:   Tue May 8 15:24:57 2018 +0200

    add license and credit to SWC
```

and then use `git show` to display the changeset for the second commit:

```
$ git show a0cc9e1d0

commit a0cc9e1d0ef853464cd0019479f6ac4eb4ba88c7
Author: Kjartan Thor Wikfeldt <ktwikfeldt@gmail.com>
Date:   Tue May 8 15:24:57 2018 +0200

    add license and credit to SWC

diff --git a/README.md b/README.md
index 8fe4059..d11eb04 100644
--- a/README.md
+++ b/README.md
@@ -1,8 +1,9 @@
-[![License](https://img.shields.io/badge/license-%20MPL--v2.0-blue.svg)](../master/LICENSE)
-
-
 # Word count example

+This example project is inspired by and derived from
+work by [Software Carpentry](http://software-carpentry.org) licensed under the
+[Creative Commons Attribution license (CC BY4.0)](https://creativecommons.org/licenses/by/4.0/).
 These programs will count words in a given text, plot a bar chart of the 10 mos
t common words,
 and test [Zipf's law](https://en.wikipedia.org/wiki/Zipf%27s_law) on the two mo
st common words.
Compare this with: [https://github.com/coderefinery/word-count/commit/a0cc9e1d0](https://github.com/coderefinery/word-count/commit/a0cc9e1d0)
What if the combination of `git log` and `git show` is not enough to find what we need?
```shell
$ git grep -i zipf

Makefile:# Test Zipf's law
Makefile:results/results.txt: processed_data/abyss.dat source/zipf_test.py
Makefile:       python source/zipf_test.py processed_data/abyss.dat > results/results.txt
Makefile_all:$(RESDIR)/results.txt: $(DATA) source/zipf_test.py
Makefile_all:   python source/zipf_test.py $(DATA) > $@
README.md:most common words, and test [Zipf's
README.md:law](https://en.wikipedia.org/wiki/Zipf%27s_law) on the two most common words.
Snakefile_all:        'zipf_analysis.tar.gz'
Snakefile_all:        rm -f zipf_analysis.tar.gz processed_data/* results/*
Snakefile_all:rule zipf_test:
Snakefile_all:        zipf='source/zipf_test.py',
Snakefile_all:    shell:  'python {input.zipf} {input.books} > {output}'
Snakefile_all:    output: 'zipf_analysis.tar.gz'
doc/exercises.rst:- Write a sentence or two about Zipf's law and link to Wikipedia
doc/purpose.rst:Zipf's law
```shell
$ git blame README.md

73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200  1)
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200  2)
^c4a32ca (Kjartan Thor Wikfeldt 2018-05-08 15:15:48 +0200  3) # Word count example
^c4a32ca (Kjartan Thor Wikfeldt 2018-05-08 15:15:48 +0200  4)
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200  5) These programs will count words in a given text, plot a bar chart of the 10
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200  6) most common words, and test [Zipf's
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200  7) law](https://en.wikipedia.org/wiki/Zipf%27s_law) on the two most common words.
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200  8)
9187d4be (Radovan Bast          2018-08-22 15:16:56 +0200  9) - Inspired by and derived from https://hpc-carpentry.github.io/hpc-python/
9187d4be (Radovan Bast          2018-08-22 15:16:56 +0200 10)   which is distributed under
9187d4be (Radovan Bast          2018-08-22 15:16:56 +0200 11)   [Creative Commons Attribution license (CC-BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200 12) - Documentation: https://word-count.readthedocs.io
a0cc9e1d (Kjartan Thor Wikfeldt 2018-05-08 15:24:57 +0200 13)
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200 14) We use this example in two [CodeRefinery](https://coderefinery.org/) lessons:
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200 15) - https://coderefinery.github.io/reproducible-research/
73434d63 (Radovan Bast          2018-08-22 15:20:30 +0200 16) - https://coderefinery.github.io/documentation/
- [https://github.com/coderefinery/word-count/blame/master/README.md](https://github.com/coderefinery/word-count/blame/master/README.md)
$ git log --oneline --grep "remove"
707c200 remove trailing whitespace for more silent diffs
cc843ff Merge pull request #5 from coderefinery/radovan/encoding
bbf088e (origin/radovan/encoding, radovan/encoding) remove encoding="utf-8" arg to allow also python 2.7
> *I remember there used to be a function called "typeset_labels".
```shell
$ git grep 'typeset_labels' source/plotcount.py
(You can also grep all files at once: `git grep 'typeset_labels`)
```shell
$ git log --oneline source/plotcount.py

7ef076e rm a lot of unused code; fixes #12
aa8cd8a clean up sources with pycodestyle
086715d rm outcommented code
707c200 remove trailing whitespace for more silent diffs
a362e23 python scripts do not need to be executable
6297979 add python command and rm shebangs
8738e1e call python scripts using py3 shebang
c4a32ca initial commit
$ git log -S 'typeset_labels' source/plotcount.py
commit 7ef076eb516851f5f5e2be50d1fd1a1681294e6d
Author: Radovan Bast <bast@users.noreply.github.com>
Date:   Tue Aug 21 00:37:43 2018 +0200
    rm a lot of unused code; fixes #12
commit c4a32caae2f0ddc4d85481f5adf61360198edc2f
Author: Kjartan Thor Wikfeldt <ktwikfeldt@gmail.com>
Date:   Tue May 8 15:15:48 2018 +0200

    initial commit
```shell
$ git show 7ef076eb source/plotcount.py
commit 7ef076eb516851f5f5e2be50d1fd1a1681294e6d
Author: Radovan Bast <bast@users.noreply.github.com>
Date:   Tue Aug 21 00:37:43 2018 +0200
    rm a lot of unused code; fixes #12
diff --git a/source/plotcount.py b/source/plotcount.py
index db7180f..268de5b 100644
--- a/source/plotcount.py
+++ b/source/plotcount.py
@@ -1,7 +1,6 @@
 import numpy as np
 import matplotlib.pyplot as plt
 import sys
-from collections import Sequence

 from wordcount import load_word_counts

@@ -23,67 +22,6 @@ def plot_word_counts(counts, limit=10):
     plt.bar(position, count_data, width, color='b')


-def typeset_labels(labels=None, gap=5):
-    """
-    Given a list of labels, create a new list of labels such that each label
-    is right-padded by spaces so that every label has the same width, then
-    is further right padded by ' ' * gap.
-    """
> ## Git bisect exercise
> 
> Clone [this repository](https://github.com/coderefinery/git-bisect-exercise).
> 
> 
> #### Motivation
> 
> The motivation for this exercise is to be able to do archaeology with Git on a
> source code where the bug is difficult to see visually. **Finding the offending
> commit is often more than half the debugging**.
> 
> 
> #### Background
> 
> The script `get_pi.py` approximates pi using terms of the Nilakantha series. It
> should produce 3.14 but it does not. The script broke at some point and
> produces 3.57 using the last commit:
> 
> ```
> $ python get_pi.py
> 
> 3.57
> ```
> 
> At some point within the 500 first commits, an error was introduced. The only
> thing we know is that the first commit worked correctly.
> 
> 
> #### Your task
> 
> Use `git bisect` to find the commit which broke the computation.
> 
> 
> - But how to find the first commit? Either by `git log --reverse` or `git log --oneline | tail -n 1`
{: .task}

> ## Bonus exercise
> 
> Write a script that checks for a correct result and use `git bisect run` to
> find the offending commit automatically.
{: .task}