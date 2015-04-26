**Warning!** These directions have been rattled off from memory, so if
something doesn't work, send me a note at wordcram at gmail.

# Requirements #

You'll need:

  * svn
  * eclipse
  * ant
  * Processing

# Getting the Source #

Just follow Google's [directions for getting the source](http://code.google.com/p/wordcram/source/checkout).

# Building WordCram #

1. Make a build.properties file in your WordCram directory, with the
a property named `processing.sketchFolder`, set to the path of your
Processing sketch folder.  (It's used in the `publish.local` task,
which builds WordCram and updates your Processing installation, so
you can test out your changes quickly.)

2. `cd` into your WordCram directory, and run `ant`.  This will
create a `build` directory, compile the code, run a few unit tests,
and build a wordcram.jar for you under `build/p5lib/WordCram/library`.

That should be it!  Let me know at wordcram at gmail if you have any
problems.