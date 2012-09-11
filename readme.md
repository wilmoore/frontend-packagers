Front-End Package Manager Comparison
============================================================


Why do this?
------------------------------------------------------------

It is about time we have a decent package manager for the browser.  Front-end development is serious stuff and there is no good reason for us to continue with sub-par tools or no tools at all.

These problems have been solved on the server but we need the same for the browser.


The contenders
------------------------------------------------------------

First of all, there are other players in the game; however, these are the three that have the most potential and solve the problems that I believe need solving. Perhaps you see it differently...this is my opinion.

-   [component][component]
-   [jam][jam]
-   [volo][volo]

To be completely fair, *[component][component]* attempts to solve a similar, but slightly different set of problems. The confusing bit is that many of [components][component] concerns overlap with the tools that set out to be just package managers.

Finally, I really appreciate the effort that has gone into all of these.  It is a task that no many are willing to take on so I want to thank all of the authors for putting in the time and energy.


What is a package manager?
------------------------------------------------------------

A package manager is a tool that allows you to specify a list of
depeendencies for your library or application.

For example, I may be writing a library that handles HTML5Video. The
library likely needs to infer the mime type; thus, I'd list something
like [component/mime](http://github.com/component/mime) as a dependency.

You might be thinking that we should also include a unit testing
framework. Maybe, or maybe not. Something similar like node-tap should
work; however, a simple script using `assert` may be a fine idea as
well.

Another example might be that you are writing an application (a todo
list app perhaps). The most obvious dependencies for such an app might
be (assumes you won't use a monolithic MV* framework):

-   Event manager (e.g. Event Emitter)
-   Object attribute manager
-   Router
-   Unit Test Framework (e.g. Mocha)

The idea here is that the application developer should worry about just
this pieces of the application that are unique to the application. The
reusable parts should be dependencies.

The *[component][component]* tool stands out as more of a framework that
has just enough convention to allow you to start building up modular
components for your application.

To be fair *[component][component]* doesn't try to compete with the pure
package managers. It wants to manage all of your application's components
and/or widgets. For example, you may have built a color picker component.
The color picker component is an aggregation of HTML, CSS, JavaScript,
and maybe even icons and fonts.  *[component][component]* wants to
concatenate and load those for you.

On the other hand, *[jam][jam]* and *[volo][volo]* are only package managers
in the realm of say [Bundler](http://gembundler.com/), [NPM](https://npmjs.org/),
or [Composer](http://getcomposer.org/).

If you want to read more on this distinction, check out the [issue #1 thread](https://github.com/wilmoore/frontend-packagers/issues/1).


How is this thing scored?
------------------------------------------------------------

Several categories with a maximum of (3) points per category per tool.

A tool can score 0 for a category. That doesn't necessarily mean it is a
true fail; however, it means that it doesn't meet my personal criteria
for the category.


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


Package installation directory
------------------------------------------------------------

Where are downloaded packages placed?

 
  `path`                 |  bower                  |  component  ✓✓✓         |  jam                ✓✓✓ |  volo               ✓✓✓ 
:------------------------|:------------------------|:------------------------|:------------------------|:------------------------
 default path            | -                       | ./components            | ./jam                   | ./
 custom path             | -                       | install --out dir       | `jam.packageDir`        | `volo.{baseDir,baseUrl}`
                         |                         |                         |                         | `amd.baseUrl`


I don't hate any of the defaults. If you use NodeJS/NPM, you've likely gotten used to the `./node_modules` directory.
Sure, it's ugly, but it works and [it ain't](https://twitter.com/dshaw/status/244118074264010752) [changing](https://github.com/joyent/node/issues/3694#issuecomment-6937179).

That being said, each tool allows you to change the package installation directory. Choice allows you to use the tool with workflows that were not
immediately obvious to the tool author.

*[volo][volo]* has a pretty complex algorithm which says:

If not defined in the `package.json` file, it:

-   Looks for a js directory
-   Looks for a scripts directory
-   Otherwise, the current working directory is used


Single Purpose Tool
------------------------------------------------------------

I love single purpose tools. They are easy to debug when things go wrong
and they are generally easy to grok even without documentation.


  `concerns`                 |  component              ✓✓✓ |  jam                     ✓✓ |  volo                    ✓✓
:----------------------------|:----------------------------|:----------------------------|:----------------------------
                             | package management          | package management          | [package management](https://github.com/volojs/volo/blob/master/commands/add/doc.md)
                             | compile                     | requirejs config            | [project scaffolding](https://github.com/volojs/volo/blob/master/commands/create/doc.md)
                             |                             |                             | [build tool](https://github.com/volojs/volo/wiki/Creating-a-volofile)


It seems that all of the tools take on a bit of extra responsibility; however, it is *[volo][volo]* that goes a bit overboard with build/task management. I was originally against the project scaffolding (`volo create`); however, I am now warm on the idea of having a bit of sugar for pulling down project templates. I am still not comfortable with one tool also handling build concerns. If you are interested, an interesting comparison of [volo and grunt](https://github.com/volojs/volo/wiki/volo-and-grunt) is available.

*[jam][jam]* want to handle configuration of *[requirejs][requirejs]* which seems nice at first; however, some developers will want alternative loaders and forcing *[requirejs][requirejs]* can be a turn-off. That being said, at this point, *[requirejs][requirejs]* is my choice; however, I know it won't be everyones choice. I also don't like that *[jam][jam]* delivers a custom *[requirejs][requirejs]*. This is a leaky abstraction just waiting to happen. 

Like I mentioned earlier, *[component][component]* is a little bit different; however, it does a good job of sticking to a conceptual theme and delivering in that problem space.


Ease of development
------------------------------------------------------------

Each package manager provides a particular style of workflow. I am looking for the most natural and friction-free flow possible. I don't mind a build step; however, I don't want to have to complile everything for every little change.

The following table lists the command you need to run after every code change.


 component      0 |  jam       ✓✓✓ |  volo      ✓✓✓
:-----------------|:---------------|:---------------
 component build  |                | 


-   *[component][component]* was rated low here because you are required
    to run `component build` after each change. This is easily remedied
    with a file watcher or even `watch(1)`, but I'm still not fond of it
    being a requirement.
-   *[jam][jam]* / *[volo][volo]* do not require a build step to realize code changes.


Registry free
------------------------------------------------------------

There are several arguments for and against having a central registry.
What it really boils down to is the potential for naming conflicts at
scale.

This is a real issue with NPM today; however, that doesn't mean it can't
be [done well][packagist].


 component    0 |  jam         0 |  volo        0
:---------------|:---------------|:---------------

If we are going to have a registry, I think it should:

-   Enforce [user/package namespacing][packagist] at a minimum.
-   If it is a bottleneck, it is useless, so make it fast and always
    available.
-   The registry shouldn't be the only way to obtain dependencies. In
    most cases, I'd prefer to retrieve directly from git/github.

Currently, *[jam][jam]* is the only one with a registry; however, it
currently suffers the same [issues as NPM](https://github.com/wilmoore/frontend-packagers/issues/1#issuecomment-8338583).


Package installation sources
------------------------------------------------------------

All of the package managers support git/github repositories as sources;
however, *[jam][jam]* is the only one that doesn't currently seem to
support git/github via the manifest (`package.json`) file.


  `source`     |  component ✓✓ |  jam        ✓ |  volo     ✓✓
:--------------|:-------------:|:-------------:|:-------------:
 git/github    | yes           | cli only      | yes
 private repos | yes           | coming soon   | coming soon
 zip/tarball   | no            | cli only      | zipball only
 registry      | no            | yes           | no


Module formats
------------------------------------------------------------


  `format`          |  component   ✓ |  jam         ✓ |  volo      ✓✓
:-------------------|:--------------:|:--------------:|:--------------:
 Node/CJS           |  yes (no wrap) |  yes (wrapped) |  yes (wrapped)
 AMD                |  no            |  yes           |  yes         
 Auto-Wrap Globals  |  no            |  no            |  yes         



Loader agnostic
------------------------------------------------------------

*[volo][volo]* seems to be the the only loader agnostic package manager of
the bunch. *[component][component]* ships with it's own `require` function
and `build` command while *[jam][jam]* ships a custom version of
[requirejs][requirejs].


  component   0 |  jam         0 |  volo      ✓✓✓
:---------------|:---------------|:---------------
  no            |  no            |  yes


Packages include JavaScript, CSS, HTML
------------------------------------------------------------

*[component][component]* seems to be the only of the bunch that makes
CSS and HTML a prioroty along with JavaScript.


  component ✓✓✓ |  jam         0 |  volo        0
:---------------|:---------------|:---------------
  yes           |  no            |  no      


Summary
------------------------------------------------------------

-   (18) [Volo][volo] ✓
-   (13) [Jam][jam]
-   (12) [Component][component]


Final thoughts
------------------------------------------------------------

This comparision is very subjective. My personal tastes are just
that...my personal tastes. I've spent a single day working with all
three tools and I come away with feeling like I could totally use either
*[jam][jam]* or *[volo][volo]* on a real project today.

I think *[jam][jam]* has superior documentation and a little bit more
traction; however, I feel like *[volo][volo]* is off to a great start
and has the most potential (especially if it sticks to package
management as a single concern).

That being said, *[jam][jam]* could steal the show by doing the
following:

-   Make [requirejs][requirejs] optional (although this is what I will
    be using).
-   Support more than just JavaScript.
-   Support zip/tarballs and ad-hoc git repositories.


Other tools you might consider
------------------------------------------------------------

Package Managers

-   [Tiki](http://sirtiki.com)

Loaders

-   [inject](https://github.com/linkedin/inject)
-   [curl](https://github.com/cujojs/curl)
-   [requirejs](http://requirejs.org)
-   [cajon](https://github.com/requirejs/cajon)
-   [almond](https://github.com/jrburke/almond)


Contributing
------------------------------------------------------------

I am sure I've made a few gramatical and spelling errors. I've probably
even made comparison errors in a few spots.

Please feel free to contribute to this. If you feel I should be rating
on more categories or if you feel a score is incorrect or outdated,
please speak up or submit a pull request.





[component]: https://github.com/component/component
[jam]:       http://jamjs.org
[volo]:      http://volojs.org
[requirejs]: http://requirejs.org/
[packagist]: http://packagist.org/about
