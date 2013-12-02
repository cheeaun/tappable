Tappable
========

Tappable is a simple, standalone library to invoke the **tap** event for touch-friendly web browsers. Currently it's only tested on iOS Mobile Safari as I don't have any other smartphones to test with. The codebase is heavily inspired by Matteo Spinelli's [Remove onClick delay on webkit for iPhone](http://cubiq.org/remove-onclick-delay-on-webkit-for-iphone) and Ryan Fioravanti's [Creating Fast Buttons for Mobile Web Applications](http://code.google.com/mobile/articles/fast_buttons.html).

Here's how you implement the code:

	tappable('#selector', function(){
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

When the page scrolls, the button is not tapped.

The second case is the `noScroll` mode, where moving your finger on the element will not make the page scroll. This is useful for mobile web apps which might implement their own *fixed* headers or sections on the page.

![Diagram 4](https://github.com/cheeaun/tappable/raw/master/diagrams/diagram-4.png)

The button is tapped when the finger is on top of the button, even after moving in and out.

Documentation
-------------

###Syntax

	tappable(selector, opts);

### Arguments

1. `selector` - (*string*) The CSS selector expression of element to be tapped.
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
* allowClick - (*boolean*: defaults to `false`) Whether or not to `preventDefault` the click on the element.
* boundMargin - (*integer*: defaults to 50) A number indicating the bounding area of tapped region (of the element).
* noScrollDelay - (*integer*: defaults to 0) A number indicating the delay in ms before 'noScroll' option kicks in.
* activeClassDelay - (*integer*: defaults to 0) A number indicating the delay in ms before the *active* class is applied.
* inactiveClassDelay - (*integer*: defaults to 0) A number indicating the delay in ms before the *active* class is removed.

### Instance Object

* el - (*object*) A reference to the bound DOM element.
* destroy - (*function*) Removes event listeners from the bound DOM element.

Demo
----

Load <http://fiddle.jshell.net/cheeaun/jxwsy/show/light/> in your browser. Edit here <http://jsfiddle.net/cheeaun/jxwsy/>. Or scan this QR code:

![http://fiddle.jshell.net/cheeaun/jxwsy/show/light/](http://goo.gl/wFhSC.qr)

Event Delegation (for tagged version 0.1)
----------------------------------------

**Note: This is no longer needed. The latest code now does event delegation by default**.

Here's a simple example:

	tappable(document.body || document.getElementsByTagName('body')[0], {
		onTap: function(e, target){
			// e.target works too
			if (target.tagName.toLowerCase() == 'a'){
				alert('tap');
			}
		}
	});

For (almost) every callback function, a second argument which is the target element node, is passed. As a bonus, the event object also have an additional `target` attribute which is the target node (can be any node type, not just element node).

Contributing
------------

Feel free to fork this project! Help and feedback would be appreciated, especially if this could be tested on Android, WebOS or any other touch-friendly browsers, not just mobile ones.

License
-------

Tappable is licensed under the [MIT license](http://cheeaun.mit-license.org/).
