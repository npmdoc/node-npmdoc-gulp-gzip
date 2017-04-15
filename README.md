# api documentation for  [gulp-gzip (v1.4.0)](https://github.com/jstuckey/gulp-gzip/)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-gzip.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-gzip) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-gzip.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-gzip)
#### Gzip plugin for gulp.

[![NPM](https://nodei.co/npm/gulp-gzip.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/gulp-gzip)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-gzip/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-gzip/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-gzip/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-gzip/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Jeremy Stuckey"
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
            "name": "jstuckey"
        }
    ],
    "name": "gulp-gzip",
    "optionalDependencies": {},
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
1.  [function <span class="apidocSignatureSpan"></span>gulp-gzip (options)](#apidoc.element.gulp-gzip.gulp-gzip)
1.  [function <span class="apidocSignatureSpan">gulp-gzip.</span>toString ()](#apidoc.element.gulp-gzip.toString)



# <a name="apidoc.module.gulp-gzip"></a>[module gulp-gzip](#apidoc.module.gulp-gzip)

#### <a name="apidoc.element.gulp-gzip.gulp-gzip"></a>[function <span class="apidocSignatureSpan"></span>gulp-gzip (options)](#apidoc.element.gulp-gzip.gulp-gzip)
- description and source-code
```javascript
gulp-gzip = function (options) {

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

  function gulpGzip(file, enc, done) {

<span class="apidocCodeCommentSpan">    /*jshint validthis: true */
</span>    var self = this;

    // Check for empty file
    if (file.isNull()) {
      // Pass along the empty file to the next plugin
      self.push(file);
      done();
      return;
    }

    // Call when finished with compression
    var finished = function(err, contents, wasCompressed) {
      if (err) {
        var error = new PluginError(PLUGIN_NAME, err, { showStack: true });
        self.emit('error', error);
        done();
        return;
      }

      var complete = function() {
        file.contents = contents;
        self.push(file);
        done();
      };

      var getFixedPath = function(filepath) {
        if (config.extension) {
          filepath += '.' + config.extension;
        } else if (config.preExtension) {
          filepath = filepath.replace(/(\.[^\.]+)$/, '.' + config.preExtension + '$1');
        } else if (config.append) {
          filepath += '.gz';
        }

        return filepath;
      };

      if (wasCompressed) {
        if (file.contentEncoding) {
          file.contentEncoding.push('gzip');
        } else {
          file.contentEncoding = [ 'gzip' ];
        }

        file.path = getFixedPath(file.path);
        complete();
      } else if (config.deleteMode) {
        var cwd = path.resolve(config.deleteModeCwd || process.cwd());
        var directory = typeof config.deleteMode === 'string' ? config.deleteMode : config.deleteMode(file);
        var filepath = path.resolve(cwd, directory, getFixedPath(file.relative));

        fs.exists(filepath, function(exists) {
          if(exists) {
            gutil.log(gutil.colors.green('Gzipped file ' + filepath + ' deleted'));
            fs.unlink(filepath, complete);
          } else {
            complete();
          }
        });
      } else {
        complete();
      }

      return;
    };

    compress(file.contents, config, finished);
  }

  return stream;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-gzip.toString"></a>[function <span class="apidocSignatureSpan">gulp-gzip.</span>toString ()](#apidoc.element.gulp-gzip.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
