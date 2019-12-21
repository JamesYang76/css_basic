# css_basic

## Insert CSS
### External Style Sheet
```html
<head>
  <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```
```html
<style>
  @import url(yourstyle.css)
</style> 
```
### Internal Style Sheet
```html
<head>
   <style>
    body { background-color: linen;}
</style>
</head>   
```
### Inline Styles
```html
<h1 style="color:blue;margin-left:30px;">This is a heading</h1>
```
## Selector
### Combinations of Classes and IDs
#### ID and Class Selector
```html
<style>
   #one.two { color: red; }
</style>

<h1 id="one" class="two">This Should Be Red</h1>
```
#### Double Class Selector
```html
<style>
  .three.four { color: red; }
  .item   { color: yellow; }
  .header { background-color: blue; }
</style>

<h1 class="three four">Double Class</h1>
<h1 class="item header">Lorem ipsum</h1>
```
#### Multiple
```html
<style>
  #header.select.red { color: red; }
</style>

<h1 id="header" class="select red">Double Class</h1>
```

### Combinators and groups of selectors
#### Group of selectors
`A, B` : Any element matching A and/or B
```html
body,p,h1,h2,h3,h4,h5,h6 {margin:0; paddig:0}
```
#### Descendant selectors
`A B`: Any element matching B that is a descendant of an element matching A (that is, a child, or a child of a child, etc.).
```html
<style>
div p {
    background-color: yellow;
}
</style>
<div>
  <p>Paragraph 1 in the div.</p>
  <span><p>Paragraph 2 in the div.</p></span>
</div>
```
#### Child selector
`A > B` : Any element matching B that is a direct child of an element matching A.
```html
<style>
div > p {
    background-color: yellow;
}
</style>
<div>
  <p>Paragraph yellow</p>
   <span><p>Paragraph not yellow</p></span>
</div>
```
#### Adjacent sibling selector
`A + B` : Any element matching B that is the next sibling of an element matching A (that is, the next child of the same parent).
```html
<style>
   h1 + h2 { color: red;}
</style>
<h1> header </h1>
<h2> red </h2>
<h2> not red </h2>
```
#### General sibling selector
`A ~ B` : Any element matching B that is one of the next siblings of an element matching A (that is, one of the next children of the same parent).
```html
<style>
   h1 ~ h2 { color: red;}
</style>
<h1> header </h1>
<h2> red </h2>
<h2> red </h2>
```
### Attribute selectors
#### Presence and value attribute selectors
`[attr]` : This selector will select all elements with the attribute attr, whatever its value.\
`[attr=val]` : This selector will select all elements with the attribute attr, but only if its value is val.\
`[attr~=val]`: This selector will select all elements with the attribute attr, but only if the value val is one of a space-separated list of values contained in attr's value, for example a single class in a space-separated list of classes.
```html
<style>
  [data-vegetable] { color: green; }
  [data-vegetable="liquid"] { background-color: goldenrod;}
  [data-vegetable~="spicy"] { color: red; }
  input[type=text] {background:red;}
</style>
<input type="text" value="red"></input> 
<input type="password"/>
<ul>
  <li data-quantity="1kg" data-vegetable>Tomatoes</li>
  <li data-quantity="3" data-vegetable="liquid">Onions liquid</li>
  <li data-quantity="3" data-vegetable="liquid spicy">Red spicy not liquid</li>
<ul>   
```
#### Substring value attribute selectors
`[attr|=val]` : This selector will select all elements with the attribute attr for which the value is exactly val or starts with val- (careful, the dash here isn't a mistake, this is to handle language codes.)\
`[attr^=val]` : This selector will select all elements with the attribute attr for which the value starts with val.\
`[attr$=val]` : This selector will select all elements with the attribute attr for which the value ends with val.\
`[attr*=val]` : This selector will select all elements with the attribute attr for which the value contains the string val (unlike `[attr~=val]`, this selector doesn't treat spaces as value separators but as part of the attribute value.)
```html
<style>
   [lang|=fr] { font-weight: bold; }
   [data-quantity^="optional"] { opacity: 0.5;}
   [data-quantity$="kg"] { font-weight: bold; }
   [data-vegetable*="not spicy"] { color: green; }
</style>

Ingredients for my recipe: <i lang="fr-FR">Poulet basquaise</i>
<li data-quantity="optional 150kg" data-meat>Bacon bits</li>
<li data-quantity="700g" data-vegetable="not spicy like chili">Red pepper</li>
```
### Pseudo-classes and pseudo-elements
#### Pseudo-classes
```html
<style>
  a:link { color: blue; }          /* Unvisited links */
  a:visited { color: purple; }     /* Visited links */
  a:hover { background: yellow; text-decoration: none; }  /* User hovers */
  a:active { color: lime; }        /* Active links- when click */
</style>

<a href="#">This link will turn lime while you click on it.</a>
```
```html
<style>
  input[type="checkbox"]:checked + div { height:0px; }
  div { overflow: hidden; }
  input[type="text"]:disabled {background: #ccc;}
  input[type="text"]:enabled {background:  blue;}
  input[type="text"]:focus {background-color: orange;}
</style>

 <input type="checkbox"/>
 <div>
   <input type="text" placeholder="Name" disabled/>
   <input type="text" placeholder="enabled"/>
 </div>
```
```html
<!-- :not() -->
<style>
  input:not([type=password]) { background:red; }
</style>
<input type="text"/>
<input type="password"/>  
```
```html
<!--
matches one or more elements of a given type, based on their position among a group of siblings.
-->
<style>
   ul {overflow:hidden;}
   li { list-style:none;float:left;padding: 15px;}
   li:first-child { border-radius: 10px 0 0 10px;}  
   li:last-child { border-radius: 0 10px 10px 0;}  
   li:nth-child(2n+1) { background-color: #800000} 
   li:nth-child(2n) { background-color: #FF0003}
   li:nth-last-child(1) { color: blue}
</style>

<ul>
    <li>First</li>
    <li>Second</li>
    <li>Third</li>
    <li>Forth</li>
    <li>Fifth blue</li>
</ul>
```
```html
<style>
 h1:first-of-type { color:red }
 h1:last-of-type  { color:green }
 /* Even paragraphs */
 p:nth-of-type(2n) { color: blue;}
</style>
<h1>Red</h1>
<h1> Normal </h1>
<h1> Green </h1>
<p> Para </p>
<p> Blue Para </p>

```
#### Pseudo-elements
```html
<style>
   p { counter-increment: rint;}
   p::first-letter { font-size: 3em;}
   p::first-line { color: red;}
   p::before {content: counter(rint) ".";}
   p::after { content: " - " attr(data-page) " page"; }
   
   a:link::after {content: ' - ' attr(href);}
</style>

<p data-page="12"> Para </p>
<p data-page="212"> Blue Para </p>
<a href = "https://github.com/">Github</a>
```

