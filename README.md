# TypeScript + Webpack Problem Matchers for VS Code

Provides [problem matchers](https://code.visualstudio.com/docs/editor/tasks#_processing-task-output-with-problem-matchers) for use with TypeScript projects using [Webpack](https://webpack.js.org/) with [ts-loader](https://github.com/TypeStrong/ts-loader), [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin) v5.0 or later with or without [ESLint](https://eslint.org/), and/or [tslint-loader](https://github.com/wbuchwalter/tslint-loader).

## Features

Provides the following problem matchers:

- **\$ts-webpack** &mdash; adds errors and warnings reported by [ts-loader](https://github.com/TypeStrong/ts-loader)
- **\$ts-webpack-watch** &mdash; adds errors and warnings reported by [ts-loader](https://github.com/TypeStrong/ts-loader) while in watch mode
- **\$ts-checker-webpack** &mdash; adds errors and warnings reported by the [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin)
- **\$ts-checker-webpack-watch** &mdash; adds errors and warnings reported by the [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin) while in watch mode
- **\$ts-checker-eslint-webpack** &mdash; adds ESLint errors and warnings reported by the [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin)
- **\$ts-checker-eslint-webpack-watch** &mdash; adds ESLint errors and warnings reported by the [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin) while in watch mode
- **\$tslint-webpack** &mdash; adds lint warnings reported by tslint-loader
- **\$tslint-webpack-watch** &mdash; adds lint warnings reported by tslint-loader while in watch mode

## Usage

The following example shows how to add problem matchers to your project:

```jsonc
// .vscode/tasks.json
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "npm",
			"script": "build",
			"group": "build",
			"problemMatcher": ["$ts-webpack", "$tslint-webpack"]
		},
		{
			"type": "npm",
			"script": "watch",
			"group": "build",
			"isBackground": true,
			"problemMatcher": ["$ts-webpack-watch", "$tslint-webpack-watch"]
		}
	]
}
```

### webpack-cli@3

In order for the _watch_ matchers to work properly, you must add `--info-verbosity verbose` to your `webpack --watch` command e.g. `webpack --watch --info-verbosity verbose` as this instructs webpack to output lifecycle event messages for each re-compile.

### webpack-cli@4

In order for the _watch_ matchers to work properly, you must add `infrastructureLogging: { level: "log" }` to your `webpack.config.js` as this instructs webpack to output lifecycle event messages for each re-compile. E.g.:

```js
// webpack.config.js

module.exports = {
	// ...the webpack configuration
	infrastructureLogging: {
		level: 'log',
	},
};
```

**Note:** versions of webpack-cli lower than 4.3 are not supported, as they do not support the `infrastructureLogging` configuration.

### ts-checker

In addition, when using the **\$ts-checker-webpack**, **\$ts-checker-webpack-watch**, **\$ts-checker-eslint-webpack**, and **\$ts-checker-eslint-webpack-watch** matchers, you must also set `formatter: 'basic'` in your [fork-ts-checker-webpack-plugin options](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin/tree/alpha#options)

### Using as base

You can also use any of the problem matchers as a base problem matcher for your own custom needs:

```json
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "npm",
			"script": "build",
			"group": "build",
			"problemMatcher": ["$ts-webpack", "$tslint-webpack"]
		},
		{
			"type": "npm",
			"script": "watch",
			"group": "build",
			"isBackground": true,
			"problemMatcher": [
				{
					"base": "$ts-webpack",
					"background": {
						"activeOnStart": true,
						"beginsPattern": {
							"regexp": "<your-custom-starting-regex-pattern here>"
						},
						"endsPattern": {
							"regexp": "<your-custom-ending-regex-pattern here>"
						}
					}
				},
				{
					"base": "$tslint-webpack",
					"background": {
						"activeOnStart": true,
						"beginsPattern": {
							"regexp": "<your-custom-starting-regex-pattern here>"
						},
						"endsPattern": {
							"regexp": "<your-custom-ending-regex-pattern here>"
						}
					}
				}
			]
		}
	]
}
```
