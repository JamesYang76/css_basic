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



Refer to: https://developer.mozilla.org/en-US/docs/Learn/CSS
