# GitHub Checklist

A somewhat opinionated checklist of things to do to prepare your local environment for GitHub.

## Blame Ignore Revs File

Set up the default file that `git blame` uses to know which commits to ignore.

```shell
git config --global blame.ignoreRevsFile .git-blame-ignore-revs
```

***NOTE:*** If you find yourself working on more repositories that *don't* have this file than
repositories that *do,* then you may want to configure this value locally for each repository
instead of globally. Configuring this globally can result in an error when calling `git blame`
in a repository that doesn't have this file.

### Why?

GitHub now uses [a file called `.git-blame-ignore-revs` that lists commits to ignore][blame-ignore-docs].
This setting ensures that your local instance uses the same file by default, matching GitHub's behavior.
Otherwise, you would need to use the `--ignore-revs-file` command-line option of `git blame` to get
the same behavior.

## Initial Default Branch

Set your initial default branch. Some common branch names are `main`, `master`, and `trunk`.
This will be the branch where your very first commit will be.

```shell
git config --global init.defaultBranch BRANCH
```

### Why?

GitHub now allows you to specify the name of the default branch of new repositories in your
profile's settings. Using this `git config` option, you can mirror this preferred default
branch name locally. Note that this requires Git 2.28 or above, and previous versions may
continue to default to `master`.

## Git LFS

Install [Git LFS][git-lfs].

### Why?

This isn't exclusive to GitHub, but GitHub is one of the services that utilizes Large File Storage.
You can read more about Large File Storage in [their docs][git-lfs], but the gist is it allows you
to version large files without bloating the size of your main repository. Git LFS does this by
storing a *reference* to a file in the repository, and downloading it on-demand. Eventually, you
may want to use this feature that GitHub provides, or you may encounter a repository that uses this
feature.

## Git Lazy Commit

A bit of self-promotion here :wink:

GitHub generates commit messages for you when you use the web UI. For example, `Update README.md`.
I wrote [git lazy-commit][git-lzc] to behave roughly the same way when generating commits locally.

### Why?

Sometimes you don't care about writing the commit message when you use the web UI. Similarly, this
allows you to be lazy about writing your commit message locally.

## GitHub CLI

Install the [GitHub CLI][gh-cli], and set it as your credential manager for GitHub with `gh auth setup-git`.

After that, install some extensions with `gh extension install OWNER/REPO`. Some useful ones are:

- [action/gh-actions-cache](https://github.com/actions/gh-actions-cache)
- [ymmmtym/gh-gitignore](https://github.com/ymmmtym/gh-gitignore)
- [mislav/gh-license](https://github.com/mislav/gh-license)

You can find other extensions for `gh` by searching for the [`gh-extension` topic][gh-extension-topic].
Also, I've written a few extensions that I personally find useful :wink:

### Why?

Interacting with GitHub via the command-line allows you to stay in the same context instead of frequently
switching between the terminal and the web browser. Several of the commands and extensions are also
arguably faster in the terminal than switching to a browser.

## GitHub's Web Flow GPG Key

Import the key from [github.com/web-flow.gpg][github-web-flow-key].

### Why?

This allows you to verify commits that were signed by GitHub locally.

[blame-ignore-docs]: https://docs.github.com/en/repositories/working-with-files/using-files/viewing-a-file#ignore-commits-in-the-blame-view
[gh-cli]: https://github.com/cli/cli
[gh-extension-topic]: https://github.com/topics/gh-extension
[git-lzc]: https://github.com/spenserblack/git-lazy-commit
[git-lfs]: https://github.com/git-lfs/git-lfs
[github-web-flow-key]: https://github.com/web-flow.gpg
