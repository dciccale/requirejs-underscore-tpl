# underscore-tpl

> underscore-tpl is a [RequireJS](http://requirejs.org) plugin to load and precompile [Underscore.js](http://underscorejs.org) templates.

Here are some [performance tests](http://jsperf.com/underscore-templates-precompiled-performance) that show the
difference when rendering precompiled templates.

## Usage

Use the `tpl!` prefix when loading a template.

`myview.js`

```javascript
define(['tpl!mytemplate.tpl'], function (template) {

  var MyView = Backbone.View.extend({
    template: template // just pass in the template
  });                  // do not use _.template(), at this point it is already compiled

  return MyView;
});
```

The plugin will compile the template after requirejs `r.js` optimizer.

And also when developing, it will compile the template the first time is loaded so that the next
time is required it will just render the template saving a function call to underscore's internal render method.

## Configuration

You can pass underscoreTemplateSettings to RequireJS config

```javascript
requirejs.config({
  config: {
    underscoreTemplateSettings: {
      interpolate: /\{\{\s*([^#\{]+?)\s*\}\}/g,  // {{ title }}
      evaluate:    /\{\{#([\s\S]+?)\}\}/g,       // {{# console.log("stuff") }}
      escape:      /\{\{\{([\s\S]+?)\}\}\}/g     // {{{ title }}}
    }
  });
```

## Dependecies

For this plugin to work you need:
- [Underscore.js](http://underscorejs.org)
- [RequireJS text plugin](https://github.com/requirejs/text)

## License
See [LICENSE](https://raw.github.com/dciccale/requirejs-underscore-tpl/master/LICENSE-MIT)
