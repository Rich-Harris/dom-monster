# dom-monster

The dbmonster benchmark has been [widely used](https://github.com/Rich-Harris/ractive-dbmonster) to compare various front-end frameworks and libraries. Andrew Giammarchi aka [@WebReflection](https://twitter.com/webreflection) argues, in [this post](http://webreflection.blogspot.com/2015/04/the-dom-is-not-slow-your-abstraction-is.html), that those tools are often unnecessary and often cause performance problems.

Personally, I wouldn't want to build an app without a suitable abstraction (*cough* [Ractive](http://ractivejs.org) *cough*), because your code becomes hellaciously complex surprisingly quickly if you try to rely on vanilla DOM. But Andrea makes a reasonable point that a vanilla DOM implementation serves as a useful benchmark against which to evaluate frameworks.

His [vanilla DOM implementation](http://webreflection.github.io/dbmonster/) is actually *slower* than the [Ractive implementation](http://www.rich-harris.co.uk/ractive-dbmonster/), at least on Chrome on the machine I'm writing this on. That's because Ractive implements various optimisations that no sane developer would bother with themselves. (Yep, abstractions *can* be faster than the thing they're abstracting, when the underlying primitives are sufficiently complex that we don't use them correctly.)

But what would the fastest possible vanilla DOM implementation look like?


## Something like [this](http://www.rich-harris.co.uk/dom-monster), presumably

dom-monster is a fork of the Ractive implementation, without Ractive. It's *really bad code*, with lots of hardcoded assumptions (e.g. about the number of rows staying constant), and anyone who produced code like this would receive some stern words if they were working on the same team as me. But because the code doesn't make any attempt to be non-brittle, it's pretty fast.

This is the standard that those of us authoring tools should be aiming for. (I have to hand it to [paperclip](http://paperclipjs.com/), which is [within spitting distance](http://paperclip-dbmonster.herokuapp.com/) of dom-monster.) Besides raw update performance, we should be aiming for the same degree of compatibility, initialisation speed, and memory footprint.

Theoretically, that's pretty much impossible, but it's still a useful target.

(Incidentally, Ractive is undergoing some changes for the upcoming 0.8 version that improve its update performance significantly - even beyond its current React/Underscore/Ember-beating performance. Yay!)


## I bet I can make dom-monster faster

Please send me a PR!


## License

MIT.