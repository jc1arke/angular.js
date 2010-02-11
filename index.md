---
title: Home
layout: default
open: '{{'
close: '}}'
---

# <tt>&lt;angular.js/&gt;</tt>

> Web apps made simple.

## What is <tt>&lt;angular.js/&gt;</tt>?

The <tt>&lt;angular.js/&gt;</tt> library teaches your old browser new tricks. It is what HTML would have been, 
if it was designed for building web applications.

Add <tt>&lt;angular.js/&gt;</tt> to any static web page and extend the HTML vocabulary of your browser to 
understand:
* [ng-attributes] such as <tt>&lt;div ng-repeat="item in items"/&gt;</tt> which control the rendering process.
* Inline {{page.open}}[mustache]{{page.close}} which binds expression in spreadsheet-like auto-update manner.
* [filters], [formatters], [validators], [widgets], [charts], and [more]


## Demos
### Calculator

In it's simplest form <tt>&lt;angular.js/&gt;</tt> is a client-side auto-evaluating templating system.
Try changing the numbers, enter negatives, or non-number text, to see what happens. Then see 
what the page looks like without <tt>&lt;angular.js/&gt;</tt> and view the source behind it, by clicking
on the appropriate tab.

{% include calculator.html %}

### Invoice

Here is a more complex example of an invoice, showing spreadsheet-like characteristics of auto-updating,
[validation][validators], [repeater][ng-repeat], and [charts]. Pay special attention to adding and removing
new items, and column summations of totals. At the bottom we have dumped the current model of the invoice in JSON format 
for you to examine. This whole demo is 100% in declarative HTML, no JavaScript was
written to achieve this interactive UI, and there is no server in the background.

{% include spreadsheet.html %}

### Programmatic Control & Model - View - Controller

Here we show you how seamless it is to bridge <tt>&lt;angular.js/&gt;</tt> (which acts as view) and 
JavaScript (which acts as controller). On <tt>init</tt> we copy the controller methods into 
<tt>&lt;angular.js/&gt;</tt> scope, which makes them freely available to be called from the view. 
When the method is invoked it has easy access to the model through "this".

<div class="angular">
  <script>
    function NamesController() {};
    NamesController.prototype = {
      greet: function(name) {
        alert("Hello " + name);
      },
      addName: function(){
        this.names.push(this.newName);
        this.newName = "";
      }
    };
    function initDemo() {
      scope.set("names", ["Adam", "Misko", "John", "Mary"]);
      $.each(NamesController.prototype, function(name, fn) {
        scope.set(name, fn);
      });
    };
  </script>
  Filter: <input name="filterText"/>
  <ul ng-init="$window.initDemo()">
    <li ng-repeat="name in names.$filter(filterText)">
      <a href="" ng-action="greet(name)">{{ page.open }}name{{ page.close }}</a>
    </li>
  </ul>
  Name: 
    <input name="newName"/> 
    <input type="button" value="Add" ng-action="addName()"/>  
</div>

If you have JavaScript debugger running (FireBug, Safari or Chrome) than you can open console and 
try these commands directly from your browser. Watch what happens to the view after each updateView() 
command.

    scope.get('names'); 
    scope.get('names').push('my name');
    scope.updateView();
    
    scope.set('filterText', 'a');
    scope.updateView();


### Database

What good is easy way of building UI, without persistence? therefore <tt>&lt;angular.js/&gt;</tt>
also includes a service ([http://www.getangular.com](http://www.getangular.com)) where you can 
host your data for free. It is a cross-site RESTful JSON store and authentication service. 
Here's an [task application](/database.html) as a demo and a video explaining how it was built.

<div id="demo">
</div>
<script type='text/javascript'>
swfobject.embedSWF(
  "http://www.getangular.com/video/Tasks.swf", "demo", 
  "640", "511", "9.0.0","expressInstall.swf", {}, {
    quality: "high",
    name: "Captivate",
    id: "Captivate",
    wmode: "window",
    bgcolor: "#F1F4F5",
    menu: "false"
  }, {});
</script>


## Slides

<iframe src="http://docs.google.com/present/embed?id=d449gch_237xq95nwdq" frameborder="0" width="410" height="342"></iframe>

[ng-attributes]: http://docs.getangular.com/Main_Page#Attribute_Reference
[ng-repeat]: http://docs.getangular.com/Ng-repeat
[mustache]: http://docs.getangular.com/Ng-bind
[formatters]: http://docs.getangular.com/Formatters
[filters]: http://docs.getangular.com/Filter
[validators]: http://docs.getangular.com/Validator
[widgets]: http://docs.getangular.com/Widget
[charts]: http://docs.getangular.com/Chart
[more]: http://www.getangular.com/screencast