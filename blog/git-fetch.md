## Description

Fetch **branches** and/or **tags** (collectively, "refs") from one or more other repositories, along with the objects necessary to complete their histories. **Remote-tracking branches** are updated (see the description of `<refspec>` below for ways to control this behavior).

> **tags:** By default, any tag that points into the histories being fetched is also fetched; the effect is to fetch tags that point at branches that you are interested in. This default behavior can be changed by using the `--tags` or `--no-tags` options or by configuring `remote.<name>.tagOpt`. By using a refspec that fetches tags explicitly, you can fetch tags that do not point into branches you are interested in as well.

`git fetch` can fetch from either a single named repository or URL, or from several repositories at once if `<group>` is given and there is a `remotes.<group>` entry in the configuration file.

The names of refs that are fetched, together with the object names they point at, are written to `.git/FETCH_HEAD`.

```
$ cat .git/FETCH_HEAD
ca07d5f8b9888a29ff05b8c8b16f287cba40e747    branch 'master' of https://github.com/wangzhenj321/GitHub-Manual
24d57dc9a45456c0784e18958a8a97ef9aaacc05    not-for-merge   branch 'dummy' of https://github.com/wangzhenj321/GitHub-Manual
```

## Synopsis

- `git fetch [<options>] [<repository> [<refspec>...]]`

## Options

- `-n, --no-tags`

    By default, tags that point at objects that are downloaded from the remote repository are fetched and stored locally. This option disables this automatic tag following. The default behavior for a remote may be specified with the `remote.<name>.tagOpt` setting.

- `<repository>`

    The "remote" repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section [GIT URLS](#git-urls) below) or the name of a remote (see the section [REMOTES](#remotes) below).

- `<refspec>`

    Specifies **which refs to fetch** and **which local refs to update**. When no `<refspec>`s appear on the command line, the refs to fetch are read from `remote.<repository>.fetch` variables instead.
    
    The format of a `<refspec>` parameter is an optional plus `+`, followed by the source ref `<src>`, followed by a colon `:`, followed by the destination ref `<dst>`. The colon can be omitted when `<dst>` is empty.
    
    ```
    $ cat .git/config
    [remote "origin"]
        url = https://github.com/wangzhenj321/GitHub-Manual.git
        fetch = +refs/heads/*:refs/remotes/origin/*
    ```
    
    The remote ref that matches `<src>` is fetched, and if `<dst>` is not empty string, the local ref that matches it is fast-forwarded using `<src>`. If the optional plus + is used, the local ref is updated even if it does not result in a fast-forward update.

## GIT URLS

In general, URLs contain information about **the transport protocol**, **the address of the remote server**, and **the path to the repository**. Depending on the transport protocol, some of this information may be absent.

Git supports **ssh**, **git**, **http**, and **https** protocols (in addition, **ftp**, and **ftps** can be used for fetching and **rsync** can be used for fetching and pushing, but these are inefficient and deprecated; do not use them).

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

- `ssh://[user@]host.xz[:port]/path/to/repo.git/`
- `git://host.xz[:port]/path/to/repo.git/`
- `http[s]://host.xz[:port]/path/to/repo.git/`
- `ftp[s]://host.xz[:port]/path/to/repo.git/`
- `rsync://host.xz/path/to/repo.git/`

An alternative scp-like syntax may also be used with the ssh protocol:

- `[user@]host.xz:path/to/repo.git/`

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path `foo:bar` could be specified as an absolute path or `./foo:bar` to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support `~username` expansion:

- `ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/`
- `git://host.xz[:port]/~[user]/path/to/repo.git/`
- `[user@]host.xz:/~[user]/path/to/repo.git/`

For local repositories, also supported by Git natively, the following syntaxes may be used:

- `/path/to/repo.git/`
- `file:///path/to/repo.git/`

These two syntaxes are mostly equivalent, except when cloning, when the former implies `--local` option.

## REMOTES

The name of one of the following can be used instead of a URL as `<repository>` argument:

- a remote in the Git configuration file: `$GIT_DIR/config`
- a file in the `$GIT_DIR/remotes` directory
- a file in the `$GIT_DIR/branches` directory

> `GIT_DIR` is the location of the `.git` folder. If this isn't specified, Git walks up the directory tree until it gets to `~` or `/`, looking for a `.git` directory at every step.

All of these also allow you to omit the refspec from the command line because they each contain a refspec which git will use by default.
