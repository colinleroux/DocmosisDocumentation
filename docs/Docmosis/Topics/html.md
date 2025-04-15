# HTML in Docmosis

### Support in Docmosis for HTML is very limited.

### When data (html) is injected into a template via the `<<html:xxx>>` it is styled using the Body Text style - which is inturn based on the Normal style.

Should you desire a certain style for html in a document - this is an easy way to achieve this.

html tags / content shouldnot be set to full justify (in word).

It does not matter what styles or inline formatting are
applied to the field, the style named "Body Text" will set the formatting
of the output.

Strip unwanted p tags 

```
<<$HelpText={replaceStr(HelpText,'<p>','')}>>
<<$Stripped={replaceStr($HelpText,'</p>','')}>>
<<$myindex={indexOf(‘$Stripped’, ‘<’)=-1}>>
<<cs_{$myindex=’true’}>>
<<$Stripped>>
<<else>>
<<html:HelpText>>
<<es_>>

```