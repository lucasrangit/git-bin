# git-custom-commands
Custom Git Commands

## Installation

Git supports adding new sub commands found in your `$PATH`. Install all with:

`for f in $(\find * -maxdepth 1 -type f -executable) ; do echo ln -s $f ~/bin/$f ; done`

## git-backtag

A custom git command that implements backdating tags as described in https://git-scm.com/docs/git-tag#_on_backdating_tags.

```
usage: git backtag [-h|-a|-s|-u <key-id>] [-f] [-m <msg>|-F <file>] <tagname> <commit>
    commit    date of commit will be used to backdate tag
```

Tip: List tags by date:

```
git log --tags --simplify-by-decoration --pretty="format:%ci %d"
```

## git-cherry-pick-list

A custom git command that iteratively applies a list of patches allowing any merge issues to be fixed. It effectively makes `git cherry-pick` resumable.

```
git log --oneline --reverse master..bar | tee patchlist.txt
git cherry-pick-list patchlist.txt
```

See https://www.konsulko.com/git-workflow-for-upstreaming-patches-from-a-vendor-kernel-2/ for more details.

