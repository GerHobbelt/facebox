# Facebox

Facebox is a jQuery-based, Facebook-style lightbox which can display images, divs, or entire remote pages.

[See it in action](http://defunkt.github.com/facebox/).

![Sample Image](http://share.kyleneath.com/captures/Facebox_1.2-20100417-190352.jpg)

[Download the latest release](http://github.com/defunkt/facebox/zipball/master)

## Compatibility

This release relies on a lot of advanced CSS techniques (box-shadow, border-radius, RGBA). That being said, it's compatible with many browsers.

* **Safari 4**
* **Webkit Nightlies** (Chromium, Chrome) as of 4/17/10
* **Firefox 3.5**
* **IE8** (degraded experience)
* **IE7** (degraded experience)
* IE6 - I just don't care
* Opera - I just don't care

## Usage

Include jQuery, `src/facebox.js` and `src/facebox.css`. Then tell facebox where you've put `src/loading.gif` and `src/closelabel.png`

    $.facebox.settings.closeImage = '/images/facebox/closelabel.png'
    $.facebox.settings.loadingImage = '/images/facebox/loading.gif'

Calling facebox() on any anchor tag will do the trick, it's easier to give your Faceboxy links a class="facebox-link"  and hit them all onDomReady.

    jQuery(document).ready(function($) {
      $('.facebox-link').facebox()
    })

Any anchor links with `class="facebox-link"` with now automatically use facebox:

    <a href="#terms" class="facebox-link">Terms</a>
      Loads the #terms div in the box

    <a href="terms.html" class="facebox-link">Terms</a>
      Loads the terms.html page in the box

    <a href="terms.png" class="facebox-link">Terms</a>
      Loads the terms.png image in the box


### Using facebox programmatically

    jQuery.facebox('some html')
    jQuery.facebox('some html', 'my-groovy-style')

The above will open a facebox with "some html" as the content.

    jQuery.facebox(function($) {
      $.get('blah.html', function(data) { $.facebox(data) })
    })

The above will show a loading screen before the passed function is called,
allowing for a better ajaxy experience.

The facebox function can also display an ajax page, an image, or the contents of a div:

    jQuery.facebox({ ajax: 'remote.html' })
    jQuery.facebox({ ajax: 'remote.html' }, 'my-groovy-style')
    jQuery.facebox({ image: 'stairs.jpg' })
    jQuery.facebox({ image: 'stairs.jpg' }, 'my-groovy-style')
    jQuery.facebox({ div: '#box' })
    jQuery.facebox({ div: '#box' }, 'my-groovy-style')

### Events

Want to close the facebox?  Trigger the `close.facebox` document event:

    jQuery(document).trigger('close.facebox')

Facebox also has a bunch of other hooks:

* `loading.facebox`
* `beforeReveal.facebox`
* `reveal.facebox` (aliased as `afterReveal.facebox`)
* `init.facebox`
* `afterClose.facebox`  (callback after closing `facebox`)

Simply bind a function to any of these hooks:

    $(document).bind('reveal.facebox', function() { ...stuff to do after the facebox and contents are revealed... })

### Customization

You can give the facebox container an extra class (to fine-tune the display of the facebox) with the facebox[.class] rel syntax.

    <a href="remote.html" rel="facebox[.bolder]">text</a>

### Caveats

Do not give any DOM element of yours an id of `facebox`. This library creates its own div with an id of `facebox` and you will get unpredictable effects if there are two `#facebox` elements.

## Contact & Help

If you have questions, feel free to ask on the [Google Groups Mailing List](http://groups.google.com/group/facebox/). Alternatively if you find a bug, you can [open an issue](http://github.com/defunkt/facebox/issues).
