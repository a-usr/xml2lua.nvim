# XML Handlers
This directory contains a list of handlers used by the XML parser to process a XML producing different results.
There are currently 3 available handlers:

- tree: generates a lua table from an XML content string (the most common used handler).
- print: generates a simple event trace which outputs messages to the terminal during the XML parsing, usually for debugging purposes.
- dom: generates a DOM-like node tree structure with a single ROOT node parent.

# Usage
Handlers are usually defined in modules, so to get an instance you'd usually do something like `local handler = require("xml2lua.xmlhandler.tree")`.
Then you have to use one the handler instance when getting an instance of the XML parser using `local parser = xml2lua.parser(handler)`.
This way, the handler is called internally when the `parser:parse(xml)` function is called.

Check the documentation on the root directory for complete examples.
