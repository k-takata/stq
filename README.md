# Stq -- A Mercurial-Queues-like wrapper for StGit

## Overview

**Caution**: This software is still in the Alpha stage.

There are already several [Mercurial-Queues](https://wiki.mercurial-scm.org/MqExtension)-like tools for Git. [Guilt](https://github.com/git-guilt/guilt) is one of them. However, Guilt is extremely slow on Windows.
[StGit](https://stacked-git.github.io/) is another option. The speed is fast enough, but the usage is different from Mercurial Queue. It stores all metadata as Git objects, and managing the patch files themselves is not easy.

Stq is a wrapper for StGit that stores patch files in `.git/stq-patches/`, similar to Mercurial Queues. Users can also manage the patch files with Git and easily publish them, e.g., on GitHub.


## Requirements

- OS:
  - Cygwin
- StGit 1.5 (Not tested with 2.x)
- Git
- Python 3.9+


## Sample Usage

Initialize the patch directory:

```shell
$ stq init
```

Create a new patch named `new-feature-1.patch`:

```shell
$ stq new new-feature-1.patch
```

Edit somefile:

```shell
$ vim somefile
```

Refresh new-feature-1.patch:

```shell
$ stq refresh
```

Now, `.git/stq-patches/new-feature-1.patch` has the change just we made.

List all patches:

```shell
$ stq series
```

Pop the top most applied patch:

```shell
$ stq pop
```

Push the next patch:

```shell
$ stq push
```

Pull the latest changes from the remote repository:

```shell
$ stq pull
```

Run the git command (e.g. `git status`) in the `.git/stq-patches/` directory:

```shell
$ stq qgit status
```

(Similar to the `--mq` option in Mercurial Queues.)

Subcommands can be shortened if they are not ambiguous. E.g.:

```shell
$ stq ser  # Same as "stq series"
```

## Settings

If you use a long name for a patch file, consider increasing `stgit.namelength`. E.g.:

```shell
$ git config set --global stgit.namelength 60  # Default is 30. (0 means unlimited.)
```

Stq itself doesn't have any settings for now.

## Appendix

### Installing StGit 1.5

```shell
$ git clone https://github.com/stacked-git/stgit.git
$ git checkout v1.5
$ make all
$ python3 setup.py install --user
```

See `INSTALL` in the stgit directory for details.

## License

MIT License
