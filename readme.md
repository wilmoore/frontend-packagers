Front-End Package Manager Comparison
============================================================


Why do this?
------------------------------------------------------------

It is about time for front-end developers to have a decent package manager. Front-end development is [serious business](http://qr.ae/8aIrF) and there is no good reason for us to continue with sub-par tools or no tools at all.

I appreciate the effort that has gone into all of these. It is awesome to see really talented developers taking on the task and sharing the result with the rest of us.


Who are you?
------------------------------------------------------------

- I am a full-stack software developer
- I love what I do
- I love sharing what I've learned
- Hit me up at [@wilmoore][@wilmoore], [@github][@github], and [@linkedin][@linkedin]


The contenders
------------------------------------------------------------

The following tools have caught my attention:

-   [bower][bower]
-   [component][component]
-   [jam][jam]
-   [volo][volo]


**NOTES**:

-  *[component][component]* is more of a concept and a framework for building and distributing front-end components. If you'd like to read more on this distinction, check out the [issue #1 thread](https://github.com/wilmoore/frontend-packagers/issues/1).
-  *[bower][bower]* is meant to be consumed by higher-level tools and frameworks. What this means in practice is:
  -  **(1)** _bring your own CJS/AMD loader_.
  -  **(2)** _bring your own build tool_.
  -  **(3)** _bring your own organization conventions_.
  -  **(4)** _ultimately, coupled with either *[make][make]* or *[grunt][grunt]*, [bower][bower] looks like a viable option_


What is a package manager?
------------------------------------------------------------

A package manager is a tool that allows you to specify a list of dependencies for your library or application. The tools depicted here are similar in scope to [Bundler](http://gembundler.com/), [NPM](https://npmjs.org/), or [Composer](http://getcomposer.org/).


How is this thing evaluated?
------------------------------------------------------------

Since tool choice is extremely subjective, you (and/or your team) should come up with your own weighting system and score each tool accordingly.


Configuration File
------------------------------------------------------------

The following table provides the name of the "manifest" file where you specify dependencies and/or the details of your package.


  Configuration          |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `filename`             |  component.json         |  component.json         |  [package.json][package]|  [package.json][package]


Sample *[bower][bower]* enabled `component.json` file:

    {
      "name": "project-name",
      "version": "x.x.x",
      "description": "A project description provided by the author",
      "homepage": "https://github.com/author/repo",
      "license" : "[PLEASE include a license URL if terms are included]",
      "main": [
        "./source.js",
        "./source.min.js"
      ],
      "dependencies": {
        "jquery": "~x.x.x"
      },
      "keywords": [
        "use",
        "intelligent",
        "keywords",
        "for",
        "search"
      ],
      "author": {
        "name": "Tool Author",
        "web": "http://website.com"
      }
    }


Sample *[component][component]* enabled `component.json` file:

    {

      "name":        "tip",
      "repo":        "component/tip",
      "description": "Tip component",
      "version":     "0.0.1",
      "keywords":    ["tooltip", "tip", "ui"],
      "dependencies": {
        "component/emitter": "*",
        "component/jquery":  "*"
      },
      "scripts": ["index.js", "template.js"],
      "styles":  ["tip.css"]

    }


Sample *[jam][jam]* enabled `package.json` file:

    {

      "name":        "csbp",
      "version":     "0.0.1",
      "description": "A Non-Framework Client-Side JavaScript/HTML5 Project Boilerplate",

      "dependencies": {
        "jamjs":         "*",
        "grunt-contrib": "*"
      },

      "devDependencies": {
        "chai":          "*",
        "mocha":         "*",
        "sinon":         "*",
        "grunt-mocha":   "*"
      },

      "jam": {
        "packageDir": "src/libs/js",
        "baseUrl":    "src/main/js"
      }

    }


Sample *[volo][volo]* enabled `package.json` file:

    {

      "name":            "csbp",
      "version":         "0.0.1",
      "description":     "A Non-Framework Client-Side JavaScript/HTML5 Project Boilerplate",

      "dependencies": {
      },

      "devDependencies": {
        "yeti":          "*",
        "docco":         "*",
        "jshint":        "*",
        "chai":          "*",
        "mocha":         "*",
        "sinon":         "*"
      },

      "amd":  {},

      "volo": {
        "baseUrl":       "src/js/lib",

        "dependencies":  {
          "page":        "github:visionmedia/page.js",
          "requirejs":   "*"
        }
      }

    }


**NOTES**:

-  *[bower][bower]* lacks the notion of `devDependencies`. This is not an issue with the package managers that support `package.json`. There is an interesting discussion regarding some of the [reasoning](https://github.com/twitter/bower/pull/62#issuecomment-8630878) [behind](https://github.com/twitter/bower/pull/62#issuecomment-8627442) *[bower][bower]* not supporting the well-known [package.json](https://github.com/twitter/bower/pull/62) format.
-   When using *[volo][volo]*, I would suggest using the flags:
      -   `-nostamp`: mitigates the reformating of your `package.json` file
      -   `skipexists`: skip existing dependencies without noisy warnings


Package Installation Location
------------------------------------------------------------

The following table details where each tool stores downloaded packages.

 
  Path                   |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `default path`         |  ./components           |  ./components           |  ./jam                  |  ./js, ./scripts, ./
  `custom path`          |  [.bowerrc][bowerrc]    |  --out dir              |  jam.packageDir         |  volo.{baseDir,baseUrl}, amd.baseDir


**NOTES**:

*[volo][volo]* has a fairly complex algorithm.

If not defined in `package.json` it:

-   Looks for a ./js directory
-   Looks for a ./scripts directory
-   Otherwise, the current working directory is used


Development Dependencies
------------------------------------------------------------

The following table details whether each tool allows specifying development dependencies.


  Development Dependencies |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:--------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `devDependencies`        |  ✗                      |  ✓                      |  ✓                      |  ✓                      


**NOTES**:

-  Since *[jam][jam]* and *[volo][volo]* use `package.json`, this just works; however, *[component][component]* re-implments this functionality [here](https://github.com/component/component/commit/f01bf04c674cbd13dcef5a4fefdefdeed268344c).


Responsibilities
------------------------------------------------------------

The following table details the responsibilities the given tool takes on.


  Responsibilities         |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:--------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `package management`     |  ✓                      |  ✓                      |  ✓                      |  ✓                      
  `project scaffolding`    |  ✗                      |  ✗                      |  ✗                      |  ✓                     
  `build automation`       |  ✗                      |  ✗                      |  ✗                      |  ✓                      
  `script/module loading`  |  ✗                      |  ✗                      |  ✓                      |  ✗                      
  `compile/build`          |  ✗                      |  ✓                      |  ✗                      |  ✗                      


**NOTES**:

-  An interesting comparison of [volo and grunt](https://github.com/volojs/volo/wiki/volo-and-grunt).


Build/Compile
------------------------------------------------------------

The following table details which tools require a build/compile step during development.


  Build/Compile?         |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `?`                    |  ✗                      |  ✓ (component build)    |  ✗                      |  ✗                      


**NOTES**:

-  N/A


Central Registry
------------------------------------------------------------

The following table details which tools expose a central "registry".


  Registry?              |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `?`                    |  ✓                      |  ✗                      |  ✓                      |  ✗                      


**NOTES**:

-  The *[bower][bower]* "registry" is only a convenient [shorturl service](https://github.com/twitter/bower/issues/10#issuecomment-8547463).
-  It is good ettiquite is to use [user/package namespacing][packagist] when registering a package.


Package installation sources
------------------------------------------------------------

The following table details the method by which each tool is able to retrieve packages.


  Source                 |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `git / github`         |  ✓                      |  ✓                      |  ✓ (CLI ONLY)           |  ✓                      
  `private repositories` |  ✓                      |  ✓                      |  ✓                      |  ✓ (SEE NOTES BELOW)
  `local repositories`   |  ✓                      |  ✓                      |  ✗                      |  ✗
  `zip / tarball`        |  ✓                      |  ✗                      |  ✓ (CLI ONLY)           |  ✓ (ZIPBALL ONLY)       
  `HTTP/HTTPS URL`       |  ✓                      |  ✗                      |  ✗                      |  ✗                      
  `NPM`                  |  ✓                      |  ✗                      |  ✗                      |  ✗                      
  `registry`             |  ✓                      |  ✗                      |  ✗                      |  ✗                      


**NOTES**:

-   I've never been on a serious team where no support for `private repositories` would be acceptable. If this is important to you, it seems that your best options are currently *[bower][bower]*, *[component][component]* and *[jam][jam]*.
-   While *[volo][volo]* doesn't actually claim to have explicit support for `private repositories`, you can achieve the notion of `private repositories` by providing a URL to a single JavaScript source file (github and github:enterprise allow you to link to a `raw` file) or you can specify a URL to a zipball. There are a few more tricks that you can choose from listed [here](https://github.com/volojs/volo/wiki/Library-best-practices).
-   You can setup a private *[jam][jam]* free repo from [garden20](http://garden20.com/market/details/jam). Other details for a private repo can be found [here](https://github.com/caolan/jam/issues/53#issuecomment-10324992).

Speed
------------------------------------------------------------

The following table details the speed of each tool.


  Registry?              |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `~85 components`       |  ~80s                   |  ~10s                   |  ~80s                   |  ~80s                   


**NOTES**:

-  For most projects, speed won't be an issue; however, it may be more import for some.
-  These benchmarks were taken from the *[component](https://github.com/component/component#features)* documentation; thus depending on your setup and dependencies, YMMV.


Supported JavaScript Module formats
------------------------------------------------------------

The following table details the JavaScript format each tool expects/handles.


  Format                 |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `Global Script`        |  ✓                      |  ✓                      |  ✓                      |  ✓                      
  `AMD`                  |  ✓ (format agnostic)    |  ✗                      |  ✓                      |  ✓                      
  `CommonJS/NodeJS`      |  ✓ (format agnostic)    |  ✓ (bundles require)    |  ✗                      |  ✗                      
  `CommonJS (WRAPPED)`   |  ✓ (format agnostic)    |  ✗                      |  ✓                      |  ✓                      


**NOTES**:

There are several JavaScript formatting methodologies:


-  Global Script

         <script src="trim.js"></script>
         <script>
            var todo = new Todo({description: '', done: false});
         </script>

-  AMD

         define(['todo'], function(Todo){
            var todo = new Todo({description: '', done: false});
         });

-  CommonJS/NodeJS

         var Todo = require('todo');
         var todo = new Todo({description: '', done: false});

-  CommonJS (wrapped in an AMD-style define)

         define(function(require){
            var Todo = require('todo');
            var todo = new Todo({description: '', done: false});
         });


**NOTES**:

-  N/A


Module / Script Loader
------------------------------------------------------------

The following table details the module/script loader supported by each tool.


  Source                 |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `Bring your own loader`|  ✓                      |  ✗                      |  ✗                      |  ✓                      
  `Includes a Loader`    |  ✗                      |  ✓ (custom require)     |  ✓ (RequireJS)          |  ✗                      


**NOTES**:

Loaders that you might be interested in:

-   [inject](https://github.com/linkedin/inject)
-   [curl](https://github.com/cujojs/curl)
-   [requirejs](http://requirejs.org)
-   [cajon](https://github.com/requirejs/cajon)
-   [almond](https://github.com/jrburke/almond)
-   [Shepherd-js](http://xcambar.github.com/shepherd-js/)


Package Contents
------------------------------------------------------------

The following table details the the types of source files that can be contained in each package per tool.


  Source                 |  [bower][bower]         |  [component][component] |  [jam][jam]             |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `JavaScript`           |  ✓                      |  ✓                      |  ✓                      |  ✓                      
  `HTML`                 |  ✓                      |  ✓                      |  ✓                      |  ✗                      
  `CSS`                  |  ✓                      |  ✓                      |  ✓                      |  ✗                      


**NOTES**:

-  N/A


Final thoughts
------------------------------------------------------------

Each package manager is built by talented, responsive, and friendly developers. Ultimately, to evaluate for your team, you will have to put a weight on each category and score per your needs.

Library and component authors may want to consider:

-   Using a [UMD][umdjs] wrapper.
-   Authoring both a {component,package}.json for front-end and npm (where appropriate).
-   Adhering to these [Library best practices](https://github.com/volojs/volo/wiki/Library-best-practices) or something similar.


Complementary Resources
------------------------------------------------------------

Below are a list of resources that will likely be useful to you if you found this comparison useful:

-   [Landscaping With Front-end Tools](https://github.com/codylindley/frontend-tools)
-   [JavaScript: Noteworthy Tools & Libraries](http://jamesonjavascript.wordpress.com/2012/11/27/javascript-noteworthy-tools-libraries/)
-   [The State of Javascript Package Management](http://wibblycode.wordpress.com/2013/01/01/the-state-of-javascript-package-management/)
-   [Javascript loaders](http://owl.li/2skp29)


Contributing
------------------------------------------------------------

I am sure I've made a few gramatical and spelling errors. I've probably even made comparison errors in a few spots. Please feel free to speak up or submit a pull request.


Symbols Used
------------------------------------------------------------

✓
✗







[bower]:     http://twitter.github.com/bower/
[component]: https://github.com/component/component
[jam]:       http://jamjs.org
[volo]:      http://volojs.org
[requirejs]: http://requirejs.org/
[packagist]: http://packagist.org/about
[umdjs]:     https://github.com/umdjs/umd
[make]:      http://www.gnu.org/software/make/
[grunt]:     http://gruntjs.com/
[bi18]:      https://github.com/twitter/bower/issues/18
[package]:   http://package.json.jit.su
[bowerrc]:   https://github.com/twitter/bower#bower-configuration

[@wilmoore]: http://twitter.com/wilmoore
[@github]:   http://github.com/wilmoore
[@linkedin]: http://www.linkedin.com/in/wilmoore
