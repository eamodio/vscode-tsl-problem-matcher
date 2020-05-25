# TypeScript + Webpack Problem Matchers for VS Code

Provides [problem matchers](https://code.visualstudio.com/docs/editor/tasks#_processing-task-output-with-problem-matchers) for use with TypeScript projects using [Webpack](https://webpack.js.org/) with [ts-loader](https://github.com/TypeStrong/ts-loader), [fork-ts-checker-webpack-plugin](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin) with or without [ESLint](https://eslint.org/), and/or [tslint-loader](https://github.com/wbuchwalter/tslint-loader).

## Features

Provides the following problem matchers:

- **\$ts-webpack** &mdash; adds errors and warnings reported by ts-loader
- **\$ts-webpack-watch** &mdash; adds errors and warnings reported by ts-loader while in watch mode
- **\$ts-checker-webpack** &mdash; adds errors and warnings reported by the fork-ts-checker-webpack-plugin
- **\$ts-checker-webpack-watch** &mdash; adds errors and warnings reported by the fork-ts-checker-webpack-plugin while in watch mode
- **\$ts-checker-eslint-webpack** &mdash; adds ESLint errors and warnings reported by the fork-ts-checker-webpack-plugin
- **\$ts-checker-eslint-webpack-watch** &mdash; adds ESLint errors and warnings reported by the fork-ts-checker-webpack-plugin while in watch mode
- **\$ts-checker5-webpack** &mdash; adds errors and warnings reported by the fork-ts-checker-webpack-plugin v5+
- **\$ts-checker5-webpack-watch** &mdash; adds errors and warnings reported by the fork-ts-checker-webpack-plugin v5+ while in watch mode
- **\$ts-checker5-eslint-webpack** &mdash; adds ESLint errors and warnings reported by the fork-ts-checker-webpack-plugin v5+
- **\$ts-checker5-eslint-webpack-watch** &mdash; adds ESLint errors and warnings reported by the fork-ts-checker-webpack-plugin v5+ while in watch mode
- **\$tslint-webpack** &mdash; adds lint warnings reported by tslint-loader
- **\$tslint-webpack-watch** &mdash; adds lint warnings reported by tslint-loader while in watch mode

## Usage

The following example shows how to add problem matchers to your project:

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
			"problemMatcher": ["$ts-webpack-watch", "$tslint-webpack-watch"]
		}
	]
}
```

👉 In order for **\$ts-webpack-watch**, **\$ts-checker-webpack-watch**, **\$ts-checker-eslint-webpack-watch**, and **\$tslint-webpack-watch** to work properly, you must add `--info-verbosity verbose` to your webpack watch command e.g. `webpack --watch --info-verbosity verbose` as this instructs webpack to output lifecycle event messages for each re-compile

👉 In order for **\$ts-checker5-webpack**, **\$ts-checker5-webpack-watch**, **\$ts-checker5-eslint-webpack**, and **\$ts-checker5-eslint-webpack-watch** to work properly, you must set `formatter: 'basic'` in your [fork-ts-checker-webpack-plugin options](https://github.com/TypeStrong/fork-ts-checker-webpack-plugin/tree/alpha#options) and add `--info-verbosity verbose` to your webpack watch command e.g. `webpack --watch --info-verbosity verbose` as this instructs webpack to output lifecycle event messages for each re-compile

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
