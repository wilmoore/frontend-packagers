Front-End Package Manager Comparison
============================================================

The finalists:

-   [component][component]
-   [jam][jam]
-   [volo][volo]

Several categories with a maximum of (3) points per category per tool.


Configuration File
------------------------------------------------------------

File which details the packages/components your project depends on.


 component    0 |  jam       ✓✓✓ |  volo      ✓✓✓
:---------------|:---------------|:---------------
 component.json | package.json   | package.json + volofile


Both *[jam][jam]* and *[volo][volo]* support `package.json`, while
*[component][component]* supports a `component.json` file.

Below is a copy of a `jam` enabled `package.json` file:

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


Package target directory
------------------------------------------------------------

Where are downloaded packages placed?


 component    0 |  jam       ✓✓✓ |  volo        ✓ 
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


I don't love any of the default choices; although, both *[jam][jam]* and
*[volo][volo]* allow you to override this package directory via the
`package.json` file. *[jam][jam]* also allows you to create a user global
`$HOME/.jamrc`.

Again, with *[volo][volo]* I had to dig for this information. Even worse
is that *[volo][volo]* supports three different keys:

- `volo.baseDir`
- `volo.baseUrl`
- `amd.baseUrl`

If none of those are defined, it:

-   Looks for a js directory
-   Looks for a scripts directory
-   Otherwise, the current working directory is used

*[jam][jam]* is simple...it looks for a `jam.packageDir` property and if
not found, uses the `./jam` directory.

Unfortunately, *[component][component]* uses the directory `./components`
which isn't terrible, but there is no obvious way to override.


Single Purpose Tool
------------------------------------------------------------

I love single purpose tools. They are easy to debug when things go wrong
and they are generally easy to grok even without documentation.


 component  ✓✓✓ |  jam        ✓✓ |  volo        0
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


*[component][component]* wins this category hands down. It downloads or
builds packages...that's it.

*[jam][jam]* almost had this one. Unfortunately, *[jam][jam]* handles
configuration of *[requirejs][requirejs]* which seems nice at first;
however, this falls apart if you decide you want to use an alternative
loader. That being said, there is nothign stopping me from using *[jam][jam]*
as just a package manager and pulling in my own *[requirejs][requirejs]*.
and manually configuring it once.


*[volo][volo]* wants to be:

-   [package manager](https://github.com/volojs/volo/blob/master/commands/add/doc.md)
-   [project scaffolding](https://github.com/volojs/volo/blob/master/commands/create/doc.md)
-   [build/deployment tool](https://github.com/volojs/volo/wiki/Creating-a-volofile)

*[volo][volo]* is trying to do way too much.


Ease of development
------------------------------------------------------------

Each package manager provides a particular style of workflow. I am
looking for the most natural and friction-free flow possible. I don't
mind a build step; however, I don't think it should be required during
development.

 component    0 |  jam       ✓✓✓ |  volo      ✓✓✓
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


-   *[component][component]* was rated low here because you are required
    to run `component build` after each change. This is easily remedied
    with a file watcher or even `watch(1)`, but I'm still not fond of it
    being a requirement.
-   Neither *[jam][jam]* nor *[volo][volo]* require a build step to
    realize code changes.


Registry free
------------------------------------------------------------

I can't realistically score this category as I'm torn on the issue.

No score.


 component    0 |  jam         0 |  volo        0
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


Sources: git, github
------------------------------------------------------------

All of the package managers support git/github repositories as sources;
however, *[jam][jam]* is the only one that doesn't currently seem to
support git/github via the manifest (`package.json`) file.


 component  ✓✓✓ |  jam         ✓ |  volo      ✓✓✓
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


Sources: zipball/tarball
------------------------------------------------------------

This is not supported via *[component][component]* as everything must be
a github repository. *[jam][jam]* seems to only support registered
packages, which leaves only *[volo][volo]* supporting zipballs and
tarballs.


 component    0 |  jam         ✓ |  volo      ✓✓✓
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


Wraps non-amd code on the fly
------------------------------------------------------------

 component    0 |  jam         0 |  volo      ✓✓✓
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


Loader agnostic
------------------------------------------------------------

*[volo][volo]* seems to the the only loader agnostic package manager of
the three. *[component][component]* ships with it's own `require`
function and `build` command and *[jam][jam]* ships a custom version of
[requirejs][requirejs].


 component    0 |  jam         0 |  volo      ✓✓✓
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


Packages include JavaScript, CSS, HTML
------------------------------------------------------------

*[component][component]* seems to be the only of the bunch that makes
CSS and HTML a prioroty along with JavaScript.


 component  ✓✓✓ |  jam         0 |  volo        0
:---------------|:---------------|:---------------
 ./components   | ./jam          | ./       


Summary
------------------------------------------------------------

-   (19) [Volo][volo] ✓
-   (12) [Jam][jam]
-   (09) [Component][component]


Other tools you might consider
------------------------------------------------------------

-   [Tiki](http://sirtiki.com)


Contributing
------------------------------------------------------------

Please feel free to contribute to this. If you feel I should be rating
on more categories or if you feel a score is incorrect or outdated,
please speak up.







[component]: https://github.com/component/component
[jam]:       http://jamjs.org
[volo]:      http://volojs.org
[requirejs]: http://requirejs.org/
