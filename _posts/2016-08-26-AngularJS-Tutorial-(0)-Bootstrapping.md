---
layout: post
title:  "AngularJS Tutorial (0) - Bootstrapping"
categories: AngularJS
---

{{ page.title }}
======

In this step of the tutorial, you will become familiar with the most important source code files of the AngularJS Phonecat App. You will also learn how to start the development servers bundled with angular-seed, and run the application in the browser.

Before you continue, make sure you have set up your development environment and installed all necessary dependencies, as described in the Environment Setup section.

In the angular-phonecat directory, run this command:


{% highlight JavaScript %}
git checkout -f step-0
{% endhighlight %}

This resets your workspace to step 0 of the tutorial app.

You must repeat this for every future step in the tutorial and change the number to the number of the step you are on. This will cause any changes you made within your working directory to be lost.

If you haven't already done so, you need to install the dependencies by running:

{% highlight JavaScript %}
npm install
{% endhighlight %}

To see the app running in a browser, open a separate terminal/command line tab or window, then run npm start to start the web server. Now, open a browser window for the app and navigate to http://localhost:8000/index.html.

Note that if you already ran the master branch app prior to checking out step-0, you may see the cached master version of the app in your browser window at this point. Just hit refresh to re-load the page.

You can now see the page in your browser. It's not very exciting, but that's OK.

The HTML page that displays "Nothing here yet!" was constructed with the HTML code shown below. The code contains some key Angular elements that we will need as we progress.

`app/index.html:`
{% highlight JavaScript%}
<!doctype html>
<html lang="en" ng-app>
  <head>
    <meta charset="utf-8">
    <title>My HTML File</title>
    <link rel="stylesheet" href="bower_components/bootstrap/dist/css/bootstrap.css" />
    <script src="bower_components/angular/angular.js"></script>
  </head>
  <body>
    <p>Nothing here {{'yet' + '!'}}</p>
  </body>
</html>
{% endhighlight%}


What is the code doing?
===

ng-app **attribute**:

{% highlight JavaScript%}
<html ng-app>
{% endhighlight %}

The ng-app attribute represents an Angular directive, named ngApp (Angular uses kebab-case for its custom attributes and camelCasefor the corresponding directives which implement them). This directive is used to flag the HTML element that Angular should consider to be the root element of our application. This gives application developers the freedom to tell Angular if the entire HTML page or only a portion of it should be treated as the AngularJS application.

For more info on ngApp, check out the API Reference.


angular.js **script tag**:

{% highlight JavaScript%}
<script src="bower_components/angular/angular.js"></script>
{% endhighlight %}

This code downloads the angular.js script which registers a callback that will be executed by the browser when the containing HTML page is fully downloaded. When the callback is executed, Angular looks for the ngApp directive. If Angular finds the directive, it will bootstrap the application with the root of the application DOM being the element on which the ngApp directive was defined.

For more info on bootstrapping your app, checkout the Bootstrap section of the Developer Guide.

**Double-curly binding with an expression:**

{% highlight JavaScript%}
{% raw %}
Nothing here {{'yet' + '!'}}
{% endraw %}
{% endhighlight %}

This line demonstrates two core features of Angular's templating capabilities:

* A binding, denoted by double-curlies: `{% raw %}{{ }}{% endraw %}`
* A simple expression used in this binding: `'yet' + '!'`

The binding tells Angular that it should evaluate an expression and insert the result into the DOM in place of the binding. As we will see in the next steps, rather than a one-time insert, a binding will result in efficient continuous updates whenever the result of the expression evaluation changes.

Angular expressions are JavaScript-like code snippets that are evaluated by Angular in the context of the current model scope, rather than within the scope of the global context (window).

As expected, once this template is processed by Angular, the HTML page contains the text:

{% highlight JavaScript %}
Nothing here yet!
{% endhighlight %}

Bootstrapping Angular Applications
===
Bootstrapping Angular applications automatically using the ngApp directive is very easy and suitable for most cases. In advanced cases, such as when using script loaders, you can use the imperative/manual way to bootstrap the application.

There are 3 important things that happen during the bootstrap phase:


1. The injector that will be used for dependency injection is created.

2. The injector will then create the root scope that will become the context for the model of our application.

3. Angular will then "compile" the DOM starting at the ngApp root element, processing any directives and bindings found along the way.

Once an application is bootstrapped, it will then wait for incoming browser events (such as mouse clicks, key presses or incoming HTTP responses) that might change the model. Once such an event occurs, Angular detects if it caused any model changes and if changes are found, Angular will reflect them in the view by updating all of the affected bindings.

The structure of our application is currently very simple. The template contains just one directive and one static binding, and our model is empty. That will soon change!

![Template&Model]({{ site.url }}/assets/angular/tutorial/00/tutorial_00.png)


What are all these files in my working directory?
===
Most of the files in your working directory come from the angular-seed project, which is typically used to bootstrap new AngularJS projects. The seed project is pre-configured to install the AngularJS framework (via bower into the app/bower_components/ directory) and tools for developing and testing a typical web application (via npm).

For the purposes of this tutorial, we modified the angular-seed with the following changes:

* Removed the example app.
* Removed unused dependencies.
* Added phone images to app/img/phones/.
* Added phone data files (JSON) to app/phones/.
* Added a dependency on Bootstrap in the bower.json file.