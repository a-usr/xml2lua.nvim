# xml2lua.nvim
![](./conversion-ways.png)

A packaging of the xml2lua library for neovim

> *xml2lua* is an XML parser written entirely in Lua which doesn't depend on any external C/C++ library.
It works for Lua 5.1 to 5.3 and enables:
>
> - parsing an XML string into a Lua Table;
> - converting a Lua Table to an XML string.
>
>This version was adapted to work with Lua 5 and can be used in Lua applications, including
interactive Digital Television (DTV) http://gingancl.org.br/en[Ginga NCL applications] for the http://www.dtv.org.br[Brazilian DTV System]
(worldwide known as https://en.wikipedia.org/wiki/ISDB-T_International[ISDB-T International or ISDB-Tb]).
>
>The original parser was written by Paul Chakravarti and is available on http://lua-users.org/wiki/LuaXml[LuaUsers].

## Installation
It is important to note, as this is a library instead of a plugin, there is no `setup` function that has to or can be called

### Using lazy.nvim: 
```lua
{
    "a-usr/xml2lua.nvim"
}
```

### Using pckr.nvim:
```lua
require("pckr").add{
    "a-usr/xml2lua.nvim",
}
```

## Useage
The Following has been taken from the original README and adapted for rendering using markdown

### Parsing an XML String into a Lua Table

A simplified example which parses an XML directly from a string is presented below.
<b> There are some caveats to deal with when an XML has just one tag.
Check the [example1.lua](./examples/example1.lua) for details. </b>

```lua
local xml2lua = require("xml2lua")
--Uses a handler that converts the XML to a Lua table
local handler = require("xmlhandler.tree")

local xml = [[
<people>
  <person type="natural">
    <name>Manoel</name>
    <city>Palmas-TO</city>
  </person>
  <person type="legal">
    <name>University of Brasília</name>
    <city>Brasília-DF</city>
  </person>
</people>
]]

--Instantiates the XML parser
local parser = xml2lua.parser(handler)
parser:parse(xml)

--Manually prints the table (since the XML structure for this example is previously known)
for i, p in pairs(handler.root.people.person) do
  print(i, "Name:", p.name, "City:", p.city, "Type:", p._attr.type)
end
```

### Converting a Lua Table to an XML String

```lua
local xml2lua = require("xml2lua")
local people = {
    person = {
        {name="Manoel", city="Palmas-TO", _attr={ type='natural' } },
        {name="Breno", city="Palmas-TO", _attr={ type='legal' } }
    }
}

print("People Table\n")
xml2lua.printable(people)

print()
print("XML Representation\n")
print(xml2lua.toXml(people, "people"))
```

## License

This code is freely distributable under the terms of the [MIT License](./LICENSE).

## Authors

- Manoel Campos da Silva Filho http://about.me/manoelcampos
- Paul Chakravarti [&#112;a&#117;&#x6c;&#x63;&#x40;&#x70;&#97;&#x73;&#x73;t&#104;&#x65;&#97;a&#114;&#100;&#118;a&#114;k&#x2e;&#99;&#x6f;&#x6d;](mailto:&#112;a&#117;&#x6c;&#x63;&#x40;&#x70;&#97;&#x73;&#x73;t&#104;&#x65;&#97;a&#114;&#100;&#118;a&#114;k&#x2e;&#99;&#x6f;&#x6d;)
