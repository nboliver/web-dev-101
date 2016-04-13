# Intro to Web Development

## Text editors
You'll need an text editor to work on your website's files.

[Atom](https://atom.io/) (free)

[Sublime Text](https://www.sublimetext.com/) (unlimited free trial)

## Browser
To preview your work, you'll need to view it in a web browser. Chrome is my preference - it has a bunch of handy dev tools.

[Google Chrome](https://www.google.com/chrome/browser/desktop/)

To access the dev tools panel, you can either `right click -> inspect` or `cmd + opt + i`.

## HTML
An HTML document is the base file that makes up a webpage. 

- HTML stands for Hyper Text Markup Language
- A markup language is a set of markup tags
- HTML documents are described by [HTML tags](http://www.w3schools.com/tags/). Tags usually come in pairs (opening & closing) to wrap their content. `<p>I'm a paragraph tag</p>`. Note the `/` in the closing tag. There are a few tags that are "self closing" - they don't come in pairs, generally because they don't wrap any content. A good example of this is the `<img />` tag.
- Each HTML tag describes different document content, for example: header, footer, article, paragraph, image, etc.
- _Attributes_ are added to tags to provide additional information about an element. They come in name/value pairs like: `name="value"`. Examples of attributes are `src` and `class`: `<img src="img/headshot.jpg" class="thumbnail-image" />`

## CSS 
CSS is used to modify the presentation of our HTML document - in other words, it makes it look good. The same HTML document could be presented an infinite number of ways using CSS. [CSS Zen Garden](http://www.csszengarden.com/), curated by Dave Shea (designer from Vancouver), describes this concept.

CSS is best placed in a separate file which is then linked to our HTML file.

- A CSS _rule_ is made up of a _selector_ and a _declaration block_. 
- The _selector_ selects (points to) the HTML element you want to style.
- The _declaration block_ contains one or more declarations separated by semicolons. These declarations are written as name/value pairs, where the name is the property you want to modify.
- The declaration blocks are wrapped in curly braces.

```
p {
  color: #0000ff;
  text-align: center;
}

```


### Selectors
The basic selectors are: 

- `element`: The element selector selects elements based on the element name. 
- `id`: The id attribute of an HTML element, which should be unique within a page. So, the id selector is used to select one unique element only. The `#` signifies and id. The id attirbute can also be used for jump-links within a single page.
- `class`: Selects HTML elements with the corresponding class attribute. The `.` signifies a class.

```
p {
  color: #0000ff;
  text-align: center;
}

#site-header {
  background-color: #fff;
}

.thumbnail-image {
  width: 100px;
}
```

Selectors can also be grouped together, with a comma separating them.

```
h1, h2, h3, h4, h5, h6 {
  font-family: Arial, Helvetica, sans-serif;
  color: green;
}
```

### The "C" in CSS
The "C" in CSS stands for "Cascading". This concept is essential to understanding how CSS works and to writing good CSS. Consider the following HTML:

```
<p>I'm a paragraph</p>

<p class="highlight">I'm a specially formatted paragraph</p>

<p id="intro-text" class="highlight">I'm a unique paragraph</p>
```

If we write some simple CSS like this, we can see the cascade in action:

```
p {
  color: black;
}

.highlight {
  color: white;
  background-color: black;
}

#intro-text {
  color: red;
  text-align: center;
}
```

All the p tags will _inherit_ the first css rule. Classes have a greater priority / weight, so the `.highlight` rule will over-ride any properties that are set in both the `p` and `.highlight` rules. Ids have a greater priority / weight than classes, so the `#intro-text` rule will over-ride the other two. 

If 2 identical rules (or properties inside a rule) are declared, the one that is further down the list has priority:

```
p {
  color: red;
  color: black; /* text will be black */
}
```

You can also select elements using specificty. Let's say you have that `.highlight` class from above, but now you want any elements with the highlight class that appear in the sidebar to have green text:

```
.sidebar .highlight {
  color: green;
}
```

`.highlight` elements will all be white text with a black background, except if they are in the sidebar, in which case they will have green text. This is because 2 classes have a greater weight than one.

We generally try to write good descriptive class names and keep the number of nested selectors to a minimum, since it's easier to over-ride styles that way.

### Properties
There are way too many properties to list here. Some are straightforward (like `font-family` or `width`). Others are less intuitive, like `display`, `position`, or `float` which are essential for creating the layout of your webpage.

#### `display`
The default display value for most elements is either `block` or `inline`.

- block elements occupy their own line and default to 100% width. Examples: `<div>`, `<p>`, `<h1>`, `<footer>`
- inline elements don't start on a new line and only take up the space they naturally fill. Examples: `<span>`, `<a>`, `<img>`

Other display values:

`display: none;`: Hides an element and the space it would normally occupy on the page.

`display: inline-block;`: Combines features of both inline and block. It only occupies the space it's content naturally fills, but can be modified with other CSS properties, like `width` and `height`.

`display: flex;` A new CSS property that is just starting to be widely adopted by modern browsers. Makes complex layout much easier to create, but is more complex than the other display values. Further reading: [guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

#### `position`
The position property specifies the type of positioning method used for an element.

Once the `position` value is set, elements are then positioned using the `top`, `bottom`, `left`, and `right` properties. However, these properties will not work unless the position property is set first. They also work differently depending on the position value.

There are four different position values:

- `static`: This is the default. Elements are positioned in the natural flow of the document. Basically the order they appear in the HTML. Note that the 4 location properties (`top`, `bottom`, `left`, and `right`) have no affect on elements with `position: static;`
- `relative`: An element is positioned _relative_ to it's normal position, but it's original "footprint" will remain where it would naturally sit. The other very important feature of `relative` elements is that they set the context for any `position: absolute;` elements that are inside them.
- `absolute`: Elements with absolute positioning can be precisely positioned using the 4 location properties. Their "footprint" does not affect the flow of the document, so they can easily overlap other content. A tooltip is a common UI piece that is usually positioned absolutely. If an absolutely positioned element has no ancestor elements that are `position: relative;`, the positioning context is the document. But if there is a relative positioned ancestor, then the 4 location properties will be _relative_ to that elements location.
- `fixed`: Similar to absolute, but always uses the viewport as the context. This is how sticky navbars are positioned.

You can use the `z-index` property to set the stack order of positioned elements.

```
.banner-image {  
  position: absolute;
  z-index: 10;
}
```

#### `float`
Float is used to wrap text around images, but it can also be used for layout. Elements can be floated `left` or `right`.

The `clear` property is used to cancel the floating behavior of elements. It is generally used on a sibling element of the element that is floated.

Elements after a floating element will flow around it. To avoid this, use the clear property.

```
.sidebar {
  float: left;
  width: 200px;
}

.site-footer {
  clear: left;
}
```


### Units
Some basic units are:

- `px`: pixels
- `%`: percent (often relative to a container / parent element)
- `vw` & `vh` viewport width and height 



