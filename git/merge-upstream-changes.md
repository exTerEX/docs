# Merge upstream changes

Developing on a fork sometimes require the upstream source code to be synced with your repository.

## Step 1: Add upstream repository

```sh
git remote add upstream <url>
```

## Step 2: Update upstream repository

```sh
git fetch upstream
```

## Step 3: Checkout correct branch

```sh
git checkout <branch>
```

## Step 4: Merge upstream

```sh
git merge upstream/<remote branch>
```
