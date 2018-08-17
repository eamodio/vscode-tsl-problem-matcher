# TypeScript + Webpack Problem Matchers for Visual Studio Code

Provides [problem matchers](https://code.visualstudio.com/docs/editor/tasks#_processing-task-output-with-problem-matchers) for use with TypeScript projects using [Webpack](https://webpack.js.org/) with [ts-loader](https://github.com/TypeStrong/ts-loader) and/or [tslint-loader](https://github.com/wbuchwalter/tslint-loader).

## Features

Provides the following problem matchers:

- **$ts-webpack** &mdash; adds errors reported by ts-loader
- **$tslint-webpack** &mdash; adds lint warnings reported by tslint-loader
- **$ts-webpack-watch** &mdash; adds errors reported by ts-loader while in watch mode
- **$tslint-webpack-watch** &mdash; adds lint warnings reported by tslint-loader while in watch mode

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

👉 In order for **$ts-webpack-watch** and **$tslint-webpack-watch** to work properly, you must add `--info-verbosity verbose` to your webpack watch command e.g. `webpack --watch --env.development --info-verbosity verbose` as this instructs webpack to output lifecycle event messages for each re-compile

If you are returning multiple configurations from your `webpack.config.js` note that currently `--info-verbosity verbose` causes webpack to crash &mdash; See 🐛 [webpack/webpack#7906](https://github.com/webpack/webpack/issues/7906)

You can also use **$ts-webpack-watch** and **$tslint-webpack-watch** as a base problem matcher for your own custom needs:

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
