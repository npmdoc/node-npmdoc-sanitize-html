# npmdoc-sanitize-html

#### basic api documentation for  [sanitize-html (v1.14.1)](https://github.com/punkave/sanitize-html#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-sanitize-html.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-sanitize-html) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-sanitize-html.svg)](https://travis-ci.org/npmdoc/node-npmdoc-sanitize-html)

#### Clean up user-submitted HTML, preserving whitelisted elements and whitelisted attributes on a per-element basis

[![NPM](https://nodei.co/npm/sanitize-html.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/sanitize-html)

- [https://npmdoc.github.io/node-npmdoc-sanitize-html/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/screenCapture.npmPackageDependencyTree.svg)



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
            "name": "alexgilbert"
        },
        {
            "name": "austinstarin"
        },
        {
            "name": "boutell"
        },
        {
            "name": "colpanik"
        },
        {
            "name": "grdunn"
        },
        {
            "name": "jimmyh"
        },
        {
            "name": "kyjoya"
        },
        {
            "name": "mcoppola"
        },
        {
            "name": "stuartromanek"
        }
    ],
    "name": "sanitize-html",
    "optionalDependencies": {},
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
    "version": "1.14.1",
    "bin": {}
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
