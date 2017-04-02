# api documentation for  [gulp-gzip (v1.4.0)](https://github.com/jstuckey/gulp-gzip/)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-gzip.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-gzip) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-gzip.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-gzip)
#### Gzip plugin for gulp.

[![NPM](https://nodei.co/npm/gulp-gzip.png?downloads=true)](https://www.npmjs.com/package/gulp-gzip)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-gzip/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-gzip_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-gzip/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-gulp-gzip/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "Jeremy Stuckey",
        "email": "jeremystuckey@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/jstuckey/gulp-gzip/issues"
    },
    "dependencies": {
        "bytes": "^0.3.0",
        "gulp-util": "^2.2.14",
        "stream-to-array": "~1.0.0",
        "through2": "^0.4.1"
    },
    "description": "Gzip plugin for gulp.",
    "devDependencies": {
        "gulp": "^3.6.2",
        "gulp-clean": "^0.2.4",
        "gulp-filter": "^0.3.1",
        "gulp-jshint": "~1.5.4",
        "gulp-mocha": "^0.4.1",
        "gulp-rename": "^1.2.0",
        "gulp-tap": "^0.1.1",
        "gulp-watch": "^0.6.4",
        "jshint-stylish": "~0.1.5",
        "mocha": "^1.18.2",
        "nid": "^0.3.2",
        "should": "^3.2.0-beta1"
    },
    "directories": {},
    "dist": {
        "shasum": "5ff8dff837cac2ebc2c89743dc0ac76e2be5e6c2",
        "tarball": "https://registry.npmjs.org/gulp-gzip/-/gulp-gzip-1.4.0.tgz"
    },
    "engines": {
        "node": ">= 0.10.0"
    },
    "homepage": "https://github.com/jstuckey/gulp-gzip/",
    "keywords": [
        "compress",
        "gulpplugin",
        "gzip"
    ],
    "licenses": [
        {
            "type": "MIT",
            "url": "http://github.com/jstuckey/gulp-gzip/raw/master/LICENSE"
        }
    ],
    "main": "index.js",
    "maintainers": [
        {
            "name": "jstuckey",
            "email": "jeremystuckey@gmail.com"
        }
    ],
    "name": "gulp-gzip",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/jstuckey/gulp-gzip.git"
    },
    "scripts": {
        "test": "gulp"
    },
    "version": "1.4.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-gzip](#apidoc.module.gulp-gzip)
1.  object <span class="apidocSignatureSpan">gulp-gzip.</span>utils

#### [module gulp-gzip.utils](#apidoc.module.gulp-gzip.utils)
1.  [function <span class="apidocSignatureSpan">gulp-gzip.utils.</span>merge (target, source)](#apidoc.element.gulp-gzip.utils.merge)
1.  [function <span class="apidocSignatureSpan">gulp-gzip.utils.</span>threshold (obj)](#apidoc.element.gulp-gzip.utils.threshold)



# <a name="apidoc.module.gulp-gzip"></a>[module gulp-gzip](#apidoc.module.gulp-gzip)



# <a name="apidoc.module.gulp-gzip.utils"></a>[module gulp-gzip.utils](#apidoc.module.gulp-gzip.utils)

#### <a name="apidoc.element.gulp-gzip.utils.merge"></a>[function <span class="apidocSignatureSpan">gulp-gzip.utils.</span>merge (target, source)](#apidoc.element.gulp-gzip.utils.merge)
- description and source-code
```javascript
function merge(target, source) {
  if (typeof source === 'undefined') source = {};

  Object.keys(source).forEach(function(key) {
    if (key === 'threshold') {
      target[key] = threshold(source[key]);
    } else {
      target[key] = source[key];
    }
  });

  return target;
}
```
- example usage
```shell
...
// Combine user defined options with default options
var defaultConfig = {
  append: true,
  threshold: false,
  gzipOptions: {},
  skipGrowingFiles: false
};
var config = utils.merge(defaultConfig, options);

// Create a through2 object stream. This is our plugin export
var stream = through2.obj(gulpGzip);

// Expose the config so we can test it
stream.config = config;
...
```

#### <a name="apidoc.element.gulp-gzip.utils.threshold"></a>[function <span class="apidocSignatureSpan">gulp-gzip.utils.</span>threshold (obj)](#apidoc.element.gulp-gzip.utils.threshold)
- description and source-code
```javascript
function threshold(obj) {
  var ret;

  switch (typeof obj) {
    case 'string':
      ret = bytes(obj) < 150 ? 150 : bytes(obj);
      break;
    case 'number':
      ret = obj < 150 ? 150 : obj;
      break;
    case 'boolean':
      ret = obj === false ? false : 150;
      break;
    default:
      throw new Error('threshold must be String|Number|Boolean');
  }

  return ret;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