## Box

### display
#### display:none and visibility: hidden
`display:none`: a tag does not take place, while `visibility: hidden`: a tag takes place.

```html
<style>
p {color: red;}
p.ex1 {display: none;}
 p.ex2 {visibility: hidden;}
</style>

<div>
 Lorem ipsum dolor sit amet <p class="ex1">No place</p> Vestibulum volutpat tellus diam
</div>
<div>
 Lorem ipsum dolor sit amet <p class="ex2">Just Take Play like block with no contents</p> 
 Vestibulum volutpat tellus diam
</div>
```
#### display:block
Displays an element as a block element/ It starts on a new line, and takes up the whole width.
   
#### display:inline and inline-block
`display:inline`: Any height and width properties will have no effect, only left and right margin works\
`display:inline-block`: width/height and margin including top,bottom,left,right can be applied.

### box size
#### padding and margin
The padding sets the width of the padding(from inside border to content)\
The margin sets the width of the outer area surrounding the CSS box(from out side border)
```html
<style>
 div {
    margin: 0 30px;  /*top bottom, left right*/
    padding: 0 30px;  /*top bottom, left right*/
  }
</style>
```
#### box-size
```text
box-sizing: content-box : default 
Total width  : content width + 2x(margin + border+padding)
Total height : content height +2x (margin + border+padding)
width:   content width 
height:  content height

box-sizing: border-box`
width : Total width
height: Total height


