# 更新日志


## 1.4.2（2013-07-20）

- 如果不传入“严格运算模式”参数，`font-size`/`line-height`又可以正确计算了
- npmignore中包含了`.gitattributes`
- 属性名可以包含大写字母
- 一些windows路径处理的bug修复（大写字母，路径中有多个`//`等）

## 1.4.1（2013-07-05）

- 修复`syncImports`和`yui-compress`选项，之前它们是被忽略的
- 修复一些全局变量污染的问题
- 处理参数对象为`null`或者`undefined`的情况

## 1.4.0（2013-06-05）

- 修复传入“严格运算模式”参数的bug

## 1.4.0 Beta 4（2013-05-04）

- 将`strictMaths`修改为`strictMath`。可通过在lessc中使用`--strict-math=on`或者在JavaScript中使用`strictMath:true`来开启。
- 将lessc使用的“严格单位模式”选项改为`--strict-units=off`

## 1.4.0 Beta 3（2013-04-30）

- “严格单位模式”默认关闭，在开启的情况下会给出更有用但正确性稍低的结果，如`2px/1px = 2px`
- 处理相对路径中的`./`
- 为混合的guards表达式和非基本单位的情况添加`isunit`函数
- 扩充了可识别的属性集合
- 错误继承自JavaScript中的Error
- 在浏览器中移除es-5-shim
- 修复在windows/linux中处理本地路径的bug

## 1.4.0 Beta 1 & 2（2013-03-07）

- 在选择器中支持`:extend()`（如`input:extend(.button) {}`），在规则中支持`&:extend();`（如`input { &:extend(.button all); }`）。
- 只有在括号中的表达式才算是运算，这意味着`font: statements`、media query以及`calc`函数可以不用使用“避免编译”格式。可以在lessc中通过`--strict-maths-off`或者在JavaScript中通过`strictMaths:false`来关闭这个特性。
- 单位会参与运算，如`200cm+1m = 3m`、`3px/1px = 3`。如果单位无法正确运算的话，将会得到错误。可以通过在lessc中使用`--strict-units-off`或者在JavaScript中通过`strictUnits:false`来关闭这个错误。
- 选择器中使用`(~"@var")`插值的方式被移除了，请使用`@{var}`。
- 导入的默认行为即是对每个文件只导入一次，`@import-once`被移除。
- 可以通过给导入语句指定参数来指定导入的文件是CSS还是LESS，`@import (less) "file.css"`会将`file.css`当作LESS处理
- 混合中的变量不再“泄露”到调用它的作用域中
- 添加了`data-uri`函数，它会将图片通过BASE64编码直接输出到CSS中，如果`ieCompat`选项为`true`，并且文件过大的话，将会回退为`url()`
- 修复debug选项的明显bug
- 在混合中可以使用其它参数作为参数的默认值，例如`.a(@a, @b:@a)`
- 如果在规则范围（即大括号）之外使用CSS属性，会产生一个错误
- 添加`extract`函数用于从一组值中取中一个值，如`extract(12 13 14, 3)` => `3`
- 添加`luma`、`hsvhue`、`hsvsaturation`、`hsvvalue`函数
- 添加`pow`、`pi`、`mod`、`tan`、`sin`、`cos`、`atan`、`asin`、`acos`和`sqrt`数学函数
- 添加转换函数，如`convert(1rad, deg)` => 角度值
- lessc 在输出时如果目标目录不存在会自动创建
- lessc `@import`支持https和301跳转跟踪
- lessc `-depends`选项会以makefile格式输出导入的文件列表
- lessc `-lint`选项只报告错误
- 在属性中以及选择器插值中支持命名空间
- 其它bug修复

## 1.3.3（2012-12-30）

- 修复使用多个括号调用混合时的bug
- 使用`contrast`函数时， 如果第一个参数不是颜色，将会跳过

## 1.3.2（2012-12-28）

browser and server url re-writing is now aligned to not re-write (previous lessc behaviour)
url-rewriting can be made to re-write to be relative to the entry file using the relative-urls option (less.relativeUrls option)
rootpath option can be used to add a base path to every url
Support mixin argument seperator of ';' so you can pass comma seperated values. e.g. .mixin(23px, 12px;);
Fix lots of problems with named arguments in corner cases, not behaving as expected
hsv, hsva, unit functions
fixed lots more bad error messages
fix @import-once to use the full path, not the relative one for determining if an import has been imported already
support :not(:nth-child(3))
mixin guards take units into account
support unicode descriptors (U+00A1-00A9)
support calling mixins with a stack when using & (broken in 1.3.1)
support @namespace and namespace combinators
when using % with colour functions, take into account a colour is out of 256
when doing maths with a % do not divide by 100 and keep the unit
allow url to contain % (e.g. %20 for a space)
if a mixin guard stops execution a default mixin is not required
units are output in strings (use the unit function if you need to get the value without unit)
do not infinite recurse when mixins call mixins of the same name
fix issue on important on mixin calls
fix issue with multiple comments being confused
tolerate multiple semi-colons on rules
ignore subsequant @charset
syncImport option for node.js to read files syncronously
write the output directory if it is missing
change dependency on cssmin to ycssmin
lessc can load files over http
allow calling less.watch() in non dev mode
don't cache in dev mode
less files cope with query parameters better
sass debug statements are now chrome compatible
modifyVars function added to re-render with different root variables
1.3.1
2012-10-18

Support for comment and @media debugging statements
bug fix for async access in chrome extensions
new functions tint, shade, multiply, screen, overlay, hardlight, difference, exclusion, average, negation, softlight, red, green, blue, contrast
allow escaped characters in attributes
in selectors support @{a} directly, e.g. .a.@{a} { color: black; }
add fraction parameter to round function
much better support for & selector
preserve order of link statements client side
lessc has better help
rhino version fixed
fix bugs in clientside error handling
support dpi, vmin, vm, dppx, dpcm units
Fix ratios in media statements
in mixin guards allow comparing colors and strings
support for -*-keyframes (for -khtml but now supports any)
in mix function, default weight to 50%
support @import-once
remove duplicate rules in output
implement named parameters when calling mixins
many numerous bug fixes
1.3.0
2012-03-10

@media bubbling
Support arbitrary entities as selectors
Variadic argument support
Behaviour of zero-arity mixins has changed
Allow @import directives in any selector
Media-query features can now be a variable
Automatic merging of media-query conditions
Fix global variable leaks
Fix error message on wrong-arity call
Fix an @arguments behaviour bug
Fix :: selector output
Fix a bug when using @media with mixins
1.2.1
2012-01-15

Fix imports in browser
Improve error reporting in browser
Fix Runtime error reports from imported files
Fix File not found import error reporting
1.2.0
2012-01-07

Mixin guards
New function percentage
New color function to parse hex color strings
New type-checking stylesheet functions
Fix Rhino support
Fix bug in string arguments to mixin call
Fix error reporting when index is 0
Fix browser support in WebKit and IE
Fix string interpolation bug when var is empty
Support !important after mixin calls
Support vanilla @keyframes directive
Support variables in certain css selectors, like nth-child
Support @media and @import features properly
Improve @import support with media features
Improve error reports from imported files
Improve function call error reporting
Improve error-reporting