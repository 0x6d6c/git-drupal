# git-drupal

Manage official contributed Drupal modules & themes in repository.

## Requirements

This script has been **tested only on Linux** (and git 2.1.4) so it can be not
compatible with other operating systems (definitely I am not going to port it
for Windows&reg;). Additionally, it needs the following tools to be present on your
system:

- `curl` (tested with 7.42.1)
- `tar` (tested with 1.28)
- `wget` (tested with 1.16)

## Usage

```
usage: git drupal add    --prefix <prefix> <extension> <version> [-m <message>] [-q] [--no-commit]
   or: git drupal move   --prefix <prefix> <extension> [-m <message>] [-q] [--no-commit]
   or: git drupal remove <extension> [-m <message>] [-q] [--no-commit]
   or: git drupal update <extension> <version> [-m <message>] [-q] [--no-commit]

    -h, --help            show help
    -P, --prefix ...      name of subdirectory where extensions are stored

options for 'add', 'move', 'remove', 'update'
    -m, --message ...     use the given message as the commit message for the merge commit
    -q, --quiet           supress most of the output, always show errors
    --no-commit           add changes to index but do not commit them
```

This script uses a config file called `.drupal` stored it GIT top-level
directory. By default, all changes to this file are also commited to make it
possible to "share" this file with other contributors.

### Usage in detail

#### git drupal add
```
git drupal add --prefix <prefix> <extension> <version>
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
$ git drupal add zen 7.x-6.4 -P sites/all/themes/contrib
```

---

#### git drupal move
```
git drupal move --prefix <prefix> <extension>
```

Moves an existing extension (module/theme) to another location (`<prefix>`)
within GIT working tree. In this case you need no provide only the *new*
`prefix` where the extension should be moved into.

**Examples**

```
$ git drupal move --prefix sites/all/themes/contributed views
```

---

#### git drupal remove

```
git drupal remove <extension>
```

Removes an existing extension (module/theme) from GIT working tree and index.

**Examples**

```
$ git drupal remove views
```

---

#### git drupal update

```
git drupal update <extension> <version>
```

Updates an existing extension (module/theme) to another version (it can not be
said "to newer" because it does not validates whether you upgrade or downgrade
an extension). In this case you need to provide only the *new* release number.

**Examples**

```
$ git drupal update views 7.x-3.10
```

## End notes

1. `git drupal` tries to determine extension type (module/theme) based on
`--prefix` switch, e.g. if the `--prefix` contains `themes` word than the
extension is considered as "theme".
1. You may not add again the same extension (module/theme), even if it is not
present in `.drupal` config file.
1. You may not update (upgrade/downgrade) an extension again to the same
version.
1. There is defined a default content of commit messages but you may give your
own ones by using `-m`/`--message` switch.
1. Changes can be added to index but not yet commited by using `--no-commit`
switch.
1. *coming soon*
