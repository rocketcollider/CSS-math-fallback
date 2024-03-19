# A CSS MathML fallback
This project is from 2017. It is intended as a fallback and by nature not perfect.

***There is NO javascript code! Github's detection seems to be broken somehow.***

## Usage
Have a look at `index.html`. You should see some nice mathematical expressions. Only Firefox and Safari will actually render MathML correctly, though. When a Chromium encounters MathML, it tries to render it as XML elements and looks awful. `cmml.css` needs to be loaded to style that "XML" in ways that look almost right. Due to limitations of CSS (such as no lookahead), not all features of MathML can be implemented. Height-scaling brackets are impossible. The root-symbol is an amalgamation of border and unicode-sign, beauty will depend on the font used.

## Theory of Operation
### Fallback Loading
There exist [browser specific hacks](http://browserhacks.com/#hack-a13653e3599eb6e6c11ba7f1a859193e) to target Safari and Firefox. (Bonus: Chrome #24, the only Chrome to support MathML, is excluded!)

These queries need to be negated, so Firefox and Safari are excluded instead of targeted. I'm not sure weather this works reliably across all browsers, test on your own!

A CSS-file is loaded when MathML is not supported. The according media-query should be:

    not \\0 screen or (-moz-images-in-menus:0)

(a `not` always negates the full media-query.)

Once media-query is cleared, the fallback-css is loaded.

There is a JS-based method of loading fallback-CSS, which looks at the aspect-ration of a fraction. [Fred Wang](https://github.com/fred-wang/mathml.css) uses this method, which should be easy enough to implement, but I wanted a CSS-only solution.

### Styling + Fonts
The fonts are all taken from MathJax. They are loaded inside `local_fonts.css` and need to be declared for the `math` element. (`index.html` uses `MathJax_Size3`.)

### Testing
`index.html` contains a basic implementation and some formulas to test the CSS-fallback. If you use firefox, disable MathML in the about:config and remove the media-selector to test the fallback.

Due to it's very nature, this can't be tested automatically, as it needs to "look similar" in different browsers. (yes, visual AI, but that's too much overkill atm.)

## Motivation
Speed. JS takes time to load and I don't like that. So here is a completely CSS-based MathML fallback. I edited Fred Wang's original CSS a bit, mostly regarding roots.
