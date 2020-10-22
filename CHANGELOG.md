# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/) and this project adheres to [Semantic Versioning](http://semver.org/).

## [0.3.1]

### Changed

- Changes problem matcher names to be simplier

## [0.3.0]

### Changed

- Changes to support updated warning/error output for v5 of the [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin)

## [0.2.0]

### Added

- Adds support for v5 of the [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin) using the `basic` formatter
- Adds the code to the problem output

### Fixed

- Fixes an issue with ESLint matching

## [0.1.1]

### Added

- Adds support for running under `webpack-dev-server`

## [0.1.0]

### Added

- Adds new **\$ts-checker-webpack** and **\$ts-checker-webpack-watch** problem matchers to support errors and warnings reported by the [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin)
- Adds new **\$ts-checker-eslint-webpack** and **\$ts-checker-eslint-webpack-watch** problem matchers to support errors and warnings reported by [ESLint](https://eslint.org/) via the [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin)
- Adds warning support to **\$ts-webpack** and **\$ts-webpack-watch**

## [0.0.4]

### Added

- Adds support for `--info-verbosity verbose` as [webpack/webpack-cli#570](https://github.com/webpack/webpack-cli/issues/570) as been fixed

## [0.0.3]

### Fixed

- Fixes issue (_maybe?_) with matchers conflicting with language services

## [0.0.2]

### Fixed

- Fixes issue **\$ts-webpack-watch** not handling absolute paths properly &mdash; Watch out for 🐛[Microsoft/vscode#56721](https://github.com/Microsoft/vscode/issues/56721) if you are basing a problem matcher on another
- Fixes issues with multi-root folders and tslint warnings
- Fixes some issues with errors overlapping with language services

## [0.0.1]

### Added

- Initial release
