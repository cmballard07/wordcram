# Documentation and Examples #

~~Installation documentation (like a standard Processing library)~~

~~Create more examples, and get them into the downloads.~~

~~JavaDoc!  Put it in the code, and put it in the ant script.  Generate
it into a `reference` folder, with an index.html, per the
[library guidelines](http://code.google.com/p/processing/wiki/LibraryGuidelines)~~.

Generate wiki-page documentation for WordPlacers, WordColorers, etc, from javadoc comments?  Auto-deploy them to the wiki svn?

Make a WordCram API cheat-sheet.

~~Tutorial/blog post/example sketches on:~~
  * ~~Word.setSize(), Word.setPlace(), etc.~~
  * ~~Word.getRenderedPlace() vs Word.getTargetedPlace()~~ _for troubleshooting, too_

## WordCrams to Create ##

[Beatles lyrics](http://www.beatleslyricsarchive.com/albums.php),
~~[the US Constitution](http://www.usconstitution.net/const.txt)~~,
~~[popular baby names](http://www.census.gov/genealogy/names/names_files.html)~~,
[Apache license](http://www.apache.org/licenses/LICENSE-2.0.html),
[The Cathedral and the Bazaar](http://catb.org/esr/writings/cathedral-bazaar/),
[The Art of Unix Programming](http://www.faqs.org/docs/artu/)

~~A Blog header from WordCram's source.  The odd dimensions will be a
good test, and it'll require a text provider that can parse out Java
words (variable names, methods, classes, etc) -- along with
[java stop words](http://download.oracle.com/javase/tutorial/java/nutsandbolts/_keywords.html).~~  Throw in the example sketches and wiki pages.  _This is all set,
except it needs a TextSource for loading a source folder of java files.  Once that's
in place, the example can be included with the rest of them,
and this can be crossed off._


# Plug-in Improvements #

## Color ##

Pick some really nice default fonts & colors for demos.  Look at
[colourlovers.com](http://www.colourlovers.com/palette/1281472/Hybrid?widths=1).

Colorers something like http://colorschemedesigner.com's Mono(hue),
Complement(hue), Triad(hue, offsetAngle), etc.

## Auto-Angler ##

An auto-angler that decides whether to rotate a word or not, based on
the destination's aspect ratio.  If it's wide & short, longer words
will be horizontal; if it's tall & narrow, longer words will be
vertical.  Short words will be random.
```
double aspect = width / height;
double lenPercentile = maxWordLen / thisWordLen;
//...not sure of the math here, work it out
```

## Placers ##

A placer that renders bigger words horizontally by weight, and
vertically close to the bottom -- should produce a right triangle w/
the right angle in the bottom left.

## Text Sources ##

new DeliciousTagsTextLoader(username), new RssTextLoader(url), ~~new
HtmlTextLoader(url)~~, new TwitterStreamTextLoader(twitterer), new
JavaSourceCodeTextLoader(srcDir)

_Not sure of this one:_ API change for TextSources: move WordCram methods include/excludeNumbers, withStopWords, and upper/lower/keepCase onto the TextSource.  Rather than WordCram's fromWebPage() and fromTextFile(), it'd just have
`fromTextSource(new TextFile(path, this).excludeNumbers().upperCase())`.  _Well, that last
part sucks.  Maybe not._

~~Text parsing options: case-sensitivity, and whether numbers are included.~~

Make a standard text format for saving (and re-loading) Words, so you
can generate your word weights once, and store it (for faster
applets).

# Core Improvements #

## Layout ##

~~Get the words to render closer to where the Placer places them.  Right
now, the PImage the word is rendered to is so large (to account for
rotated words), that there's a lot of background color between the
point and the first pixels of the word.  This makes it harder to
effectively code up a WordPlacer, and get the output you want.~~
_**DONE:** switched to java.awt.Shapes, which take up minimal room._

~~Move around rendering process -- separate word placement from word
rendering, and render as late as possible.  Cleaner organization, and
will let words be re-colored without being placed again, or re-laid
out without being Shaped again.~~

Keep words from going off-screen.  Scale the window (somehow) to fit words in, when they run off-screen.  There's some basic bounds-checking now, but it could be a lot better.

Try changing the color scheme AFTER rendering it, without totally
re-rendering.  Try re-laying out words with the same settings.

Arbitrary shapes, like tagxedo.com.

## Performance ##

When placing a word, remember which quadrant it's in.  When checking
for colliding words, check the appropriate quadrant first, to speed
things up.

~~Parameterize minShapeSize.~~ _WordCram.minShapeSize(n)_

~~Give WordCram a "max number of words to draw" parameter.~~ _WordCram.maxNumberOfWordsToDraw(n)_

## API ##

~~Give WordCram a fluent builder interface (in addition to the huge one
already there), with sensible overloads (varargs) and sensible defaults.~~

Add more overloads to the fluent builder API.

~~Let users pass a destination PGraphics to WordCram, so it can go to
something other than the host PApplet.~~ _Thanks, Felix!_

~~Fix up `printSkippedWords` so it's clearer.~~ _Renamed it `printWhenSkippingWords`, and clarified the javadoc._

~~Add a method to get the Word at the given (x,y) coordinates.~~  _Done, with a naive implementation, without memoization.  Seems fast enough for now.  If it becomes too slow, try a quad-tree._

~~Provide a way to set/get properties on Words, so you don't _have_ to sub-class Word for simple things.~~ _Word.getProperty and Word.setProperty._

# Building WordCram #

~~GZip the tar downloads.~~

Better unit tests: use [Mockito](http://code.google.com/p/mockito/)? _In progress_