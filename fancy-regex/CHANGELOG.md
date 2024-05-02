# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/).
This project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html),
with the exception that 0.x versions can break between minor versions.

## [0.7.1] - 2021-07-29
### Fixed
- Fix panic on incomplete escape sequences in input regexes
- Disallow quantifers on lookarounds and other zero-width assertion
  expressions, e.g. the `+` in `(?=hello)+`

## [0.7.0] - 2021-07-12
### Added
- `Regex` now has replace methods like the regex crate:
  - `replace` - single replacement
  - `replace_all` - replace all non-overlapping matches
  - `replacen` - configurable number of replacements

## [0.6.0] - 2021-05-17
### Added
- `Regex` now implements `Clone`, `Display`, `FromStr`
- `Captures` now implements `Index<usize>` to access captures by number
  and `Index<&str>` to access by name

## [0.5.0] - 2021-02-15
### Added
- Methods `find_iter` and `captures_iter` to iterate over all
  non-overlapping matches for a string
- Method `find_from_pos` to `find` starting from a specific position
### Changed
- MSRV (minimum supported Rust version) is now 1.41.1 (from 1.32.0)

## [0.4.1] - 2020-11-09
### Added
- `escape` function to escape special characters in a string so that it
  matches literally

## [0.4.0] - 2020-09-27
### Added
- Support for named groups and backrefs:
  - Capture with `(?<name>...)` or `(?P<name>...)`
  - Backref with `\k<name>` or `(?P=name)`
  - `Captures::name` to get matched group by name
  - `Regex::capture_names` to get capture names in regex
- Support for expanding matches using a replacement template string
  - `Captures::expand` for regex crate compatible syntax
  - See `Expander` for python-compatible syntax and advanced usage
- `Match::range` and some `From` impls for convenience

## [0.3.5] - 2020-04-28
### Changed
- Include string snippet in errors for unknown group and invalid escape
  to make it easier to identify the problem.

## [0.3.4] - 2020-04-28
### Added
- Support comments using `(?# comment)` syntax
- Support unicode escapes like `\u21D2` and `\U0001F60A`

## [0.3.3] - 2020-02-28
### Changed
- Optimization: Delegate const-sized suffixes in more cases
- Optimization: Use `captures_read_at` when delegating to regex crate

## [0.3.2] - 2020-02-05
### Fixed
- Some regexes with fancy parts in the beginning/middle didn't match
  when they should have, e.g. `((?!x)(a|ab))c` didn't match `abc`.

## [0.3.1] - 2019-12-09
### Added
- Add `delegate_size_limit` and `delegate_dfa_size_limit` to
  `RegexBuilder` to allow configuring these limits for regex crate.

## [0.3.0] - 2019-11-27
### Added
- Add limit for backtracking so that execution errors instead of running
  for a long time in case of catastrophic backtracking.
- Add `RegexBuilder` with `backtrack_limit` to configure the new
  backtrack limit per regex.
- `Error` now implements `std::error::Error` trait
### Fixed
- Fix panic in backref matching with multibyte chars

## [0.2.0] - 2019-10-19
### Added
- More documentation and examples
- Support character class nesting and intersections (implemented in
  regex crate)
- Support atomic groups, both the the `(?>foo)` group syntax and the
  `a++`, `a*+` and `a?+` possessive syntax
- Support `\b`, `\f`, `\t`, `\n`, `\r`, `\v`
- Support look-behind with variable sized alternative
- Implement `Debug` for `Regex`
- More test coverage including running one of Oniguruma's test suites
### Changed
- Change `find` to return a `Match` struct (breaking change)
- Change `Captures` API (breaking change):
  - Replace `at` and `pos` with `get` that returns a `Match` struct
  - Remove `is_empty` (use `len`)
- Allow unescaped `]` and `}` as literals
- Allow unescaped `{` as literal when not after atom
- Allow escapes such as `\<` or `\e` inside character classes
- Allow up to 8 characters in `\x{...}` escape
- Allow escaping of space to make literal space
- Allow `(a|)`
- Reject invalid backreferences
### Fixed
- Multiple fixes for alternatives in look-arounds
- Fix hex escape to not include letters after "F"
- Fix handling of unescaped `]` in character classes
- Fix case insensitive character classes and other escapes
- Don't ignore spaces in character classes even with "comment mode"

## [0.1.0] - 2017-02-06
### Added
- Initial release

[0.7.1]: https://github.com/fancy-regex/fancy-regex/compare/0.7.0...0.7.1
[0.7.0]: https://github.com/fancy-regex/fancy-regex/compare/0.6.0...0.7.0
[0.6.0]: https://github.com/fancy-regex/fancy-regex/compare/0.5.0...0.6.0
[0.5.0]: https://github.com/fancy-regex/fancy-regex/compare/0.4.1...0.5.0
[0.4.1]: https://github.com/fancy-regex/fancy-regex/compare/0.4.0...0.4.1
[0.4.0]: https://github.com/fancy-regex/fancy-regex/compare/0.3.5...0.4.0
[0.3.5]: https://github.com/fancy-regex/fancy-regex/compare/0.3.4...0.3.5
[0.3.4]: https://github.com/fancy-regex/fancy-regex/compare/0.3.3...0.3.4
[0.3.3]: https://github.com/fancy-regex/fancy-regex/compare/0.3.2...0.3.3
[0.3.2]: https://github.com/fancy-regex/fancy-regex/compare/0.3.1...0.3.2
[0.3.1]: https://github.com/fancy-regex/fancy-regex/compare/0.3.0...0.3.1
[0.3.0]: https://github.com/fancy-regex/fancy-regex/compare/0.2.0...0.3.0
[0.2.0]: https://github.com/fancy-regex/fancy-regex/compare/0.1.0...0.2.0
[0.1.0]: https://github.com/fancy-regex/fancy-regex/commits/0.1.0
