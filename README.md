Tappable
========

Tappable is a simple, standalone library to invoke the **tap** event for touch-friendly web browsers. Currently it's only tested on iOS Mobile Safari as I don't have any other smartphones to test with. The codebase is heavily inspired by Matteo Spinelli's [Remove onClick delay on webkit for iPhone](http://cubiq.org/remove-onclick-delay-on-webkit-for-iphone) and Ryan Fioravanti's [Creating Fast Buttons for Mobile Web Applications](http://code.google.com/mobile/articles/fast_buttons.html).

Here's how you implement the code:

	tappable('elementID', function(){
		alert('tap');
	});

Simple.

Why 'tap'?
----------

First, it would be wise to read the articles linked above to understand the purpose  of this script. But if you're lazy, take a look at this diagram:

![Diagram 1](https://github.com/cheeaun/tappable/raw/master/diagrams/diagram-1.png)

So, that's the **tap** event. But wait the minute, I can just use the `touchend` event to *simulate* a tap, right? Wrong, because:

![Diagram 2](https://github.com/cheeaun/tappable/raw/master/diagrams/diagram-2.png)

This means that once the finger moves, it will not fire the tap event. However, Tappable works in two special cases. First is the *normal* case:

![Diagram 3](https://github.com/cheeaun/tappable/raw/master/diagrams/diagram-3.png)

The second case is the `noScroll` mode, where moving your finger on the element will no make the page scroll. This is useful for mobile web apps which might implement their own *fixed* headers or sections on the page.

![Diagram 4](https://github.com/cheeaun/tappable/raw/master/diagrams/diagram-4.png)

Documentation
-------------

###Syntax

	tappable(el, opts);

### Arguments

1. `el` - The element to be tapped.
	* (*element*) The DOM element.
	* (*string*) A string containing the id of the DOM element.
2. `opts` - The options object or a function.
	* (*object*) The options to be passed.
	* (*function*) The function to execute when tapped.

### Options

* noScroll - (*boolean*: defaults to `false`) Whether or not to scroll when *moving* on the element.
* activeClass - (*string*: defaults to `tappable-active`) A string indicating the *active* class applied to the element.
* onTap - (*function*) The function to execute when tapped.
* onStart - (*function*) The function to execute when `touchstart` event is fired.
* onMove - (*function*) The function to execute when `touchmove` event is fired.
* onMoveOut - (*function*) The function to execute when touch moves *out* of the element, if `noScroll` is `true`.
* onMoveIn - (*function*) The function to execute when touch moves back in the element, if `noScroll` is `true`.
* onEnd - (*function*) The function to execute when `touchend` event is fired.
* onCancel - (*function*) The function to execute when `touchcancel` event is fired, **or** when touch *moves* if `noScroll` is `false`.

Contributing
------------

Feel free to fork this project! Help and feedback would be appreciated, especially if this could be tested on Android, WebOS or any other touch-friendly browsers, not just mobile ones.

License
-------

Tappable is licensed under the MIT license.