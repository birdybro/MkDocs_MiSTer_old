# MkDocs_MiSTer

https://birdybro.github.io/MkDocs_MiSTer/

A work-in-progress replacement for the MiSTer FPGA Github Wiki. 

In order to contribute to this documentation repository first please read the instructions on MkDocs' website --> https://www.mkdocs.org/user-guide/writing-your-docs/

Try your best to follow along with the general structure of folders (categories) and the quality of the articles. Remember, quality over quantity. :)

It's very easy to contribute, just fork this repo, make your changes (such as making a new markdown file or editing one) and follow normal markdown syntax, commit changes to your fork, submit your pull request, and we will review it to see if it's suitable to merge.

## Useful resources

https://www.markdownguide.org/tools/mkdocs/

## Style guide

Any internally facing links must be relative links. `./docs` is the implicit root folder, so if you want to link to the assets folder you just need to use `/assets/` and type in the file that you want to link to in there.

Any externally facing links need to use "open link in new tab" by default, so as not to confuse the user and keep them on their setup step, reduce the need to click "back", etc... This is enabled by the `- attr_list` extension. To do this, just add `{target=_blank}` to the end of your link. e.g.:

`[DE10-Nano](http://de10-nano.terasic.com){target=_blank}`

Make images links when it may benefit the user. Here is the syntax:

`[![Download Mr. Fusion](dl-mr-fusion.png)](https://github.com/MiSTer-devel/mr-fusion/releases){target=_blank}`

To embed a video:

`![type:video](videos/downloader.mp4)`

To link to another doc with a specific sub-url:

`[WiFi tutorial](wifi.md#setup-wifi-with-a-script)`

## Prerequisites and deploying a local environment

* Python 3
* Pip

Make sure you update [python 3](https://www.python.org/downloads/) and [update pip](https://pip.pypa.io/en/stable/installation/).

`cd` into the root folder of this repo and install these modules:

`pip install mkdocs mkdocs-material mkdocs-minify-plugin mkdocs-redirects mkdocs-video mkdocs-git-revision-date-localized-plugin mkdocs-rss-plugin`

Deploy to local server from that root folder:

```
mkdocs serve
```

And it should give you a weburl in the terminal to go to, http://127.0.0.1:8000

## Credits

Huge thanks to @tofukazoo (Jorge González) for helping me with the initial GitHub automation, lots of conceptual brainstorming, important early-stage debating, and finally the motivation and encouragement to get this project going!

Thanks to [@Kitrinx](https://github.com/Kitrinx/), [@sentientsix](https://github.com/sentientsix), [@alanswx](https://github.com/alanswx/), [@MiSTerAddons](https://github.com/misteraddons), [@Tonurics](https://github.com/tonurics/), [@theypsilon](https://github.com/theypsilon/), and many more for so much help and advice with the content written on the initial layout!

Thanks to [@hewhoisred](https://github.com/hewhoisred) for supplying art and giving expert UI design and aesthetics advice!

Thanks to [@sorgelig](https://github.com/sorgelig/) (Alexey Melnikov) for all of his amazing hard work on the MiSTer FPGA project that we all are so happy to enjoy!
