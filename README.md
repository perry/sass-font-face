# A bullet-proof Sass `@font-face` mixin

A Sass mixin to take the pain out of creating bullet-proof `@font-face` declarations. With added `@extend` goodness.

## Usage
### Directory structure
You will first need to configure the variable on line 4 of the mixin to reflect the path relative to your CSS file.
The default will provide support for a directory structure like
```
static
├── css
│   └── main.css
└── fonts
│   └── family
│       ├── filename.woff
│       ├── filename.eot
│       ├── filename.ttf
│       └── filename.svg
```

### Using the mixin
Add the mixin file below any compass imports and above any other styles.

***

`@include font-face($style-name, $file, $family, $category)`

`$style-name`: The style name, used for the `@font-face` font-family, the extend classname and font-family.

`$file`: The name of your file (all formats of this style need to have the same file name) without its extention.

`$family`: The font family (NOT the CSS `font-family` e.g. opensans, ptsans, arial, etc) - this is used in the url path.

`$category`: The category of the font, e.g. `serif`, `sans-serif` - this is used in the extend class font-family declaration as a fallback.

For each variation of font that you have, you will need to include the mixin.

#### Example

##### Sass
```
@include font-face('ptsans', 'ptsans-webfont', 'ptsans', 'sans-serif')
@include font-face('ptsans-italic', 'ptsans-italic-webfont', 'ptsans', 'sans-serif')
```

##### Compiled CSS
```
@font-face {
  font-family: "ptsans";
  src: url("../fonts/ptsans/ptsans-webfont.eot");
  src: url("../fonts/ptsans/ptsans-webfont.eot?#iefix") format("embedded-opentype"), url("../fonts/ptsans-webfont-webfont.woff") format("woff"), url("../fonts/ptsans/ptsans-webfont.ttf") format("truetype"), url("../fonts/ptsans/ptsans-webfont.svg#ptsans") format("svg");
}

%ptsans (This is a placeholder selector [SASS - Placeholder](http://sass-lang.com/docs/yardoc/Sass/Selector/Placeholder.html) {
  font-family: "ptsans", sans-serif;
  font-weight: normal;
}

@font-face {
  font-family: "ptsans-italic";
  src: url("../fonts/ptsans/ptsans-italic-webfont.eot");
  src: url("../fonts/ptsans/ptsans-italic-webfont.eot?#iefix") format("embedded-opentype"), url("../fonts/ptsans/ptsans-italic-webfont.woff") format("woff"), url("../fonts/ptsans/ptsans-italic-webfont.ttf") format("truetype"), url("../fonts/ptsans/ptsans-italic-webfont.svg#ptsans-italic") format("svg");
}

.ptsans-italic (See above selector) {
  font-family: "ptsans-italic", sans-serif;
  font-weight: normal;
}
```

And there you have it, bullet-proof `@font-face` that will work in the following browsers ([FontSpring Reference](http://www.fontspring.com/blog/the-new-bulletproof-font-face-syntax/)):

Safari 5.03+, IE 6+, Firefox 3.6+, Chrome 8+, iOS 3.2+, Android 2.2+, Opera 11+

## Using Sass's `@extend` directive

As you may have noticed, the mixin also outputs [placeholder classes](http://sass-lang.com/docs/yardoc/Sass/Selector/Placeholder.html) with properties below each `@font-face` declaration.

This is so we can use [Sass's `@extend` directive](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#extend), which keeps the compiled CSS as well as the Sass DRY.

Instead of declaring the `font-family` and just as importantly the `font-weight: normal` every single time you want to use the font, you can do the following.

```
body
  background: #fff
  @extend %ptsans
  font-size: 14px
  line-height: 1.4
```

which then compiles to


```
@font-face {
  font-family: "ptsans";
  src: url("../fonts/ptsans/ptsans-webfont.eot");
  src: url("../fonts/ptsans/ptsans-webfont.eot?#iefix") format("embedded-opentype"), url("../fonts/ptsans-webfont-webfont.woff") format("woff"), url("../fonts/ptsans/ptsans-webfont.ttf") format("truetype"), url("../fonts/ptsans/ptsans-webfont.svg#ptsans") format("svg");
}

body {
  font-family: "ptsans", sans-serif;
  font-weight: normal;
}

...

body {
  background: #fff;
  font-size: 14px;
  line-height: 1.4
}
```


There we have it, no more repeating `font-family`'s and forgetting to add the important `font-weight: normal` to all your selectors.

Note that the first set of properties will include all other selectors you `@extend` not just the single one we have in this example.


###### References
http://www.fontspring.com/blog/the-new-bulletproof-font-face-syntax/