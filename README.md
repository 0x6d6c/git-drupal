# git-drupal

Manage official contributed Drupal modules & themes in repository.

## Requirements

This script has been **tested only on Linux** (and git 2.1.4) so it can be not
compatible with other operating systems (definitely I am not going to port it
for Windows&reg;). Additionally, it needs the following tools to be present on
your system:

- `curl` (tested with 7.42.1)
- `tar` (tested with 1.28)
- `wget` (tested with 1.16)

## Installation

The simplest and easiest way to install `git drupal` is to download or clone
this repository and place `git-drupal` file or `git-drupal@` symlink on your
`$PATH`. After restarting your shell (e.g. by using `exec bash` if you don't
want to reopen it) `git drupal` command will be available as GIT subcommand. Of
course `git-drupal` file (or symlink) must be executable.

## Usage

```
usage: git drupal add    <extension> <version> --prefix <prefix> [-m <message>] [--quiet] [--no-index] [--no-commit]
   or: git drupal move   <extension> --prefix <prefix> [-m <message>] [--quiet] [--no-index] [--no-commit]
   or: git drupal remove <extension> [-m <message>] [--quiet] [--no-index] [--no-commit]
   or: git drupal update <extension> <version> [-m <message>] [--quiet] [--no-index] [--no-commit]

    -h, --help            show help
    -P, --prefix ...      name of subdirectory where extensions are stored

options for 'add', 'move', 'remove', 'update'
    -m, --message ...     use the given message as the commit message
    -q, --quiet           supress most of the output, always show errors
    --no-index            do not check in chages to index nor commit them
    --no-commit           check in changes to index but do not commit them
```

This script uses a config file called `.drupal` stored it GIT top-level
directory. By default, all changes to this file are also commited to make it
possible to "share" this file with other contributors.

### Usage in detail

#### git drupal add
```
<extension> <version> --prefix <prefix> [-m <message>] [--quiet] [--no-index] [--no-commit]
```

Adds a new contributed extension (module/theme) to the repository.
The `--prefix`/`-P` switch means the project subdirectory where extensions are
stored, e.g. `sites/all/modules` or `sites/all/themes`. Extension name and its
version are validated:

- extension name must follow [Drupal naming conventions](https://www.drupal.org/node/1074362);
simply use lowercase letters, digits and underscores
- version number must start with a digit between 3 and 9 ([Drupal GIT repository
has no releases under 3.x](http://cgit.drupalcode.org/drupal/refs))

**Examples**

```
$ git drupal add --prefix sites/all/modules views 7.x-3.13
$ git drupal add zen 7.x-6.4 -qP sites/all/themes/contrib
```

---

#### git drupal move
```
git drupal move <extension> --prefix <prefix> [-m <message>] [--quiet] [--no-index] [--no-commit]
```

Moves an existing extension (module/theme) to another location (`<prefix>`)
within GIT working tree. In this case you need no provide only the *new*
`prefix` where the extension should be moved into.

`<version>` parameter is ignored even if provided.

**Examples**

```
$ git drupal move --prefix sites/all/themes/contributed views
```

---

#### git drupal remove

```
git drupal remove <extension> [-m <message>] [--quiet] [--no-index] [--no-commit]
```

Removes an existing extension (module/theme) from GIT working tree and index.

`<version>` parameter and `--prefix` option are ignored even if provided.

**Examples**

```
$ git drupal remove views
```

---

#### git drupal update

```
git drupal update <extension> <version> [-m <message>] [--quiet] [--no-index] [--no-commit]
```

Updates an existing extension (module/theme) to another version (it can not be
said "to newer" because it does not validates whether you upgrade or downgrade
an extension). In this case you need to provide only the *new* release number.

`--prefix` option is ignored even if provided.

**Examples**

```
$ git drupal update views 7.x-3.10
```

## End notes

1. `git drupal` tries to determine extension type (module/theme) based on
`--prefix` switch, e.g. if the `--prefix` contains `themes` word than the
extension is considered as "theme".
1. You may not add again the same extension (module/theme), even if it is not
present in `.drupal` config file (TODO?).
1. You may not update (upgrade/downgrade) an extension again to the same
version.
1. Changes can be not checked in to index nor commited by usinf `--no-index`
option (can not be used simultaneously with `--no-commit` nor `--message`).
1. Changes can be checked in to index but not yet commited by using `--no-commit`
option (cn not be used simultaneously with `--no-index` nor `--message`).
1. There is defined a default content of commit messages but you may give your
own ones by using `--message` option.
1. Change log attached.
1. *coming soon*
