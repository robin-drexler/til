---
layout: post
title:  "The DOM event dispatch phases"
date:   2014-08-28 21:00:00
---

Browsing [MDN](https://developer.mozilla.org/en/docs/Web/API/EventTarget.addEventListener), I stumbled upon the fact that ```target.addEventListener``` actually has a third parameter, called ```useCapture```.
{% highlight javascript %}
target.addEventListener(type, listener[, useCapture]); 
{% endhighlight %}

Turns out, it's to control when a event listener gets called during an event dispatch.

When an event is dispatched on a DOM element, [there are actually three phases](http://www.w3.org/TR/DOM-Level-3-Events/#event-flow). During the first, the capture phase, all listeners (that make use of the useCapture flag) bound to ancestors of the event target are getting called.

Secondly the event listeners bound to the target it self are being invoked. (Target phase)

Last but not least, the event bubbles up through all ancesors and all listeners (that do not(!) make use of the useCapture flag) are getting called. (Bubble phase)

An event listener can either be registered for the capture or bubble phase, but not both. However the same function can be registered for both phases separately.

## Example code


{% highlight javascript %}
function listen(){};

// register for capture phase
// 3rd param useCapture is set to true
someDomElement.addEventListener('click', listen, true);

// register for bubble phase
// 3rd param useCapture is set to false (default)
someDomElement.addEventListener('click', listen, false);


{% endhighlight %}

## Scribble
![Scribble demoing event phases]({{site.baseurl}}/assets/images/posts/scribble_event_phases.jpg)
 