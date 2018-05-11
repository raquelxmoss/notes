A bit about how CSS works under the hood, guided by [this wonderful article](https://medium.freecodecamp.org/its-not-dark-magic-pulling-back-the-curtains-from-your-stylesheets-c8d677fa21b2)

Browsers contain a Javascript engine (e.g. V8) and a rendering engine (e.g. Webkit, Blink, Gecko).

To render a page, the browser goes through a process that constructs the DOM and CSSOM. This process to construct the DOM and CSSOM is:

- **Conversion**: Reading raw bytes of HTML and CSS off the disc or network. Another person referred to this part as 'scanning'.
- **Tokenization**: Breaking the the html and css into chunks (e.g. start tag, attribute name) and removing whitespace, line breaks, etc.
- **Lexing**: Takes the tokens and identifies each type.
- **Parsing**: Takes the tokens, interprets the tokens using a grammar, and turns it into an abstract syntax tree (the DOM and CSSOM?)

> Once both tree structures are created, the rendering engine then attaches the data structures into what’s called a render tree as part of the layout process.

**I don't quite understand what "attaches the data structures into a render tree" means yet. Does it mean that it takes the ASTs and puts them into this 'render tree'?**

### What is a render tree?

The render tree is a **visual** representation of the document which allows the painting of contents of the page in the correct order.

**Question: where is this visual representation stored? Why is it a visual representation? A computer doesn't have eyes… if we never see it (maybe we do see it?), why is it visual?**

The order:

Start at the root of the DOM tree, traverse each visible node and omit invisible nodes. For each visible node, find the matching CSSOM rules and apply them. Once that's all done, return the render tree with the content & styles of all the visible content on the screen.

> The CSSOM can have drastic effects on the render tree but none on the DOM tree.

Okay, sure.

### Rendering

Once we have a render tree, we can paint the tree. The article also mentions compositing. What's that? It's time for some definitions:

- **Layout**: Calcuating how much space an element will take up and where it is on screen. Parent elements can affect child elements, sometimes vice versa. It is implied in the article that there's more involved in layout.
- **Painting**: Taking each node in the render tree and making it actual pixels on the screen. I'm still confused by the mention of the render tree being a 'visual' representation — to me, the pixels on the screen is the visual representation. Maybe it was just a strange word choice on the author's part. Multiple rounds of painting can happen, caused by JS being loaded that makes changes.
- **Compositing**: Flattening all layers into the final image that we see on screen. In my mind, it's like taking a `.psd` and exporting it to a `.jpg`.

The bigger the size of the element, the longer the paiting time will be. Paiting follows the order that elements are stacked in their stacking context (back to front).

### Hardware Acceleration

When people talk about this, apparently they usually mean 'accelerated compositing', which means using the GPU to do the compositing.

> For example, when using CSS transforms, the will-change property allows for hinting to the browser that a DOM element will be transformed in the near future. This enables offloading some drawing and compositing operations onto the GPU, which can greatly improve performance for pages with a lot of animations. It has similar gains for scroll position, contents, opacity, and top or left positioning.

Good to know.

### Relayout and Repaiting

Changes to certain properties will trigger a repaint, while others will trigger a relayout. My understanding is that a repaint is quicker and easier than a relayout. Changing an element's colour will repaint it, while changing its position will trigger a relayout and repaint of the element, its children, and possibly its siblings.

Increasing the font size of an html element will cause a relayout and repaint of the entire tree (so maybe it would be better to use a css transformation to make the text bigger/smaller?)

## CSSOM

By default, CSS is treated as a render-blocking resource. This means that the broswer will hold rendering of any other process until the CSSOM is constructed.

CSSOM only contains information about visible things on screen (e.g. not meta tags, head, script tags, etc.).

> Another difference between the CSSOM and the DOM is that CSS parsing uses a context free grammar. In other words, the rendering engine does not have code that will fill in missing syntax for CSS like it will when parsing HTML to create the DOM.

**I don't understand this. I can infer that when browsers parse html to create the DOM, the fill in missing syntax. I would like to learn about that.**

So, here's what happens in the browser:

- Browser sends an HTTP request for page
- Web server sends a response
- Browser converts response data (bytes) into tokens, via tokenization
- Browser turns tokens into nodes
- Browser turns nodes into the DOM tree
- Awaits CSSOM tree construction



> I’m also asked frequently about using flexbox versus floats. Of course, flexbox is great from a usability standpoint, but when applied to the same element, a flexbox layout will render in roughly 3.5ms whereas a floated layout can take around 14ms. So, it pays to keep up with your CSS skills just as much as you do your JavaScript skills

Cool