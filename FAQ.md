Can't find the answer you need? Send it to wordcram-at-gmail, or ask [@wordcram on twitter](http://twitter.com/wordcram).



# What can it do? #

## Are words "clickable"? ##

Yes. Save a reference to your wordcram, and in your `mouseClicked` events, ask the wordcram whether there's a word at the mouse-click's coordinates. Something like this:
```
WordCram wordCram;

void setup() {
  wordCram = new WordCram(this)...
  wordCram.drawAll();
}

void mouseClicked() {
  Word word = wordCram.getWordAt(mouseX, mouseY);
  if (word != null) {
    ...
  }
}
```

For a complete running sketch like this, check out Sketchbook > libraries > WordCram > tutorials > L\_clickableWords.

## Can I write to PDF? ##

Yes! It's in the [2011-04-27 daily build](http://code.google.com/p/wordcram/downloads/detail?name=wordcram.20110427.zip&can=2&q=), and will be in the 0.5 release.

## Does this work with Processing.js? ##

No, but I'm looking into it. It depends on whether javascript can "sense" the shape of the words to detect collisions. But it would be really cool to see word clouds in the browser.

# Something's not working right... #

## Why do my words come out fuzzy? ##

If you're loading your fonts with [loadFont](http://processing.org/reference/loadFont_.html), try using [createFont](http://processing.org/reference/createFont_.html) instead.  `loadFont` doesn't work as well for rendering characters at different sizes.

## Why don't any of my words show up? ##

Are you using something like `Colorers.pickFrom(0)` or `Colorers.pickFrom(255)`?  Try using `Colorers.pickFrom(color(0))` and `Colorers.pickFrom(color(255))` instead.

Processing internally stores colors as integers, with the alpha in the highest bits, so it sees the integer 0 as colorless and completely transparent.  A WordCram created with `Colorers.pickFrom(0)` will render the words, they'll just be invisible.

`Colorers.pickFrom()` takes a _bunch_ of colors, so it treats each integer it gets as a Processing color/integer.  This is really a misleading API, and it should be sorted out.