# tred-macros

Keyboard shortcuts and other macros to speed up UD annotation in TrEd.

TrEd is a customizable cross-platform treebank annotation program written in Perl and Tk.
The homepage is [https://ufal.mff.cuni.cz/tred/](https://ufal.mff.cuni.cz/tred/) but at
the time of writing this, it is pretty outdated. You may want to use TrEd directly from
its [GitHub repository](https://github.com/ufal/TrEd/tree/backend) (the `backend` branch),
which is newer.

TrEd has many extensions for different annotation scenarios, including one for
[Universal Dependencies](https://universaldependencies.org/) and its CoNLL-U file format.
Extensions come with macros that help you achieve certain operations easier and faster.
You can also define your own macros. I keep mine in this repository.



## Loading the macros to TrEd

The information in this section is based on my observations and it may not be the best or
intended way of achieving what I want to achieve. It is quite possible that the correct
way is documented somewhere and I have overlooked it. I know of two ways how to have the
macros loaded in TrEd. One is via the global configuration, the other via an extension.

TrEd's main configuration file is named `.tredrc` and its location depends on the operating
system. On my Windows 11, it is

```
%USERPROFILE%\AppData\Roaming
```

It is possible to add the following to the configuration file:

```
;; ------------------------------------------------------------
;; Macros
;; ------------------------------------------------------------

MacroFile = contrib/dan/tred-ud-treex.mac
```

The `MacroFile` option is supposed to hold path relative to the `tredlib` subfolder in the
TrEd installation folder, i.e., `C:\tred\tredlib` on my computer. The option thus cannot take
absolute path starting with `C:\Users\. We can create a new subfolder of `C:\tred\tredlib\contrib`
and copy the file there.

The second option is to add the macros to those of an installed TrEd extension, such as
EasyTreex or UD. (Historical note: The macros were originally created for Treex in times when
there was no UD extension. But now that we have the UD extension, we preferably want to use it
and annotate directly CoNLL-U files.) Installed extensions can be found in the Roaming profile
(just like the `.tredrc` file) in a folder called `.tred.d`. Each extension has a `contrib.mac`
file, for example, the UD extension has it here:

```
%USERPROFILE%\AppData\Roaming\.tred.d\extensions\ud\contrib\ud\contrib.mac
```

We can edit the file and add an include of our own macro file. Again, the path must be relative,
now to the folder in which `contrib.mac` is found. We can either copy our file to that folder
and include it just by name, or not copy it and include it by a long relative path (the first
include is already part of the extension):

```
#include "ud.inc"
{
package UD;
#include "../../../../../../../Documents/lingvistika-projekty/tred-macros/tred-ud-treex.mac"
}
```

Regardless whether the macros were loaded via tredlib or via an extension, it is important which
package (Perl namespace) they are in. Names of macro packages typically correspond to names of
TrEd annotation modes (can be selected in the upper right corner; reset automatically when
a file of a particular type is open). An extension typically defines its own annotation mode
and package, often with the same name as the extension itself. Macros in tredlib belong to the
`TredMacro` mode and package. To make sure that the macros are in the right package, either
the `package` keyword must be used inside the macro file (e.g., `package TredMacro;`) or the
macro file must be included from a place where the package namespace is still in effect. If the
macro subroutines are not in the right package, they will be offered by the TrEd interface but
an attempt to use them will fail.

All macros of all annotation modes will become available in the menu Macros / All Modes (and
for the current annotation mode, also in Macros / Current Mode). Those that have keyboard
shortcuts defined will be also accessible via these shortcuts provided their mode is the current
mode and the shortcut has not been stolen by another macro defined later in the same mode.

I currently include the macros in package UD from the UD extension, as shown above. Some of
them will need adaptation, as they were originally written for the Treex mode.

The macro language is essentially Perl. Documentation of macro writing is at:
<https://ufal.mff.cuni.cz/pdt2.0/doc/tools/tred/ar01s14.html>


## Keyboard shortcuts

### Dependency relation labels

* `Q` = acl
* `V` = advcl
* `v` = advmod
* `h` = advmod:emph
* `q` = amod
* `N` = appos
* `a` = aux
* `A` = aux:pass
* `z` = case
* `C` = cc
* `k` = ccomp
* `u` = compound
* `j` = conj
* `c` = cop
* `S` = csubj
* `Y` = csubj:pass
* (no shortcut for dep)
* `d` = det
* `G` = det:numgov
* `D` = det:nummod
* `t` = discourse
* `p` = expl:pass
* `e` = expl:pv
* `f` = fixed
* `F` = flat
* `g` = goeswith
* `i` = iobj
* `l` = list
* `Z` = mark
* `n` = nmod
* `s` = nsubj
* `y` = nsubj:pass
* `m` = nummod
* `M` = nummod:gov
* `o` = obj
* `b` = obl
* `B` = obl:agent
* `O` = orphan
* `P` = parataxis
* `;` = punct
* `r` = root
* `T` = vocative
* `x` = xcomp

### Parts of speech

* `CTRL+A` = ADJ
* `CTRL+R` = ADP
* `CTRL+B` = ADV
* `CTRL+U` = AUX
* `CTRL+C` = CCONJ
* `CTRL+D` = DET
* `CTRL+I` = INTJ
* `CTRL+N` = NOUN
* `CTRL+M` = NUM
* `CTRL+T` = PART
* `CTRL+P` = PRON
* `CTRL+Z` = PROPN
* `CTRL+S` = SCONJ
* `CTRL+Y` = SYM
* `CTRL+V` = VERB
* `CTRL+X` = X

### Verb forms

* `CTRL+j` = infinitive

### Genders

* `CTRL+m` = masculine
* `CTRL+f` = feminine
* `CTRL+o` = neuter

### Numbers

* `CTRL+s` = singular
* `CTRL+p` = plural

### Cases

* `CTRL+n` = nominative
* `CTRL+g` = genitive
* `CTRL+d` = dative
* `CTRL+a` = accusative
* `CTRL+v` = vocative
* `CTRL+l` = locative
* `CTRL+i` = instrumental
