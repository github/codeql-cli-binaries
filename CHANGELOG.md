[@IsabelSchoepd](https://avatars.githubusercontent.com/u/20960374?v=4)

<!-- *********************************
     **                             **
     ** GITHUB IS COPYRIGHT FILE!    **
     **                             **
     *********************************
.
     Pull requests should instead drop Markdown snippets in the
     subdirectory `unreleased-changelog-entries` found next to
     the authoritative copy of this file in semmle-code.
     Please include a three-hash heading such as "Bugs fixed"
     and format your snippet as a list item.
.
     (Okay, if you're the CLI release manager following the
     checklist for a CLI release, you can edit here. But then
     you know what to do).
-->
## Release 2.15.3 (2023-11-22)

### New features

- A new compilation flag (`--fail-on-ambiguous-relation-name`) has been added to specify
  that compilation should fail if the compiler generates an ambiguous relation name.
- The new (advanced) command-line option `--[no-]linkage-aware-import` disables the
  linkage-awareness phase of `codeql dataset import`, as a quick fix (at the expense of
  database completeness) for C++ projects where this part of database creation consumes
  too much memory. This option is available in the commands `database create`,
  `database finalize`, `database import`, `dataset import`, `test extract`, and
  `test run`.
- The CodeQL language server now provides basic support for Rename, and you can
  now use the Rename Symbol functionality in Visual Studio Code for CodeQL. The
  current Rename support is less a refactoring tool and more a labor-saving
  device. You may have to perform some manual edits after using Rename, but it
  should still be faster and less work than renaming a symbol manually.
- `codeql database analyze` now defaults to include markdown query help for all custom
  queries with help files available. To change the default behaviour you can pass the
  new flag `--sarif-include-query-help`, which provides the options `always` (which
  includes query help for all queries), `custom_queries_only` (the default) and `never`
  (which does not include query help for any query). The existing flag
  `--sarif-add-query-help` has been deprecated and will be removed in a future release.

### Improvements

- The Find References feature in the CodeQL language server now supports all
  CodeQL identifiers and offers improved performance compared to CodeQL CLI
  2.14 releases.
- The compiler generates shorter human-readable DIL and RA relation names. Due
  to use of an extended character set, full VS Code support for short relation
  names requires VS Code extension 1.9.4 or newer. 
- `codeql database create` and `codeql database finalize` now log more diagnostic
  information during database finalization, including the size of each relation, their
  total size, and the rate at which they were written to disk.

### Bugs fixed

- Fixed an internal error in the compiler when arguments to the `codePointCount` string
  primitive were not bound.
- Fixed a bug where `codeql database finalize` would fail if a
  database under construction was moved between machines between
  `codeql database init` and `codeql database finalize`.  This should
  now work, as long as both commands are run by the same _release_ of
  the CodeQL CLI and the extractors used are the ones bundled with the
  CLI.
- Fixed a bug where `codeql database run-queries` would fail in some
  circumstances when the database path included an `@`.

p- The `codeql query compile` command now accepts a `--keep-going` or
  `-k` option, which indicates that the compiler should continue
  compiling queries even if one of the queries has a compile error in
  it.

- CLI commands now run default queries if none are specified. If no
  queries are specified, the `codeql database analyze`, `codeql
  database run-queries`, and `codeql database interpret-results`
  commands will now run the default suite for the language being
  analyzed.

- `codeql pack publish` now copies the published package to the local
  package cache. In addition to publishing to a remote repository, the
  `codeql pack publish` command will also copy the published package
  to the local package cache.

## Release 2.6.2 (2021-09-21)

- CodeQL CLI 2.6.2 includes the same functionality as **the CodeQL
  runner**, which is being deprecated. For more information, see
  [CodeQL runner deprecation][5].

  [5]: https://github.blog/changelog/2021-09-21-codeql-runner-deprecation/

- The bundled extractors are updated to match the versions currently
  used on LGTM.com. These are newer than the last release (1.28) of
  LGTM Enterprise. If you plan to upload databases to an LGTM
  Enterprise 1.28 instance, you need to create them with release
  2.5.9.

### Bugs fixed

- A bug where `codeql generate log-summary` would sometimes crash with
  a `JsonMappingException` has been fixed.

### New features

- The CodeQL CLI now counts the lines of code found under
  `--source-root` when `codeql database init` or `codeql database
  create` is called. This information can be viewed later by either
  the new `codeql database print-baseline` command or the new
  `--print-baseline-loc` argument to `codeql database
  interpret-results`.

- `qlpack.yml` files now support an additional field `include` in
  which glob patterns of additional files that should be included (or
  excluded) when creating a given CodeQL pack can be specified.

- QL packs created by the experimental `codeql pack create` command
  will now include some information about the build in a new
  `buildMetadata` field of their `qlpack.yml` file.

- `codeql database create` now supports the same flags as `codeql
  database init` for automatically recognizing the languages present
  in checkouts of GitHub repositories:

  - `--github-url` accepts the URL of a custom GitHub instance
    (previously only `github.com` was supported).

  - `--github-auth-stdin` allows a personal access token to be
    provided through standard input (previously only the
    `GITHUB_TOKEN` environment variable was supported).

### Notable documentation changes

- Documentation has been added detailing how to use the "indirect
  build tracing" feature, which is enabled by using the
  `--begin-tracing` flag provided by `codeql database init`. The new
  documentation can be found [here][4]. This feature was temporarily
  described as "sandwiched tracing" in the 2.6.0 release notes.

  [4]: https://aka.ms/codeql-docs/indirect-tracing

## Release 2.6.1 (2021-09-07)

- The bundled extractors are updated to match the versions currently
  used on LGTM.com. These are newer than the last release (1.28) of
  LGTM Enterprise. If you plan to upload databases to an LGTM
  Enterprise 1.28 instance, you need to create them with release
  2.5.9.

## Release 2.0.1 (2019-12-17)

-   Corresponds to LGTM Enterprise release 1.23.
-   The bundled extractors (which are responsible for converting source
    code to databases for each supported language) are updated to match
    the extractor versions used in LGTM Enterprise.
-   No other changes to the core CLI.

## Release 2.0.0 (2019-11-14)

-   First public release.
