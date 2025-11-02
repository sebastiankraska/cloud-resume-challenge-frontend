+++
title = 'Hello World'
date = 2025-10-30
categories = ["everyday life"]
tags = ["tech", "society", "kaizen"]
series = ["Essays"]
+++
Nothing is here.

Playing around with [Links inside Hugo/Markdown](about.md) and another link [some link text]({{< ref "about.md" >}}) CAUTION: renaming the file that is linked will break both of these links. 

And a third link, this time referencing the slug of the 'target file' over the file name: [About Page](/posts/hey-man-whatsup/) CAUTION: works but isn't validated at build time. Tip: make sure to remove cached files when testing, e.g. `rm -rf public/ resources/`

