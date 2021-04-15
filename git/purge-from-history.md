# Removing and purging files from git histroy

Occasionally, a git source repository needs to have something removed from the repository or from the history permanently.

## Step 1: Find the files that you want to remove

### Large files

```sh
git rev-list main | while read rev; do git ls-tree -lr $rev | cut -c54- | sed -r 's/^ +//g;'; done | sort -u | perl -e 'while (<>) { chomp; @stuff=split("\t");$sums{$stuff[1]} += $stuff[0];} print "$sums{$_} $_\n" for (keys %sums);' | sort -rn | head -n 20
```

### Deleting a file that contains a password

```sh
git grep -i 'password' $(git rev-list --all)
```

### Deleting entire deleleted directories

```sh
git log --all --pretty=format: --name-only --diff-filter=D | sed -r 's|[^/]+$||g' | sort -u
```

## Step 2: Rewrite history and remove the old files

```sh
git filter-branch --tag-name-filter cat --index-filter 'git rm -r --cached --ignore-unmatch FILE_LIST' --prune-empty -f -- --all
```

## Step 3: Prune all references

```sh
rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --aggressive --prune=now
```

## Step 6: Push the history changes

```sh
git push origin --force --all
git push origin --force --tags
```
