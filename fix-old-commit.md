To "fix" an old commit with a small change, without changing the commit message of the old commit, where `OLDCOMMIT` is something like `091b73a`:

```
git add <my fixed files>
git commit --fixup=OLDCOMMIT
git rebase --interactive --autosquash OLDCOMMIT^
```

You can also use `git commit --squash=OLDCOMMIT` to edit the old commit message during rebase.

See documentation for git commit and git rebase. As always, when rewriting git history, you should only fixup or squash commits you have not yet published to anyone else (including random internet users and build servers).

Detailed explanation
* `git commit --fixup=OLDCOMMIT` copies the `OLDCOMMIT` commit message and automatically prefixes `fixup!` so it can be put in the correct order during interactive rebase. (`--squash=OLDCOMMIT` does the same but prefixes squash!.)
* `git rebase --interactive` will bring up a text editor (which can be configured) to confirm (or edit) the rebase instruction sequence. There is info for rebase instruction changes in the file; just save and quit the editor (:wq in vim) to continue with the rebase.
* `--autosquash` will automatically put any `--fixup=OLDCOMMIT` commits in the correct order. Note that `--autosquash` is only valid when the `--interactive` option is used.
* The `^` in `OLDCOMMIT^` means it's a reference to the commit just before `OLDCOMMIT`. (`OLDCOMMIT^` is the first parent of `OLDCOMMIT`.)
