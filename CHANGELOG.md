git-drupal -- change log
------------------------

### 01.03 - 2016-10-11

#### Improvements

- Do not allow to use `--message` and `--no-commit` simultaneously (which simply
does not make sense)
- Check wheter `<extension>` and/or `<version>` parameters have been provided
to return a better error message
- Ignore some options and/or parameters if their use makes no sense (e.g. use
of `<version>` with `remove`)
- Options and switches in help output have been reordered to make it more
readable
- Provide more details in default commit messages

### 01.02 - 2016-10-11

#### Improvements

- Remove `.drupal` file: custom GIT config file (`/.drupal`) is removed if there
are no more extensions in it

#### New

- `--no-commit` option: changed files are checked in to index but not commited
- "quiet mode" (`--quiet` option): Most of the output is supressed (e.g. of git
or wget), errors are always printed

### 01.01 - 2016-10-11

#### New

- `.gitattributes` file: ignore all but `git-drupal` script during export
- README

### 01.00 - 2016-10-10

Initial release

Available commands: `add`, `move`, `remove`, `update`
