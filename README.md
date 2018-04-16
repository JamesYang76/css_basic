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
