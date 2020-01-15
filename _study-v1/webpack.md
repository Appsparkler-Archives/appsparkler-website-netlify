---
layout: post
title: Webpack
categories: study webpack
---

## What is?
1. `output.publicPath` - The path on the server from where the files will be references.  For ex. if your `build` folder is `dist`, you may want to set the public path to `/dist` if you are serving the root of your folder with `serve`.  Example here: https://github.com/appsparkler/webpacked/tree/examples/public-path - `yarn serve` and then visit `http://localhost:5000/dist`

## POCs from Documentation
- i. [Getting Started](https://webpack.js.org/guides/getting-started/) - [POC](https://github.com/appsparkler/poc/tree/webpack/i-getting-started)
- ii. [Asset Management](https://webpack.js.org/guides/asset-management/) - [POC](https://github.com/appsparkler/poc/tree/webpack/ii-asset-management)

## Important Links
- [Dependency Graph](https://webpack.js.org/concepts/dependency-graph/)
- Loaders:
  - Enhancing Image Loading process
    - [Image Webpack Loader](https://github.com/tcoopman/image-webpack-loader)
    - [URL Loader](https://webpack.js.org/loaders/url-loader)
- [The Manifest](https://webpack.js.org/concepts/manifest/)
- [Code Splitting](https://webpack.js.org/guides/code-splitting/)
- [Dynamic Imports](https://webpack.js.org/guides/code-splitting/#dynamic-imports)
  - A very good example of chunking without any chunking configuration
  - This happens due to `import()` syntax.  Webpack, while bundling, chunks-out the dynamically imported modules.
- [Bundle Analysis Tools](https://webpack.js.org/guides/code-splitting/#bundle-analysis)
- [Substitutions](https://webpack.js.org/configuration/output/#outputdevtoolmodulefilenametemplate)
  - for ex. `[name]`, `[contenthash]`, etc.

### Webpack Magic Comments
- [Medium Article by Tobias Koppers](https://medium.com/webpack/link-rel-prefetch-preload-in-webpack-51a52358f84c)
- [Preload Webpack Plugin by GoogleChromeLabs](https://github.com/GoogleChromeLabs/preload-webpack-plugin)
- Chunk Name: `import(/* webpackChunkName: "lodash" */ 'lodash')`
  - This will set the chunk-name in the `[name]` 
- Preload : `import(/* webpackPreload: true */ ChartingLibrary)`
  - Let's imagine a component `ChartComponent` which needs huge `ChartingLibrary`. It displays a `LoadingIndicator` when rendered and instantly does an on demand import of ChartingLibrary:
  - When a page which uses the `ChartComponent` is requested, the `charting-library-chunk` is also requested via `<link rel="preload">`. Assuming the page-chunk is smaller and finishes faster, the page will be displayed with a `LoadingIndicator`, until the already requested `charting-library-chunk` finishes. This will give a little load time boost since it only needs one round-trip instead of two. Especially in high-latency environments.
  - [Example Link](https://github.com/appsparkler/poc/tree/webpack/v-code-splitting-preloading-example)
- Pre-fetch : `import(/* webpackPrefetch: true */ './LoginModal')`
  - Helpful to load components in the background.
  - This is mainly to make the code readily available when the user needs it.
  - [Example Link](https://github.com/appsparkler/poc/tree/webpack/v-code-splitting-prefetching-example)

### Substitutions via [`TemplatePathPlugin`](https://github.com/webpack/webpack/blob/master/lib/TemplatedPathPlugin.js):
Template |	Description
---------|-------------
`[hash]` | 	The hash of the module identifier
`[contenthash]` | 	the hash of the content of a file, which is different for each asset
`[chunkhash]` | 	The hash of the chunk content
`[name]` | The module name
`[id]` | 	The module identifier
`[query]` | 	The module query, i.e., the string following ? in the filename
`[function]` | 	The function, which can return filename `[string]`


### Substitutions via [`ModuleFilenameHelpers`](https://github.com/webpack/webpack/blob/master/lib/ModuleFilenameHelpers.js)
Template |	Description
---------|--------------
`absolute-resource-path` | The absolute filename
`all-loaders` | Automatic and explicit loaders and params up to the name of the first loader
`hash` | 	The hash of the module identifier
`id` | 	The module identifier
`loaders` | 	Explicit loaders and params up to the name of the first loader
`resource` | 	The path used to resolve the file and any query params used on the first loader
`resource-path` | 	The path used to resolve the file without any query params
`namespace` | 	The modules namespace. This is usually the library name when building as a library, empty otherwise
