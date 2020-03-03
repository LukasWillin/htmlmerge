htmlmerge
=========

__HTML, CSS and Javascript merging tool__  
Merge all linked _css_ and _javascript_ resources of an _html_ file into a
single file.

### Intention ###
The aim of this script is to decrease TCP connections as much as possible when
loading a webpage. This is achieved by merging as much of your project files as
possible into one single file. Additionally the HTML, CSS and JavaScript in this
file could be compressed by the google htmlcompressor and the Yahoo
YUIcompressor. By that the charging time of the website is significantly
reduced. This is especially interesting for mobile devices.


### Requirements ###
* `Python 3`
* `BeautifulSoup v4` python library
* (optional) Google
  [`htmlcompressor`](http://code.google.com/p/htmlcompressor/downloads/list)
* (optional) Yahoo
  [`YUIcompressor`](https://github.com/yui/yuicompressor/releases)

This script was tested on:
- Unknown Date: `Gentoo Linux` with `Python 3.2.5` and
`BeautifulSoup4`.
- 03.03.2020: `Windows 10 (Version 1809, OS Build: 17763.1039)` with `python3 (3.8.2)` and
`BeautifulSoup4 (4.8.2)`.

### Install ###
Save `htmlmerge` to your bin path and make it executable.
e.g.

    wget https://raw.github.com/fin-ger/htmlmerge/master/htmlmerge
    mv htmlmerge ~/bin/
    chmod +x ~/bin/htmlmerge

Make sure `~/bin/` is in your `$PATH` variable.

### Usage ###
    Usage: htmlmerge infile [options] [-h|--help]
    
    Merge all linked css and javascript resources of an html file into one file
    
    Required arguments:
      infile                Set input html file
                            Use '-' to read piped output from another program
    
    Optional arguments:
      -h, --help            Show short help message and exit
      -l, --long-help       Show this help message and exit
      -V, --version         Show program's version number and exit
      -H, --compress-html   Compress html (Google htmlcompressor required)
      -C, --compile-css     Compile stylesheets (YUIcompressor required)
      -J, --compile-js      Compile javascript (YUIcompressor required)
      -c, --no-css          Disable css merging
      -i, --no-css-import   Disable css @import merging
      -j, --no-js           Disable javascript merging
      -u, --unlock-comments
                            Unlock comments in javascript and css
                            (e.g. /*! ... */ becomes /* ... */)
      -o FILE, --output FILE
                            Set output file (default: merged.html)
                            If the file extension is .gzip the html will be gziped
                            Use '-o -' to pipe output to another program
      -g, --gzip            Force a gziped output. The file extension does not
                            matter.
                            This is useful if you would like to pipe gziped output
      -L VAL, --loglevel VAL
                            Set logging level [quiet|error|warning|info|debug]
                            (default: info)
    
    Javascript and css compiler options:
      YUIcompressor
    
      -w COLUMN, --line-break COLUMN
                            Insert a line break after the specified column number
                            (default: 500)
    
    Javascript compiler options:
      YUIcompressor
    
      --nomunge             Minify only, do not obfuscate
      --preserve-semi       Preserve all semicolons
      --disable-optimizations
                            Disable all micro optimizations
    
    Examples:
      htmlmerge index.html
      htmlmerge index.html -H -C -J -o build/out.html -u
      htmlmerge index.html -H --loglevel quiet -c -i -j
      
    Examples (Windows):
      py htmlmerge index.dev.html -o index.html
    
    For CSS or JavaScript compression, additional YUIcompressor jar file must be
    present in the same directory as this script.
    For HTML compression, additional Google htmlcompressor jar file must be present
    in the same directory as this script.
    
    Copyright (c) Fin Christensen 2013 - All rights reserved!

### How It Works ###
This script searches for `link`, `style` and `script` tags in the given html
file and looks for `src` or `href` attributes. It will write all scripts into
one single `script` tag and all stylesheets into one single `style` tag.
Stylesheets linked via `@import` will be merged, too. If a media query is given
with `@import` the scripts skips the import because this stylesheet is not
needed for all devices. The generated *merged* html will be written to the given
output file. If there is no output file given the script will save to
`merged.html`.

### Todo ###
* convert small graphics to base64 string
* concatenate bigger graphics to one big image
* possibility to compile javascript with Googles closure compiler
* possibility to merge `@import`'s with a media query
* possibility to keep merged sources in single tags
* possibility to pass arguments to htmlcompressor
* add a preset system

### Author ###
Fin Christensen

__License__  
*Have a look into `LICENSE`* `MIT`

__Copyright__  
Copyright &copy; Fin Christensen 2013 - All rights reserved!
