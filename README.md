# css_basic

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

### Display
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
</style>
```
#### box-size
```text
box-sizing: content-box : default 
Total width  : content width + 2x(margin + border+padding)
Total height : content height +2x (margin + border+padding)

box-sizing: border-box`
Total width  : width + 2x(margin)
Total height : height +2x (margin)

i.e, for content-box, css property width or height points to only content width or height,
for border-box, it points to  conent width + 2x(margin)
```
```html
<style>
div#one {
    border: 1px solid black;
    padding: 10px;
    margin: 10px;
    width: 100px; /* only point to content width*/
    height: 100px;
}
div#two {
    border: 1px solid black;
    padding: 10px;
    margin: 10px;
    width: 100px;  /*points to contend width + left and right margin) */
    height: 100px;
    box-sizing: border-box;
}
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
#### line-height
`line-height` set height of font, but it is used for alignment of vertical.
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


Refer to: https://developer.mozilla.org/en-US/docs/Learn/CSS
