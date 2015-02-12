This repo is a fork of [InstantClick](http://instantclick.io/) v3.1.0, by Alexandre Dieulot.

## Modifications

The official version of InstantClick replaces the entire document body, via `document.documentElement.replaceChild(<new body>, document.body)`.

This version allows you to specify a custom callback so you can do something like replace only a certain div and apply a fade transition.

Here is an example usage from [my personal site](http://www.joestrommen.com) that does exactly that:

    InstantClick.init(function (newBody) {
        // Keep everything other than body-content intact
        var newBodyContent = newBody.querySelectorAll('.body-content')[0];
  
        if (newBodyContent) {
            var oldBodyContent = document.querySelectorAll('.body-content')[0];
            var parent = oldBodyContent.parentElement;
  
            parent.replaceChild(newBodyContent, oldBodyContent);
  
            var opacity = window.getComputedStyle(newBody).opacity; // Force a re-calc
            DomUtil.removeClass(newBodyContent, 'fade-in');
        } else {
            // No .body-content - perhaps it was an error page?  Show the entire thing.
            document.documentElement.replaceChild(newBody, document.body)
        }
    });