i.e, for content-box, css property width or height points to only content width or height,
for border-box, it points to  total width or height
```
```html
<style>
div#one {
    border: 1px solid black;
    padding: 10px;
    margin: 10px;
    width: 100px; /* point to only content width*/
    height: 100px;
}
div#two {
    border: 1px solid black;
    padding: 10px;
    margin: 10px;
    width: 100px;  /*points to total width */
    height: 100px;
    box-sizing: border-box;
}
</style>
```
#### Magin Collapse
Top and bottom margins of elements are sometimes collapsed into a single margin that is equal to the largest of the two margins.
```html
<style>
h1 { margin: 0 0 50px 0;}

h2 { margin: 20px 0 0 0; }
</style>

<h1>Heading 1</h1>  <!-- margin between h1 and h2 is 50px-->
<h2>Heading 2</h2>
```

## CSS Positioning
### position
`static`:the normal flow of the document. The top, right, bottom, left, and z-index properties have no effect.\
`relative`: the normal flow of the document, and then offset relative to itself based on the values of top, right, bottom, and left.\
`absolute` : the element is positioned relative to its first positioned (not static) ancestor element\
`fixed` : the element is positioned relative to the browser window\
`sticky`: the element is positioned based on the user's scroll position

#### abolute and relative
If a child element has a `abolute` postion, the parent does not take place\
It the parent has a static postion, child is not positioned according to the parent.
```html
<style>
body > div {
  border: 1px solid black;
}
.box {
   width: 100px;height: 100px;position: absolute;
}
.red { background-color: red; left: 10px; top: 10px; }
.green {background-color: green; left: 50px; top: 50px; }
.blue {background-color: blue; left: 90px; top: 90px; }
</style>

<h1> test </h1>
<div>
    <div class="box red"></div>
    <div class="box green"></div>
    <div class="box blue"></div>
</div>
<h1> bottom test </h1>
```
To iron out them, the parent has to have height and relative position. 
```html
<style>
body > div {
     border: 1px solid black;
     height: 100px; width: 400px;
     position: relative;
 }
</style>   
```
### float
#### left and right
If an element has `float` and the next element has no `float`, the next element width includes the width of the element which has the float because block takes place whole line.\
If an element and the next element have `float`, the next elment width does not take whole line.
```html
<style>
 .float_left {float: left;}
 .float_right { float: right; }
  .box { width: 100px; height: 100px; }
 .red { background-color: red;}
 .blue { background-color: blue;}
</style>

<div class="float_left box red"></div>
<span class="box blue">test</span>
<div class="float_right box blue"></div>
```
#### One true layout
`overflow:hidden` should be applied to the parent whose child has float property because parent cannot recognize height
```html
<style>
   body {width:960px;margin:0 auto;}
   #aside { width:200px; float: left;}
   #section { width:760px;float: left;}
   #wrap {overflow: hidden;}
</style>
<div id="header"></div>
<div id="navigation"></div>
<div id="wrap">
   <div id="aside">
   </div>
   <div id="section">
   </div>
</div>
<div id="footer"></div>
```
#### clear
The clear property specifies on which sides of an element floating elements are not allowed to float.
```html
<style>
   ...
   #footer { clear:both;}
</style>
 ...
```
### Alignment for center
`margin: auto`;\
Setting the width of the element will prevent it from stretching out to the edges of its container.\
The element will then take up the specified width, and the remaining space will be split equally between the two margins:
```html
<style>
    /* #main_header { width: 60; margin:auto;} */
   #main_header { width:960px; margin:0 auto;}
</style>
```
## Font
#### font-size,style and weight
```html
<style>
.a { font-size: 32px; }
.b { font-size: 2em;}
.font_italic { font-style: italic;}
.font_bold { font-weight: bold;}
}
</style>
```
#### font-family
If there is no font, css find second font which is on the list in font-family
```html
<style>
   .font_arial {font-family: 'no font',Arial }
