# git-custom-commands
Custom Git Commands

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

