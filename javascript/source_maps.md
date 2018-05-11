# What is a source map?

When your javascript is deployed, it's a good idea to compress it, and minify it, bundle it. After all that transformation and mucking around, what happens when it's time to debug? Rather than looking at compressed javascript, it's going to be a lot easier to look at the code that you originally wrote, before it got all mushed together. That's where source maps come in. Source maps help point the path between some processed code and the original file.

Source maps are usually created automatically by tools like Webpack plugins, or similar. You also need to use a browser that supports source maps, which Firefox and Chrome both do.
