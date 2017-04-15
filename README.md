# api documentation for  [sanitize-html (v1.14.1)](https://github.com/punkave/sanitize-html#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-sanitize-html.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-sanitize-html) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-sanitize-html.svg)](https://travis-ci.org/npmdoc/node-npmdoc-sanitize-html)
#### Clean up user-submitted HTML, preserving whitelisted elements and whitelisted attributes on a per-element basis

[![NPM](https://nodei.co/npm/sanitize-html.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/sanitize-html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-sanitize-html/build/apidoc.html)

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
    "version": "1.14.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module sanitize-html](#apidoc.module.sanitize-html)
1.  [function <span class="apidocSignatureSpan"></span>sanitize-html (html, options, _recursing)](#apidoc.element.sanitize-html.sanitize-html)
1.  [function <span class="apidocSignatureSpan">sanitize-html.</span>simpleTransform (newTagName, newAttribs, merge)](#apidoc.element.sanitize-html.simpleTransform)
1.  [function <span class="apidocSignatureSpan">sanitize-html.</span>toString ()](#apidoc.element.sanitize-html.toString)
1.  object <span class="apidocSignatureSpan">sanitize-html.</span>defaults



# <a name="apidoc.module.sanitize-html"></a>[module sanitize-html](#apidoc.module.sanitize-html)

#### <a name="apidoc.element.sanitize-html.sanitize-html"></a>[function <span class="apidocSignatureSpan"></span>sanitize-html (html, options, _recursing)](#apidoc.element.sanitize-html.sanitize-html)
- description and source-code
```javascript
function sanitizeHtml(html, options, _recursing) {
  var result = '';

  function Frame(tag, attribs) {
    var that = this;
    this.tag = tag;
    this.attribs = attribs || {};
    this.tagPosition = result.length;
    this.text = ''; // Node inner text

    this.updateParentNodeText = function() {
      if (stack.length) {
          var parentFrame = stack[stack.length - 1];
          parentFrame.text += that.text;
      }
    };
  }

  if (!options) {
    options = sanitizeHtml.defaults;
    options.parser = htmlParserDefaults;
  } else {
    options = extend(sanitizeHtml.defaults, options);
    if (options.parser) {
      options.parser = extend(htmlParserDefaults, options.parser);
    } else {
      options.parser = htmlParserDefaults;
    }
  }

  // Tags that contain something other than HTML, or where discarding
  // the text when the tag is disallowed makes sense for other reasons.
  // If we are not allowing these tags, we should drop their content too.
  // For other tags you would drop the tag but keep its content.
  var nonTextTagsArray = options.nonTextTags || [ 'script', 'style', 'textarea' ];
  var allowedAttributesMap;
  var allowedAttributesGlobMap;
  if(options.allowedAttributes) {
    allowedAttributesMap = {};
    allowedAttributesGlobMap = {};
    each(options.allowedAttributes, function(attributes, tag) {
      allowedAttributesMap[tag] = [];
      var globRegex = [];
      attributes.forEach(function(name) {
        if(name.indexOf('*') >= 0) {
          globRegex.push(quoteRegexp(name).replace(/\\\*/g, '.*'));
        } else {
          allowedAttributesMap[tag].push(name);
        }
      });
      allowedAttributesGlobMap[tag] = new RegExp('^(' + globRegex.join('|') + ')$');
    });
  }
  var allowedClassesMap = {};
  each(options.allowedClasses, function(classes, tag) {
    // Implicitly allows the class attribute
    if(allowedAttributesMap) {
      if (!has(allowedAttributesMap, tag)) {
        allowedAttributesMap[tag] = [];
      }
      allowedAttributesMap[tag].push('class');
    }

    allowedClassesMap[tag] = classes;
  });

  var transformTagsMap = {};
  var transformTagsAll;
  each(options.transformTags, function(transform, tag) {
    var transFun;
    if (typeof transform === 'function') {
      transFun = transform;
    } else if (typeof transform === "string") {
      transFun = sanitizeHtml.simpleTransform(transform);
    }
    if (tag === '*') {
      transformTagsAll = transFun;
    } else {
      transformTagsMap[tag] = transFun;
    }
  });

  var depth = 0;
  var stack = [];
  var skipMap = {};
  var transformMap = {};
  var skipText = false;
  var skipTextDepth = 0;

  var parser = new htmlparser.Parser({
    onopentag: function(name, attribs) {
      if (skipText) {
        skipTextDepth++;
        return;
      }
      var frame = new Frame(name, attribs);
      stack.push(frame);

      var skip = false;
      var hasText = frame.text ? true : false;
      var transformedTag;
      if (has(transformTagsMap, name)) {
        transformedTag = transformTagsMap[name](name, attribs);

        frame.attribs = attribs = transformedTag.attribs;

        if (transformedTag.text !== undefined) {
          frame.innerText = transformedTag.text;
        }

        if (name !== transformedTag.tagName) {
          frame.name = name = transformedTag.tagName;
          transformMap[depth] = transformedTag.tagName;
        }
      }
      if (transformTagsAll) {
        transformedTag = transformTagsAll(name, attribs);

        frame.attribs = attribs = transformedTag.attribs;
        if (name !== transformedTag.tagName) {
          frame.name = name = transformedTag.tagName;
          transformMap[depth] = transformedTag.tagName;
        }
      }

      if (options.allowedTags && options.allowedTags.indexOf(name) === -1) {
        skip = true;
        if (nonTextTagsArray.indexOf(name) !== -1) {
          skipText = true;
          skipTextDepth = 1;
        }
        skipMap[depth] = true;
      }
      depth++;
      if (skip) {
        // We want the contents but not this tag ...
```
- example usage
```shell
n/a
```

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

#### <a name="apidoc.element.sanitize-html.toString"></a>[function <span class="apidocSignatureSpan">sanitize-html.</span>toString ()](#apidoc.element.sanitize-html.toString)
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
