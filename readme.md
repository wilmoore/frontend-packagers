Front-End Package Manager Comparison
============================================================


Why do this?
------------------------------------------------------------

It is about time for front-end developers to have a decent package manager. Front-end development is [serious business](http://qr.ae/8aIrF) and there is no good reason for us to continue with sub-par tools or no tools at all.

I appreciate the effort that has gone into all of these. It is awesome to see really talented developers taking on the task and sharing the result with the rest of us.


The contenders
------------------------------------------------------------

The following tools have caught my attention:

-   [bower][bower]
-   [component][component]
-   [jam][jam]
-   [volo][volo]


**NOTES**:

-  *[component][component]* is more of a concept and a framework for building and distributing front-end components. If you'd like to read more on this distinction, check out the [issue #1 thread](https://github.com/wilmoore/frontend-packagers/issues/1).
-  *[bower][bower]* is meant to be consumed by higher-level tools and
frameworks. What this means in practice is, **(1)** _bring your own CJS/AMD loader_. **(2)** _bring your own build tool_.


What is a package manager?
------------------------------------------------------------

A package manager is a tool that allows you to specify a list of dependencies for your library or application. The tools depicted here are similar in scope to [Bundler](http://gembundler.com/), [NPM](https://npmjs.org/), or [Composer](http://getcomposer.org/).


How is this thing evaluated?
------------------------------------------------------------

Since tool choice is extremely subjective, you (and/or your team) should come up with your own weighting system and score each tool accordingly.


Configuration File
------------------------------------------------------------

The following table provides the name of the "manifest" file where you specify dependencies and/or the details of your package.


  Configuration          |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `filename`               |  component.json         |  component.json         |  package.json           |  package.json, volofile


Sample *[bower][bower]* enabled `component.json` file:

    {

      "name":     "myProject",
      "version":  "1.0.0",
      "main":     "./path/to/main.css",
      "dependencies": {
        "jquery": "~1.7.2"
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

      "volo": {
        "dependencies": {
          "jquery":     "github:jquery/jquery/1.8.1",
          "underscore": "github:amdjs/underscore/1.3.3",
          "backbone":   "github:documentcloud/backbone/0.9.2"
        }
      }

    }


**NOTES**:

-  N/A


Package Installation Location
------------------------------------------------------------

The following table details where each tool stores downloaded packages.

 
  Path                   |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
  `default path`           |  ./components           |  ./components           |  ./jam                  |  ./js, ./scripts, ./
  `custom path`            |  ✗                      |  --out dir              |  jam.packageDir         |  volo.{baseDir,baseUrl}, amd.baseDir


**NOTES**:

*[volo][volo]* has a fairly complex algorithm.

If not defined in `package.json` it:

-   Looks for a ./js directory
-   Looks for a ./scripts directory
-   Otherwise, the current working directory is used


Responsibilities
------------------------------------------------------------

The following table details the responsibilities the given tool takes on.


  Responsibilities       |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
 `package management`      |  ✓                      |  ✓                      |  ✓                      |  ✓                      
 `project scaffolding`     |  ✗                      |  ✗                      |  ✗                      |  ✓                     
 `build automation`        |  ✗                      |  ✗                      |  ✗                      |  ✓                      
 `script/module loading`   |  ✗                      |  ✗                      |  ✓                      |  ✓                      
 `compile/build`           |  ✗                      |  ✓                      |  ✗                      |  ✗                      


**NOTES**:

-  An interesting comparison of [volo and grunt](https://github.com/volojs/volo/wiki/volo-and-grunt).


Build/Compile
------------------------------------------------------------

The following table details which tools require a build/compile step during development.


  Build/Compile?         |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
 `?`                       |  ✗                      |  ✓ (component build)    |  ✗                      |  ✗                      


**NOTES**:

-  N/A


Central Registry
------------------------------------------------------------

The following table details which tools expose a central "registry".


  Registry?              |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
 `?`                       |  ✓                      |  ✗                      |  ✓                      |  ✗                      


**NOTES**:

-  The *[bower][bower]* "registry" is only a convenient [shorturl service](https://github.com/twitter/bower/issues/10#issuecomment-8547463).
-  It is good ettiquite is to use [user/package namespacing][packagist] when registering a package.


Package installation sources
------------------------------------------------------------

The following table details the method by which each tool is able to retrieve packages.


  Source                 |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
 `git / github`            |  ✓                      |  ✓                      |  ✓ (CLI ONLY)           |  ✓                      
 `private repositories`    |  ✓                      |  ✓                      |  ✗ (COMING SOON)        |  ✗ (COMING SOON)        
 `zip / tarball`           |  ✗                      |  ✗                      |  ✓ (CLI ONLY)           |  ✓ (ZIPBALL ONLY)       
 `registry`                |  ✓                      |  ✗                      |  ✗                      |  ✗                      


**NOTES**:

-  N/A


Supported JavaScript Module formats
------------------------------------------------------------

The following table details the JavaScript format each tool expects/handles.


  Format                 |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
 `Global Script`           |  ✓                      |  ✓                      |  ✓                      |  ✓                      
 `AMD`                     |  ✓ (format agnostic)    |  ✗                      |  ✓                      |  ✓                      
 `CommonJS/NodeJS`         |  ✓ (format agnostic)    |  ✓ (bundles require)    |  ✗                      |  ✗                      
 `CommonJS (WRAPPED)`      |  ✓ (format agnostic)    |  ✗                      |  ✓                      |  ✓                      


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


  Source                 |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
 `Bring your own loader`   |  ✓                      |  ✗                      |  ✗                      |  ✓                      
 `Includes a Loader`       |  ✗                      |  ✓ (custom require)     |  ✓ (RequireJS)          |  ✗                      


**NOTES**:

Loaders that you might be interested in:

-   [inject](https://github.com/linkedin/inject)
-   [curl](https://github.com/cujojs/curl)
-   [requirejs](http://requirejs.org)
-   [cajon](https://github.com/requirejs/cajon)
-   [almond](https://github.com/jrburke/almond)


Package Contents
------------------------------------------------------------

The following table details the the types of source files that can be contained in each package per tool.


  Source                 |  [bower][bower]                  |  [component][component]              |  [jam][jam]                    |  [volo][volo]
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
 `JavaScript`              |  ✓                      |  ✓                      |  ✓                      |  ✓                      
 `HTML`                    |  ✓                      |  ✓                      |  ✓                      |  ✗                      
 `CSS`                     |  ✓                      |  ✓                      |  ✓                      |  ✗                      


**NOTES**:

-  N/A


Final thoughts
------------------------------------------------------------

*[volo][volo]* is off to a great start; hopefully it sticks to package management as a single concern.

*[jam][jam]* currently has the most traction and a *very* [responsive and friendly author](https://twitter.com/caolan); however, *[bower][bower]* seems to have generated more buzz than all of them in just under a week. Of course, twitter and many [well-known developers](https://github.com/twitter/bower/graphs/contributors) being behind it certainly helped with that.

*[jam][jam]* could steal the show by doing the following:

-   Use *[bower][bower]* under the hood.
-   Make the loader optional and allow loader plug-ins (i.e. [requirejs][requirejs]).
-   Support zip/tarballs and ad-hoc git repositories via the manifest (but you get that for free by using *[bower][bower]*.

Library and component authors, may want to consider using deploying behind a [UMD][umdjs] wrapper and support the various package managers by authoring both {component,package}.json for front-end and npm (where appropriate).


Contributing
------------------------------------------------------------

I am sure I've made a few gramatical and spelling errors. I've probably even made comparison errors in a few spots. Please feel free to contribute to this. If you feel I should be rating on more categories or if you feel a score is incorrect or outdated, please speak up or submit a pull request.


Symbol Key
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
