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
way is documented somewhere and I have overlooked it.

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
absolute path starting with `C:\Users\zeman`, for example. It might be possible to make the
path relative and still lead it to a user space (`../../User/`). Or one can simply copy
the macros to a new subfolder of `C:\tred\tredlib\contrib`, as I did. The macros then appear
in TrEd in mode TredMacro (set the mode in the upper right corner; then menu
Macros / Current Mode / More... / Set deprel to cop (for example). If we want the UD mode on
(instead of TredMacro), we can use menu Macros / All Modes / TredMacro / More... / Set deprel
to cop.

Problém: Když soubor s makry umístím, jak je uvedeno výše, tak se makra sice objeví v menu
a TrEd bude znát příslušné klávesové zkratky, ale po pokusu některé makro opravdu spustit
se objeví chyba, že příslušnou funkci nelze v balíčku TredMacro najít.

Podle C:\tred\tredlib\contrib\README se zdá, že kdybych soubor s makry dal do podadresáře dan
a pojmenoval ho contrib.mac, TrEd by ho možná načetl automaticky a nemusel bych ho explicitně
uvádět v .tredrc.

It would be also possible to implant the file to the macros provided by the UD extension to
TrEd. The extensions are in the `.tred.d` folder (also in the Roaming profile):

```
%USERPROFILE%\AppData\Roaming\.tred.d\extensions\ud\contrib\ud\contrib.mac
```

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
