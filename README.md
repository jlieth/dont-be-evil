# dont-be-evil

Browser extension that prevents Google search from tracking clicks

## How Google tracks your search

Every external link on the search results page has a `mousedown` event callback.
The callback rewrites the `href` attribute to a Google-internal link.
A click on an external link is thus instead redirected through Google without
the user's knowledge.

Other privacy-related extensions might already mitigate this problem. I haven't
done extensive testing, but it seems that ublock origin already fixes
this behaviour.

To see if you are still affected, just search anything on Google
and right-click on one of the results. If the url of the link changes to a
Google-internal link, you can be tracked.

## How this extension works

The extension adds an event listener for mouse events (and some others) that
stops the propagation of the event. The Google code that rewrites the
`href` attribute is never called and the original `href` attribute is preserved.
Clicking on a link therefore brings up the result directly without going through
Google.

## Supported Google domains

See the [list of configured domain matches](https://github.com/jlieth/dont-be-evil/blob/main/dont-be-evil/manifest.json#L21) of this extension.
The list of domains is taken from https://www.google.com/supported_domains.
If you find another Google search domain, please let me know.

## Credit

[This gist](https://gist.github.com/radiantly/e1c7319214c77fa007f323fc56cd0239)
gave me the idea of stopping propagation of events to solve this problem.
