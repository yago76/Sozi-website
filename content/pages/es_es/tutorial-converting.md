Title: Converting Sozi presentations to PDF or video
Slug: tutorial-converting
Lang: en
Author: Guillaume Savaton
Status: hidden

`sozi-to-pdf` and `sozi-to-video` are command-line tools that you can use to export a presentation
to a single PDF document or to a video.
The source code is available in the [Sozi-export](https://github.com/senshu/Sozi-export)
repository.
These tools are independent from the presentation editor.
They have been tested only for GNU/Linux.


Install
-------

The PDF exporter depends on [pdfjam](http://www2.warwick.ac.uk/fac/sci/statistics/staff/academic-research/firth/software/pdfjam), a shell script for manipulating PDF files.
The video exporter is based on [libav](https://libav.org).
Users of Debian-based distributions can install the *texlive-extra-utils* and *libav-tools* packages.

    :::bash
    apt-get install texlive-extra-utils libav-tools

Both tools are available from a single NPM package.
Install [node.js](https://nodejs.org/) 0.10 or later
(Linux users can use the [NodeSource distributions](https://github.com/nodesource/distributions)),
then:

    :::bash
    npm install -g sozi-export


Convert a Sozi presentation to PDF
----------------------------------

    :::bash
    sozi-to-pdf [options] presentation.sozi.html

Options:

* `-h`, `--help` output usage information
* `-o`, `--output <file>` Output file
* `-W`, `--width <number>` Page width (defaults to 29.7)
* `-H`, `--height <number>` Page height (defaults to 21)
* `-r`, `--resolution <number>` Pixels per width/height unit (defaults to 72)
* `-p`, `--paper <size>` A LaTeX paper size (defaults to 'a4paper')
* `-P`, `--portrait` Set the paper orientation to portrait (disabled by default)
* `-i`, `--include <list>` Frames to include (defaults to 'all')
* `-x`, `--exclude <list>` Frames to exclude (defaults to 'none')

The width, height and resolution options specify the geometry of the browser window
where the presentation is rendered.
The paper and portrait options specify the page format to use in the final PDF document.

The `include` option is always applied before the `exclude` option.
Frames lists have the following syntax:

* `all` selects all frames in the presentation.
* `none` selects no frame.
* A comma-separated list of frame numbers or ranges.
  A range is in the form `first:last` or `first:second:last` where `first`, `second` and `last` are frame numbers.

For instance: `-i 2,4:6,10:12:18` will include frames 2, 4, 5, 6, 10, 12, 14, 16, 18.

Convert a Sozi presentation to video
------------------------------------

    :::bash
    sozi-to-video [options] presentation.sozi.html

Options:

* `-h`, `--help` output usage information
* `-o`, `--output <file>` Output file
* `-W`, `--width <number>` Video width, in pixels (defaults to 1024)
* `-H`, `--height <number>` Video height (defaults to 768)
* `-b`, `--bit-rate <number>` Video bit rate (defaults to 2M)

Known issues and limitations
----------------------------

These tools uses a *headless* web browser for rendering.
[PhantomJS](http://phantomjs.org) and [SlimerJS](https://slimerjs.org/) both have benefits and limitations:

* PhantomJS can render a web page to a PDF document, which preserves the vector graphics and text.
  However, PhantomJS 1.9.19 fails to render the SVG content of a Sozi presentation.
* SlimerJS renders SVG content correctly but it does not support the PDF format.

Currently, the PDF export tool renders each frame to a PNG image and joins them into a PDF document.