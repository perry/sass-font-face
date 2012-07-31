# A bullet-proof, sass font-face mixin

`@mixin font-face($family, $file, $set: $family, $typeface: 'sans-serif')
  @font-face
    font-family: "#{$family}"
    $filepath: "../fonts/" + $set + "/" + $file
    src: url($filepath + ".eot?#iefix") format('embedded-opentype'), url($filepath + ".woff") format('woff'), url($filepath + ".ttf")  format('truetype'), url($filepath + ".svg#" + $family + "") format('svg')

  .#{$family}
    font:
      family: "#{$family}", #{$typeface}
      weight: normal
`