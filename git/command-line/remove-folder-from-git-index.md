# Remove folder from Git Index

```
git rm -r --cached ./bin
```

`git rm -r --cached` **removes files from the Git index (the staging area) but leaves them on your filesystem**.

Think of it as: **“Stop tracking these files, but don’t delete them from disk.”**

Breaking it down:

* `rm` → remove
* `-r` → recursively (folders too)
* `--cached` → remove _only_ from the index, not from your working directory

So after running it, the files still exist locally, but Git treats them as untracked.
