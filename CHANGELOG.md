# CodeQL CLI changelog

## Release 2.3.0 (2020-09-28)

- The bundled extractors are updated to match the versions currently
  used on LGTM.com. These are newer than the last release (1.25) of
  LGTM Enterprise. If you plan to upload databases to an LGTM
  Enterprise 1.25 instance, you need to create them with release
  2.2.6.

### Potentially breaking changes

- The Java extractor no longer supports builds running on a Java 6
  JRE. The minimum supported version is Java 7.

- The interpretation of binding set annotations in QL has changed
  subtly.  In rare cases, existing QL code that contains explicit
  binding set annotations on overriding class predicates may now be
  rejected with errors of the form "... is not bound to a value". You
  can fix this by adding explicit binding sets to the overridden
  predicate, or to the abstract class itself in the case of the
  characteristic predicate.  For more information about binding sets,
  see [Annotations](https://help.semmle.com/QL/ql-handbook/annotations.html#binding-sets)
  in the QL language reference.

### QL language improvements

- You can now use binding sets on class bodies. This lets you
  explicitly annotate dynamically dispatched characteristic
  predicates.

### New features

- Query authors can use the new subcommand `codeql generate query-help` to 
  validate query help files and render the files as Markdown. For more information, 
  see [Testing query help files](https://help.semmle.com/codeql/codeql-cli/procedures/testing-query-help-files.html).

- The new subcommand `codeql bqrs hash` computes a stable hash of a
  BQRS file.

- `codeql query decompile` now accepts a `--kind` flag. This allows
  advanced users to choose which intermediate representation to show
  for a compiled QL query. `--kind dil` shows the Datalog
  representation while `--kind ra` shows the relational algebra
  representation used by the evaluator.

## Release 2.2.6 (2020-09-11)

This release corresponds to release 1.25.x of LGTM Enterprise, and
should be used when creating databases that will be uploaded to it.
Future CLI releases (numbered 2.3.x) may produce databases that are not
backwards compatible with this version of LGTM Enterprise.

For all purposes other than creating databases for LGTM Enterprise we
recommend that you continue upgrading to newer CLI releases as they
become available.

## Release 2.2.5 (2020-08-21)

  - The bundled extractors are updated to match the versions currently
    used on LGTM.com. These are newer than the last release (1.24) of
    LGTM Enterprise. If you plan to upload databases to an LGTM
    Enterprise 1.24 instance, you need to create them with release
    2.1.4.

  - Updated license terms with a rewritten description of what is and
    is not allowed.  No substantive changes are intended, but the new
    text is hopefully easier to understand.

### New features

  - The CLI can now execute queries that use QL's `external predicate`
    feature.  All subcommands that execute queries have a new
    `--external` option to specify the value set for those predicates.

  - A new `codeql bqrs diff` command can be used to compute the
    difference between two binary query result sets.

  - `codeql test run` has some new options to improve support for
    testing of extractors:
    - `--check-databases` which will run `codeql dataset check` on
      every test database produced during a run.
    - `--consistency-queries` which will run a set of additional
      queries over _all_ the test databases produced during a run.
    - `--show-extractor-output`

## Release 2.2.4 (2020-06-29)

-   The bundled extractors are updated to match the versions currently
    used on LGTM.com. These are newer than the last release (1.24) of
    LGTM Enterprise. If you plan to upload databases to an LGTM
    Enterprise 1.24 instance, you need to create them with release
    2.1.4.

### Bugs fixed

- QL packs found through the `--search-path` option, or in a sibling
  directory to the unpacked CLI would erroneously take precedence over
  the content of the workspace when using the CodeQL extension for 
  Visual Studio Code. This is now fixed such that the workspace
  takes priority.

- Two command-line options that control the amount of disk space that
  the QL evaluator will try to keep free of disk cache are now called
  `--min-disk-free` and `--min-disk-free-pct`.  Previously they were
  called `--max-disk-free` instead, which made no sense. The old names
  are still recognized such as not to break existing scripts, but are
  now undocumented and deprecated.

## Release 2.2.3 (2020-06-15)

CodeQL CLI 2.2.3 is the same as version 2.2.2, but re-released with a new
version number because the `v2.2.2` folder on the download site
originally contained the 2.2.0 binaries instead of the correct 2.2.2
ones.

If you have downloaded release 2.2.2, and `codeql --version` correctly
identifies itself as being that version, you don't need to upgrade to
2.2.3.

## Release 2.2.2 (2020-06-12)

-   The bundled extractors are updated to match the versions currently
    used on LGTM.com. These are newer than the last release (1.24) of
    LGTM Enterprise. If you plan to upload databases to an LGTM
    Enterprise 1.24 instance, you need to create them with release
    2.1.4.

### Improvements

-   Query evaluations that time out due to a `--timeout` option are no
    longer silently discarded. Instead `codeql` will terminate with exit
    code 33. Commands that evaluate multiple queries will produce as
    much output as they can even if one of the queries times out.

## Release 2.2.1

There is no CodeQL CLI version 2.2.1. This version number was used
internally to work around restrictions in the CodeQL for VS Code
extension.

## Release 2.2.0 (2020-05-29)

-   The bundled extractors are updated to match the versions currently
    used on LGTM.com. These are newer than the last release (1.24) of
    LGTM Enterprise. If you plan to upload databases to an LGTM
    Enterprise 1.24 instance, you need to create them with release
    2.1.4.
-   Starting with this release, the CodeQL CLI can be downloaded either
    as a single `codeql.zip` file containing the CLI for all supported
    platforms, or as a `codeql-PLATFORM.zip` that contains the files for
    just one platform. The single-platform zips are faster to download.

### QL language improvement

-   QL now supports the definition of new types as type unions. This
    feature currently allows unions of branches from an already existing
    algebraic data type and unions of database types.

## Release 2.1.4 (2020-05-26)

This release corresponds to release 1.24.x of LGTM Enterprise, and
should be used when creating databases that will be uploaded to it.
Future CLI releases (numbered 2.2.x) may produce databases that are not
backwards compatible with this version of LGTM Enterprise.

For all purposes other than creating databases for LGTM Enterprise we
recommend that you continue upgrading to newer CLI releases as they
become available.

### Features added

-   A new `codeql query format` command exposes the QL autoformatter for
    use on the command line.

### Bugs fixed

-   `-J` command-line options that contain spaces now ought to work on
    Windows. They still do not work reliably on Linux or MacOS, though.

## Release 2.1.3 (2020-05-13)

### Bugs fixed 

-   Fixes a bug in `codeql execute cli-server` (a helper used by the VS
    Code extension) which would sometimes cause query compilation to
    fail until the extension was restarted.
-   Fixes a bug in `codeql database upgrade` which could lead to
    performance losses if the upgraded database was subsequently used
    with LGTM or the legacy Semmle Core product.
-   Fixes a bug in the QL evaluator that would sometimes lead to crashes
    for queries that use the new `unique` aggregate added in release
    2.1.0.
-   The value of the `--compilation-cache-size` option is now correctly
    interpreted as a number of megabytes rather than a number of bytes.

## Release 2.1.2 (2020-05-06)

-   Updated license terms to allow CI use with GitHub Actions for
    open-source software.

### Potentially breaking changes

-   In [query suite definitions](https://help.semmle.com/codeql/codeql-cli/procedures/query-suites.html), filter
    instructions that filter on the `query path` pseudo-tag will now
    always see the relative path to the query expressed with `/` as a
    directory separator, independently of the platform. Previously they
    erroneously used the platform's directory separator, meaning that
    query suites developed on Windows would not work correctly on Unix
    systems (and vice versa) if they used `query path`. Existing suite
    definitions developed on Windows may need to be updated to match the
    new behavior.

### Features added

-   A new `codeql test accept` subcommand helps automate updating the
    expected output for unit tests after a desired change in query
    behavior. This can also be done by the new `--learn` option for
    `codeql test run`.

### Bugs fixed

-   `codeql database create` will now report an explicit error if given
    a `--command` argument that specifies an empty string. Previously
    this would be accepted initially, leading to confusing failures
    later.

## Release 2.1.1 (2020-04-20)

-   The bundled extractors are updated to match the versions currently
    used on LGTM.com.

### Features added

-   `codeql resolve queries` accepts a `--format=bylanguage` option.
    This is used to help automated workflows determine which languages
    to create databases for, from the queries that are available to run.
-   It is now possible to attempt to execute `.ql` files that are not in
    a QL pack. This is used by a few specialized internal workflows.
    However, standalone queries cannot import any of the dependencies
    that you would usually declare in a `qlpack.yml` file, so will not
    be useful in most cases.

## Release 2.1.0 (2020-03-27)

-   The bundled extractors are updated to match the versions currently
    used on LGTM.com. These are newer than the last release (1.23) of
    LGTM Enterprise. If you plan to upload databases to an LGTM
    Enterprise 1.23 instance, you need to create them with release
    2.0.1. For more information, see [Preparing CodeQL databases to
    upload to
    LGTM](https://help.semmle.com/lgtm-enterprise/admin/help/prepare-database-upload.html)
    in the LGTM admin help.

### Potentially breaking changes

-   If you pass a directory name as a command-line argument to
    `codeql test run`, it will now consider all `.ql` or `.qlref` files
    found under that directory to be test queries, even if they have no
    accompanying `.expected` file. Tests that lack an `.expected` file
    will fail, but will generate an `.actual` file that you can rename
    to `.expected` if you want to use the results.

    The goal of this change is to support existing workflows of
    experienced CodeQL users, and also to provide clear error
    indications if an `.expected` file is accidentally lost, renamed, or
    misspelled.

    However, if you invoke `codeql test run` on a directory tree that
    contains both tests and non-test queries, you will now encounter
    errors if any of the `.ql` files can't be processed as test queries.
    If you're affected by this change, you can suppress these errors by:

    -   Adding a `tests` property to this QL pack to define specify
        which directories contain only test queries and associated test
        code. For more information, see
        [About QL packs](https://help.semmle.com/codeql/codeql-cli/reference/qlpack-overview.html).
    -   Running `codeql test run` with a new `--strict-test-discovery`
        option.

    In the longer term, we recommend that you reorganize the queries so
    that test queries are stored in a directory tree that's separate
    from actual queries.

-   `codeql database create` and `codeql database finalize` will no
    longer recognize a `--no-duplicate-code` option. This option has
    never had any effect, and its positive variant `--duplicate-code`
    previously led to a fatal error.

### Features added

-   A new XML extractor is included. It is not intended to be used as a
    stand-alone extractor, but rather to augment the data produced by
    other extractors. In particular, the C\# and Java extractors invoke
    it during database creation to include information relevant to the
    analysis of those languages, much like LGTM.com does.
-   Two new plumbing commands `codeql database index-files` and
    `codeql resolve files` have been added for support of invoking the
    XML extractor support. These commands are generally only of interest
    for extractor authors.
-   Two new plumbing commands have been added to `codeql dataset`. The
    `measure` subcommand can be used to collect size information from a
    dataset, and the `check` subcommand can scan a dataset for database
    inconsistencies. These commands are useful when developing a new
    CodeQL extractor.
-   The QL evaluator contains a number of features in support of an
    internal experiment with using machine-learning techniques to
    identify functions in unknown codebases as sources or sinks of
    taint. This includes new command-line options `--ml-model-path` and
    `--native-library-path` to several subcommands. As the new features
    are not yet ready for general use, these new options should be
    ignored by external CodeQL users.

### Bugs fixed

-   Fixes a bug that could result in empty databases for C/C++.
    Previously, extraction would mistakenly be skipped for source files
    compiled with the Clang compiler, if the `-fintegrated-cc1` option
    was specified.
-   `codeql database create` and `codeql database init` will now, as
    they have always been documented, refuse to create a database whose
    parent directory doesn't already exist.
-   `codeql test run` will no longer leave `.actual` files from previous
    runs in the file system after a test passes.

### QL language improvements

-   QL now supports set literals, and the QL extractor can identify them
    with the `SetLiteral` class. For more information, see [Set literal
    expressions](https://help.semmle.com/QL/ql-handbook/expressions.html#set-literal-expressions)
    in the QL language reference.
-   QL now supports a uniqueness aggregate. This can express constraints
    that there is precisely one value. The syntax is taken from previous
    aggregates such as `min` and `max`.

    ``` {.sourceCode .ql}
    unique(int x | x = 4 or x = 2 * 2 | x)
    ```

## Release 2.0.6 (2020-03-16)

### Bugs fixed

-   Fixes a problem preventing `codeql database create` from working
    with Python 3 on macOS.
-   Fixes a problem preventing `codeql database create` from finding
    locally installed Python packages.

## Release 2.0.5 (2020-03-13)

-   The bundled extractors (which are responsible for converting source
    code to databases for each supported language) are updated to match
    the versions currently used on LGTM.com. These are newer than the
    last release of LGTM Enterprise, so this release should not be used
    if you plan to upload databases to an LGTM Enterprise instance. For
    more information, see [Preparing CodeQL databases to upload to
    LGTM](https://help.semmle.com/lgtm-enterprise/admin/help/prepare-database-upload.html)
    in the LGTM admin help.

### Features added

-   `codeql test run` has a new `--slice` option that can be used to
    parallelize tests over more machines.

## Release 2.0.4 (2020-02-21)

-   The bundled extractors (which are responsible for converting source
    code to databases for each supported language) are updated to match
    the versions currently used on LGTM.com. These are newer than the
    last release of LGTM Enterprise, so this release should not be used
    if you plan to upload databases to an LGTM Enterprise instance. For
    more information, see [Preparing CodeQL databases to upload to
    LGTM](https://help.semmle.com/lgtm-enterprise/admin/help/prepare-database-upload.html)
    in the LGTM admin help.

### Features added

-   Subcommands that execute queries (such as `codeql database analyze`)
    now have a `--timeout` option that can be used to set a timeout to
    automatically cancel query evaluations that appear to diverge.
-   A new plumbing command `codeql query decompile` can display the DIL
    intermediate representations that is included in the output of
    `codeql query compile --dump-qlo --include-dil-in-qlo`. This is
    useful mainly for certain internal workflows; the information
    produced is the same as what `codeql query compile --dump-dil`
    already outputs.

### Bugs fixed

-   The `--debug` and `--tuple-counting` options to
    `codeql test run` erroneously had no effect. Now they ought to work.

## Release 2.0.3 (2020-02-12)

### Bugs fixed

-   Fixes a bug where `codeql test run` would fail with the
    message
    `CatastrophicError: There should be a --library-path option for com.semmle.cli2.LibraryPathOptions.libraryPath but we didn't find it`
    when running tests against the `master` branch of the CodeQL
    libraries for certain languages.
-   Otherwise identical to release 2.0.2.

## Release 2.0.2 (2020-02-05)

-   The bundled extractors (which are responsible for converting source
    code to databases for each supported language) are updated to match
    the versions currently used on LGTM.com. These are newer than the
    last release of LGTM Enterprise, so this release should not be used
    if you plan to upload databases to an LGTM Enterprise instance. For
    more information, see [Preparing CodeQL databases to upload to
    LGTM](https://help.semmle.com/lgtm-enterprise/admin/help/prepare-database-upload.html)
    in the LGTM admin help.
-   The parent and sibling directories of the unpacked CLI are no longer
    searched recursively for QL packs. QL packs will only be found if
    there's a `qlpack.yml` or `.codeqlmanifest.json` directly in a
    parent or sibling directory. This should eliminate the very long
    disk-scanning delays experienced by users who unpacked earlier
    versions of the CLI in their home directory.
-   Parent and sibling directories of the unpacked CLI will now be
    searched for QL packs as a last resort, even if you give an explicit
    `--search-path` option. This means, for example, that you can define
    a search path in the [per-user configuration file](https://help.semmle.com/codeql/codeql-cli/reference/configuration-overview.html) without it depending on
    where the CLI is unpacked. In particular, the setting can now be
    meaningfully used by users who let the CodeQL for VS Code extension
    manage the downloading and unpacking of the CLI.

### Security updates

-   The `codeql database create` command and its relatives will no
    longer attempt to find extractors located in the parent and sibling
    directories of the unpacked CLI. This closes a security risk for
    users who unpacked the CodeQL CLI in their home directory. This
    could've resulted in arbitrary code execution if the user unpacked a
    file archive containing a malicious extractor anywhere in the home
    directory. Extractors will now only be found within the unpacked CLI
    itself, or in directories explicitly listed in the `--search-path`.
    It is expected that users will only point `--search-path` to
    locations they trust at least as much as the CLI download itself.

### Features added

-   This release supports executing query regression tests using the
    `codeql test` command. For further information, see
    [Testing custom queries](https://help.semmle.com/codeql/codeql-cli/procedures/test-queries.html).
-   The error message if you try executing a query against a database
    that needs to be upgraded (which can happen routinely if you're
    using a fresh `master` checkout of the CodeQL libraries with the
    bundled extractors) will now explicitly suggest a
    `codeql database update` command to run. The database is not
    automatically upgraded, as this may make it irreversibly
    incompatible with older versions of the CodeQL libraries. This
    allows users who want to compare behavior of different versions of
    the libraries against the same database to make a copy before they
    upgrade it.

## Release 2.0.1 (2019-12-17)

-   Corresponds to LGTM Enterprise release 1.23.
-   The bundled extractors (which are responsible for converting source
    code to databases for each supported language) are updated to match
    the extractor versions used in LGTM Enterprise.
-   No other changes to the core CLI.

## Release 2.0.0 (2019-11-14)

-   First public release.
