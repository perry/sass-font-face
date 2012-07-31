# A bullet-proof, Sass font-face mixin

A Sass mixin to take the pain out of creating bullet-proof `@font-face` declarations.

## Usage
### Directory structure
You will first need to configure the variable on line 4 of the mixin to reflect the path relative to your CSS file.
The default will rpovide support for a directory structure like
```
static
├── css
│   └── main.css
└── fonts
│   └── set
│       ├── filename.woff
│       ├── filename.eot
│       ├── filename.ttf
│       └── filename.svg
```

### Using the mixin
`@include font-face($family, $file, $set: $family, $typeface: 'sans-serif')`

***

`$family`: The font family, used for the `@font-face` font-family, the extend classname and font-family.

`$file`: The name of your file (all formats of this variation need to have the same file name) without its extention.

`$set`: The font's name (e.g. opensans, ptsans, etc) - this is used in the url path. Defaults to `$family`

`$typeface`: The typeface(?) of the font, e.g. `serif`, `sans-serif` - this is used in the extend class font-family declaration as a fallback. Defaults to `sans-serif`

For each variation of font that you have, you will need to include the mixin.

