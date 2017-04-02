# api documentation for  [sanitize-html (v1.14.1)](https://github.com/punkave/sanitize-html#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-sanitize-html.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-sanitize-html) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-sanitize-html.svg)](https://travis-ci.org/npmdoc/node-npmdoc-sanitize-html)
#### Clean up user-submitted HTML, preserving whitelisted elements and whitelisted attributes on a per-element basis

[![NPM](https://nodei.co/npm/sanitize-html.png?downloads=true)](https://www.npmjs.com/package/sanitize-html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-sanitize-html_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-sanitize-html/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "P'unk Avenue LLC"
    },
    "bugs": {
        "url": "https://github.com/punkave/sanitize-html/issues"
    },
    "dependencies": {
        "htmlparser2": "^3.9.0",
        "regexp-quote": "0.0.0",
        "xtend": "^4.0.0"
    },
    "description": "Clean up user-submitted HTML, preserving whitelisted elements and whitelisted attributes on a per-element basis",
    "devDependencies": {
        "browserify": "^13.0.1",
        "mocha": "^2.5.3",
        "uglify-js": "^2.6.2"
    },
    "directories": {},
    "dist": {
        "shasum": "730ffa2249bdf18333effe45b286173c9c5ad0b8",
        "tarball": "https://registry.npmjs.org/sanitize-html/-/sanitize-html-1.14.1.tgz"
    },
    "gitHead": "fb89a712ba29bed52d5b2a0931b99ed7edf0f00c",
    "homepage": "https://github.com/punkave/sanitize-html#readme",
    "keywords": [
        "html",
        "parser",
        "sanitizer",
        "html",
        "sanitizer",
        "apostrophe"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "alexgilbert",
            "email": "alex@punkave.com"
        },
        {
            "name": "austinstarin",
            "email": "austin@punkave.com"
        },
        {
            "name": "boutell",
            "email": "boutell@boutell.com"
        },
        {
            "name": "colpanik",
            "email": "kerry@punkave.com"
        },
        {
            "name": "grdunn",
            "email": "grdunn@gmail.com"
        },
        {
            "name": "jimmyh",
            "email": "jimmy@punkave.com"
        },
        {
            "name": "kyjoya",
            "email": "kyleejacker@gmail.com"
        },
        {
            "name": "mcoppola",
            "email": "coppola@punkave.com"
        },
        {
            "name": "stuartromanek",
            "email": "stuart@punkave.com"
        }
    ],
    "name": "sanitize-html",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/punkave/sanitize-html.git"
    },
    "scripts": {
        "build": "browserify index.js > dist/sanitize-html.js --standalone 'sanitizeHtml'",
        "minify": "npm run build && uglifyjs dist/sanitize-html.js > dist/sanitize-html.min.js",
        "prebuild": "npm run test && rm -rf dist && mkdir dist",
        "test": "mocha test/test.js"
    },
    "version": "1.14.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module sanitize-html](#apidoc.module.sanitize-html)
1.  [function <span class="apidocSignatureSpan">sanitize-html.</span>simpleTransform (newTagName, newAttribs, merge)](#apidoc.element.sanitize-html.simpleTransform)
1.  object <span class="apidocSignatureSpan">sanitize-html.</span>defaults



# <a name="apidoc.module.sanitize-html"></a>[module sanitize-html](#apidoc.module.sanitize-html)

#### <a name="apidoc.element.sanitize-html.simpleTransform"></a>[function <span class="apidocSignatureSpan">sanitize-html.</span>simpleTransform (newTagName, newAttribs, merge)](#apidoc.element.sanitize-html.simpleTransform)
- description and source-code
```javascript
simpleTransform = function (newTagName, newAttribs, merge) {
  merge = (merge === undefined) ? true : merge;
  newAttribs = newAttribs || {};

  return function(tagName, attribs) {
    var attrib;
    if (merge) {
      for (attrib in newAttribs) {
        attribs[attrib] = newAttribs[attrib];
      }
    } else {
      attribs = newAttribs;
    }

    return {
      tagName: newTagName,
      attribs: attribs
    };
  };
}
```
- example usage
```shell
...
You can specify the '*' wildcard instead of a tag name to transform all tags.

There is also a helper method which should be enough for simple cases in which you want to change the tag and/or add some attributes
:

'''js
clean = sanitizeHtml(dirty, {
  transformTags: {
    'ol': sanitizeHtml.simpleTransform('ul', {class: 'foo'}),
  }
});
'''

The 'simpleTransform' helper method has 3 parameters:

'''js
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