</style>

<p class ="font_aria> Lorem ipsum </p>
```
#### @font-face
Allows authors to specify fonts
```html
<style type="text/css">
/*online url(), and locally local()*/
  
@font-face {
  font-family: "Bitstream Vera Serif Bold your font";
  src: url("https://mdn.mozillademos.org/files/2468/VeraSeBd.ttf"); format('ttf');
}
  
body { font-family: "Bitstream Vera Serif Bold your font", serif }
</style>
```

#### line-height
`line-height` set height of font, but it is used for alignment of vertical.\
This value also take an affect on height of element\
default value is `normal`

```html
<style>
.font_big { font-size: 2em; }
.font_italic { font-style: italic; }
.font_bold { font-weight: bold; }
.font_center { text-align:center; }

.button {
   width:150px;
   height:70px; /* for vertical alignment, height and line-height have the same height*/
   background-color: #FF6A00;
   border: 10px solid #FFFFFF;
   border-radius:30px; box-shadow: 5px 5px 5px #A9A9A9;
}

.button > a {
   display:block;
   line-height: 70px; /* for vertical alignment, height and line-height have the same height*/
   text-decoration:none;
}
</style>
<div class="button">
   <a href="#" class="font_big font_italic font_bold font_center">Click</a>
</div>
```   
#### text-align
describe how inline content like text is aligned in its parent block element
value is `left, right,center,justify`

#### white-sapce
`pre`: Lines are only broken at newline characters in the source and at <br> elements.\
`normal` : Default, Lines are only broken at newline characters in the source and at <br> elements.\
`nowrap`: Suppresses line breaks (text wrapping) within the source.
```html
<style>
p.a { white-space: nowrap; }
p.b { white-space: normal; }
p.c { white-space: pre;}
</style>
```


## media
### media property
#### meda
```html
<head>
  <link rel="stylesheet" href="desktop.css" media="screen"/>
  <link rel="stylesheet" href="print.css" media="print"/>
</head>
```
```html
<style>
  @import url(desktop.css) screen;
  @import url(print.css) print;
 </style>

```
```html
<style>
  @media screen {
    body {color: white;font-fmaily:serif}
  }
  @media print {
     h1{ text-align: center }
  } 
</style>
  
```
### viewport
The viewport is the user's visible area of a web page.\
The viewport varies with the device, and will be smaller on a mobile phone than on a computer screen.
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0,minimum-scale=1.0,user-scalable=no"/>
```

### responsible
#### screen size
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<style>
  @media screen and (max-width: 767px) {
    html{ background:red; }
  }
  @media screen and (min-width: 768px) and (max-width:959px) {
      html{  background:blue; } 
  }
  @media screen and (min-width:960px) {
      html{ background:green; }
  }
</style>  
 ```
 ####  orientation
 confirm screen orientation
 ```html
 <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
 <style>
  @media screen and (orientation: portrait) {
      html{  background:red; }
  }
  @media screen and (orientation: landscape) {
      html{ background:green; }
  }
  </style>
```
#### ratio
check ratina display
 ```html
 <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
 <style>
  @media screen and (-webkit-min-device-pixel-ratio:2) {
    html{ background:red; }
  }
 
  </style>
```
## Tips
### Button with a tag
```html
<style>
   li { list-style:none;}
   a { text-decoration:none;}
   ul { overflow: hidden;}
   ul > li { float: left;}
   ul > li > a {
      display:block; padding: 2px 10px;
      border: 1px solid black;
   }
</style>
<ul>
   <li><a href="#">HTML</a></li>
   <li><a href="#">HTML5</a></li>
</ul>
```
### Ellipsis
`white-sapce, overflow and text-overflow` come togather nomally
```html
<style>
.dexription {
   display: block;
   width:120px;
   
   white-sapce:nowrap;
   overflow: hidden;
   text-overflow: ellipsis;
}
</style>
```
Refer to: https://developer.mozilla.org/en-US/docs/Learn/CSS
