# api documentation for  [tesseract.js (v1.0.10)](https://github.com/naptha/tesseract.js)  [![npm package](https://img.shields.io/npm/v/npmdoc-tesseract.js.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-tesseract.js) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-tesseract.js.svg)](https://travis-ci.org/npmdoc/node-npmdoc-tesseract.js)
#### Pure Javascript Multilingual OCR

[![NPM](https://nodei.co/npm/tesseract.js.png?downloads=true)](https://www.npmjs.com/package/tesseract.js)

[![apidoc](https://npmdoc.github.io/node-npmdoc-tesseract.js/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-tesseract.js_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-tesseract.js/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-tesseract.js/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-tesseract.js/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": "",
    "browser": {
        "./src/node/index.js": "./src/browser/index.js"
    },
    "bugs": {
        "url": "https://github.com/naptha/tesseract.js/issues"
    },
    "dependencies": {
        "file-type": "^3.8.0",
        "is-url": "^1.2.2",
        "jpeg-js": "^0.2.0",
        "level-js": "^2.2.4",
        "node-fetch": "^1.6.3",
        "object-assign": "^4.1.0",
        "png.js": "^0.2.1",
        "tesseract.js-core": "^1.0.2"
    },
    "description": "Pure Javascript Multilingual OCR",
    "devDependencies": {
        "babel-preset-es2015": "^6.16.0",
        "babelify": "^7.3.0",
        "browserify": "^13.1.0",
        "envify": "^3.4.1",
        "http-server": "^0.9.0",
        "pako": "^1.0.3",
        "watchify": "^3.7.0"
    },
    "directories": {},
    "dist": {
        "shasum": "e11a96ae76147939d9218f88e287fb69414b1e5d",
        "tarball": "https://registry.npmjs.org/tesseract.js/-/tesseract.js-1.0.10.tgz"
    },
    "gitHead": "fc15b0ef43cbf2d8729f8db2ef06a16b2497a16e",
    "homepage": "https://github.com/naptha/tesseract.js",
    "license": "Apache-2.0",
    "main": "src/index.js",
    "maintainers": [
        {
            "name": "antimatter15",
            "email": "antimatter15@gmail.com"
        },
        {
            "name": "bijection",
            "email": "guillermo@cdbzb.com"
        }
    ],
    "name": "tesseract.js",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/naptha/tesseract.js.git"
    },
    "scripts": {
        "build": "browserify src/index.js -t [ babelify --presets [ es2015 ] ] -o dist/tesseract.js --standalone Tesseract && browserify src/browser/worker.js -t [ babelify --presets [ es2015 ] ] -o dist/worker.js",
        "release": "npm run build && git commit -am 'new release' && git push && git tag 'jq -r '.version' package.json' && git push origin --tags && npm publish",
        "start": "watchify src/index.js  -t [ envify --NODE_ENV development ] -t [ babelify --presets [ es2015 ] ] -o dist/tesseract.dev.js --standalone Tesseract & watchify src/browser/worker.js  -t [ envify --NODE_ENV development ] -t [ babelify --presets [ es2015 ] ] -o dist/worker.dev.js & http-server -p 7355",
        "test": "echo \"Error: no test specified\" & exit 1"
    },
    "version": "1.0.10"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module tesseract.js](#apidoc.module.tesseract.js)
1.  [function <span class="apidocSignatureSpan">tesseract.js.</span>create (workerOptions)](#apidoc.element.tesseract.js.create)
1.  object <span class="apidocSignatureSpan">tesseract.js.</span>_currentJob
1.  object <span class="apidocSignatureSpan">tesseract.js.</span>_queue
1.  object <span class="apidocSignatureSpan">tesseract.js.</span>worker
1.  object <span class="apidocSignatureSpan">tesseract.js.</span>workerOptions
1.  string <span class="apidocSignatureSpan">tesseract.js.</span>version



# <a name="apidoc.module.tesseract.js"></a>[module tesseract.js](#apidoc.module.tesseract.js)

#### <a name="apidoc.element.tesseract.js.create"></a>[function <span class="apidocSignatureSpan">tesseract.js.</span>create (workerOptions)](#apidoc.element.tesseract.js.create)
- description and source-code
```javascript
function create(workerOptions){
	workerOptions = workerOptions || {};
	var worker = new TesseractWorker(objectAssign({}, adapter.defaultOptions, workerOptions))
	worker.create = create;
	worker.version = version;
	return worker;
}
```
- example usage
```shell
...
## Local Installation

In the browser, 'tesseract.js' simply provides the API layer. Internally, it opens a WebWorker to handle requests. That worker itself
 loads code from the Emscripten-built 'tesseract.js-core' which itself is hosted on a CDN. Then it dynamically loads language files
 hosted on another CDN.

Because of this we recommend loading 'tesseract.js' from a CDN. But if you really need to have all your files local, you can use
 the 'Tesseract.create' function which allows you to specify custom paths for workers, languages, and core.

'''javascript
window.Tesseract = Tesseract.create({
    workerPath: '/path/to/worker.js',
    langPath: 'https://cdn.rawgit.com/naptha/tessdata/gh-pages/3.02/',
    corePath: 'https://cdn.rawgit.com/naptha/tesseract.js-core/0.1.0/index.js',
})
'''

### corePath
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
