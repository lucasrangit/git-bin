# git-custom-commands
Custom Git Commands

## Installation

Git supports adding new sub commands found in your `$PATH`. Install all with:

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

## git-removed-branches

A custom git command to list or remove tracked branches that have been removed by the remote.

```
usage: git-removed-branches [-h] [--prune] [--force] [--remote REMOTE]

Remove local branches, which are no longer available in the remote

optional arguments:
  -h, --help       show this help message and exit
  --prune          Remove branches
  --force          Force deletion
  --remote REMOTE  Remote name (default origin)
```

Copied from @nemisj https://github.com/nemisj/git-removed-branches/blob/master/git-removed-branches.py (MIT License)

