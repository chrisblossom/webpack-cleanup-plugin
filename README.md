# webpack-cleanup-plugin

This [webpack](http://webpack.github.io) plugin cleans up the extraneous files
from the webpack's output path.

Since it runs when the compile process is finished, it is useful when building
on production to remove the assets created by previous builds.

```
npm install webpack-cleanup-plugin --save-dev
```

[![npm version](https://img.shields.io/npm/v/webpack-cleanup-plugin.svg?style=flat-square)](https://www.npmjs.com/package/webpack-cleanup-plugin)
[![npm downloads](https://img.shields.io/npm/dm/webpack-cleanup-plugin.svg?style=flat-square)](http://npm-stat.com/charts.html?package=webpack-cleanup-plugin)
[![Build Status](https://img.shields.io/travis/gpbl/webpack-cleanup-plugin.svg?style=flat-square)](https://travis-ci.org/gpbl/webpack-cleanup-plugin)

⚠️ **Beware!** This plugins actually delete files. Make sure it's safe for your app
to delete files not generated by webpack. Use the `exclude` option if you want to
keep files that are not webpack assets.

## Usage

Install via npm:

```
npm install webpack-cleanup-plugin --save-dev
```

Then add the plugin to the `plugins` array in your webpack's config, e.g.:

```js
// webpack.config.js
import WebpackCleanupPlugin from 'webpack-cleanup-plugin';
const config = {
  output: {
    path: "/my/output/path"
  },
  // ...
  plugins: [
    new WebpackCleanupPlugin()
  ]
}
export default config;
```

### Options

* If you want to keep some files in the output path, e.g. a `stats.json` file generated from some other
plugins, use the **`exclude`** Array option. It accepts globbing as in [minimatch](https://github.com/isaacs/minimatch).

```js
// Do not delete `stats.json`, `important.json`, and everything in `folder`
new WebpackCleanupPlugin({
  exclude: ["stats.json", "important.js", "folder/**/*"],
})
```

* To only remove file assets created directly by current Webpack build, use the **`cleanupOnlyLastBuild`** option:

```js
new WebpackCleanupPlugin({
  cleanupOnlyLastBuild: true,
})
```

* To mute the console output, use the **`quiet`** option:

```js
new WebpackCleanupPlugin({
  quiet: true,
})
```

* To print the list of the files that will be deleted without actually deleting them, use the **`preview`** option:

```js
new WebpackCleanupPlugin({
  preview: true,
})
```
