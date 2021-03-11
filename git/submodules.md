# How To Add and Update Git Submodules

Git submodules are most of the time used in order to incorporate another versioned project within an existing project. Submodules can be used for example in order to store third-party libraries used by your main project in order to compile successfully.

## Add a Git Submodule

In order to add a Git submodule, use the _git submodule add_ command. Specify the URL of the Git remote repository to be included.

```sh
$ git submodule add <remote_url> <destination_folder>
```

When adding a Git submodule, your submodule will be staged. Consequently, you will need to commit your submodule.

```sh
$ git commit -m <MSG>
$ git push
```

## Pull a Git Submodule

Whenever you are cloning a Git repository having submodules, you need to execute an extra command in order for the submodules to be pulled. To pull a Git submodule, use _git submodule update_ with the _–-init_ and the _-–recursive_ options.

```sh
$ git submodule update --init --recursive
```

## Update a Git Submodule

In some cases, you are not pulling a Git submodule but you look to update your existing Git submodule in the project. To update an existing Git submodule, execute _git submodule update_ with the _-–remote_ and the _-–merge_ option.

```sh
$ git submodule update --remote --merge
```

## Fetch new submodule commits

To fetch new commits from a submodule repository, head into your submodule folder and fetch updates.

```sh
$ cd repository/submodule
$ git fetch
```

Then run _git log_, giving you a list of the 3 last commits.

```sh
$ git log --oneline origin/<branch> -3
```

In order for your submodule to be in-line with the newest commits, run _git checkout_ with the latest commit **SHA** (the 7 character long alphanumeric string, e.g. c01018c, c57f3fb, etc.)

```sh
$ git checkout -q <SHA>
```

Now, go back into the main repository and commit the new submodule.

```sh
$ cd ..
$ git add <submodule>
$ git commit -m <MSG>
```

## Remove Git submodules

To remove a Git submodule from your repository, use _git submodule deinit_ followed by the _git rm_ command and specify the name of the submodule folder.

```sh
$ git submodule deinit <submodule>
$ git rm <submodule>
```

## Configuring submodules for your repository

To get additional logging lines whenever you are executing _git status_.

### Submodule summary

To have a submodule summary when executing _git status_, execute _git config_ and add the _status.submoduleSummary_ option set to **true**.

```sh
$ git config --global status.submoduleSummary true
```

### Detailed diff for submodules

For the _git diff_ command to have detailed information about your submodules, use _git config_ with _diff.submodule_ set to **log**.

```sh
$ git config --global diff.submodule log
```
