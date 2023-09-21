# git-custom-commands
Custom Git Commands

## Installation

Git supports adding new sub commands found in your `$PATH`. Either add this directory to your `$PATH` or install symlinks to `~/bin` so you can remove any you don't want.

`for f in $(\find * -maxdepth 1 -type f -executable) ; do ln --verbose -s $(pwd)/$f ~/bin/$f ; done`

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

## git-reset-upstream

A custom git command that resets the local master with the upstream remote master. Useful if you are tracking a canonical master branch.

**Note:** If your local master is non canonical and has changes then you should not use this and instead use `git merge upstream/master`.

## git-clean-branches

A custom git command to list or remove locally tracked branches that have been removed on the remote.

```
usage: git-clean-branches [-h] [--prune] [--force] [--remote REMOTE]

Remove local branches, which are no longer available in the remote

optional arguments:
  -h, --help       show this help message and exit
  --prune          Remove branches
  --force          Force deletion
  --remote REMOTE  Remote name (default origin)
```

Copied from @nemisj https://github.com/nemisj/git-removed-branches/blob/master/git-removed-branches.py (MIT License) but renamed because it's almost an extension to `git-clean`.

## git-top

A custom git command to search the parent directories for the topmost git project directory. This handles submodules of any depth whereas `git rev-parse --show-toplevel --show-superproject-working-tree` only works for one level.

```
$ tree -a
/home/user/project
├── external
│   ├── library
│   │   ├── .git
├── .git
│   ├── branches
...
$ cd external/library
$ git-top
/home/user/project
```
