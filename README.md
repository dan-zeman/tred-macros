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

The location where TrEd looks for its macro files depends on the operating system.
On my Windows 11, it is

```
%USERPROFILE%\AppData\Roaming
```

After installing and running TrEd, you will probably find at least a `.tredrc` file there.
This is a configuration file, not a macro file. I copy the `tred-ud-treex.mac` file to the
same location. It will not be be imported by TrEd automatically and I did not figure out any
better way than including it from (or copying the macros to) the macro file of the ud extension
that _is_ loaded automatically. The extensions are in the `.tred.d` folder (also in the
Roaming profile):

```
%USERPROFILE%\AppData\Roaming\.tred.d\extensions\ud\contrib\ud\contrib.mac
```
