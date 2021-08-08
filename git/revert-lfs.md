# Revert LFS tracking

If you want to change file tracking for specific files from LFS to standard git tracking

```sh
git lfs untrack <files>
git rm --cached <files>
git add <files>
```

And then delete .gitattributes if empty and commit changes.
