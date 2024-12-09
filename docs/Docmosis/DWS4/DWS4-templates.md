# DWS4 - Templates

### Scope

In general it pays to create/initialize variables in the root context of templates (before going into any repeating sections), this ensures that the variable will be available throughout the entire template (essentially a global variable).
When creating a variable inside of a repeating section, it will only exist within that context (within that repeating section block) and when the repeating section ends, or you jump into another repeating section, or use $top/$parent it won't be available in the new context.

```
# Declare the variable here so it exists in the global scope
<<$asdf=’’>>

<<rs_locations>>
	<<name>><<id>><<$idx>><<$itemidx>>
<<es_locations>>


<<rs_buildings>>
<<value>>

<<$asdf=locid>>
<<$asdf>>
# $asdf can be used even though we are in a different scope
<<$top.locations[$asdf].name>>

<<es_>>

<<rs_buildings>>
<<value>>

<<$top.locations.[buildings.locid].name>>

<<es_>>


```
[See the template guide for more...](https://resources.docmosis.com/Documentation/Cloud/DWS4/Cloud-Template-Guide-DWS4.pdf)

### <<$top>> or <<$root>>

The root of the data regardless of the current position or
context in the template.

### <<$this>> or <<$current>>

The current source of data in the current position in the
template. This allows for anonymous data lookups from
arrays or collections such as <<$current[0]>>.

### <<$parent>>

The parent or container of data in the current context of the
template. Allows data lookup in the current “hotel” when
the current context is a “floor” for example.