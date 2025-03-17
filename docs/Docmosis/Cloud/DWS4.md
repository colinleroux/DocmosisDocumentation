# DWS4 

### Variable Scope

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

#### <<$top>> or <<$root>>

The root of the data regardless of the current position or
context in the template.

#### <<$this>> or <<$current>>

The current source of data in the current position in the
template. This allows for anonymous data lookups from
arrays or collections such as <<$current[0]>>.

#### <<$parent>>

The parent or container of data in the current context of the
template. Allows data lookup in the current “hotel” when
the current context is a “floor” for example.

### Charts

Injecting data into Microsoft Charts is not yet supported. (Dec2024)

Our suggested workaround currently is to generate the chart as an image and then use Docmosis to replace the image.

There are different services that can be used to generate graphs. For example, quickchart.io. Using this service, you can provide a URL in your data, which will generate a chart as an image.

[See quickchart example:](https://quickchart.io/chart?c={type:%27bar%27,data:{labels:[%27Q1%27,%27Q2%27,%27Q3%27,%27Q4%27],%20datasets:[{label:%27Users%27,data:[50,60,70,180]},{label:%27Revenue%27,data:[100,200,300,400]}]}})

If you click that link you will see the image. The challenge for you will be constructing that link before sending it to Docmosis.

Please Note: When sending to Docmosis Cloud, you will need us to whitelist the base URL (https://quickchart.io/). 

There are other services for generating charts, quickchart is just a popular one used by many of our customers.

Use a simple template with PlaceHolder image - bookmark name -imgfit_putChartHere and data below

```json
{"putChartHere": "[imageURL:https://quickchart.io/chart?c=%7B%0A%20%20%22type%22%3A%20%22radar%22%2C%0A%20%20%22data%22%3A%20%7B%0A%20%20%20%20%22labels%22%3A%20%5B%0A%20%20%20%20%20%20%22January%22%2C%0A%20%20%20%20%20%20%22February%22%2C%0A%20%20%20%20%20%20%22March%22%2C%0A%20%20%20%20%20%20%22April%22%2C%0A%20%20%20%20%20%20%22May%22%2C%0A%20%20%20%20%20%20%22June%22%2C%0A%20%20%20%20%20%20%22July%22%2C%0A%20%20%20%20%20%20%22August%22%0A%20%20%20%20%5D%2C%0A%20%20%20%20%22datasets%22%3A%20%5B%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(255%2C%2099%2C%20132%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(255%2C%2099%2C%20132)%22%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%2015.09%2C%0A%20%20%20%20%20%20%20%20%20%2015.67%2C%0A%20%20%20%20%20%20%20%20%20%2012.5%2C%0A%20%20%20%20%20%20%20%20%20%2012.77%2C%0A%20%20%20%20%20%20%20%20%20%2013.62%2C%0A%20%20%20%20%20%20%20%20%20%2013.68%2C%0A%20%20%20%20%20%20%20%20%20%2013.93%2C%0A%20%20%20%20%20%20%20%20%20%2015.95%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22D0%22%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(255%2C%20159%2C%2064%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(255%2C%20159%2C%2064)%22%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%2024.55%2C%0A%20%20%20%20%20%20%20%20%20%2028.91%2C%0A%20%20%20%20%20%20%20%20%20%2021.81%2C%0A%20%20%20%20%20%20%20%20%20%2023.27%2C%0A%20%20%20%20%20%20%20%20%20%2026.98%2C%0A%20%20%20%20%20%20%20%20%20%2026.05%2C%0A%20%20%20%20%20%20%20%20%20%2025.39%2C%0A%20%20%20%20%20%20%20%20%20%2024.92%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22D1%22%2C%0A%20%20%20%20%20%20%20%20%22fill%22%3A%20%22-1%22%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(255%2C%20205%2C%2086%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(255%2C%20205%2C%2086)%22%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%2036.35%2C%0A%20%20%20%20%20%20%20%20%20%2043.93%2C%0A%20%20%20%20%20%20%20%20%20%2032.54%2C%0A%20%20%20%20%20%20%20%20%20%2033.54%2C%0A%20%20%20%20%20%20%20%20%20%2042.82%2C%0A%20%20%20%20%20%20%20%20%20%2039.34%2C%0A%20%20%20%20%20%20%20%20%20%2035.84%2C%0A%20%20%20%20%20%20%20%20%20%2033.5%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22D2%22%2C%0A%20%20%20%20%20%20%20%20%22fill%22%3A%201%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(75%2C%20192%2C%20192%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(75%2C%20192%2C%20192)%22%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%2047.7%2C%0A%20%20%20%20%20%20%20%20%20%2058.92%2C%0A%20%20%20%20%20%20%20%20%20%2044.45%2C%0A%20%20%20%20%20%20%20%20%20%2049.08%2C%0A%20%20%20%20%20%20%20%20%20%2053.39%2C%0A%20%20%20%20%20%20%20%20%20%2051.85%2C%0A%20%20%20%20%20%20%20%20%20%2048.4%2C%0A%20%20%20%20%20%20%20%20%20%2049.36%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22D3%22%2C%0A%20%20%20%20%20%20%20%20%22fill%22%3A%20false%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(54%2C%20162%2C%20235%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(54%2C%20162%2C%20235)%22%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%2060.73%2C%0A%20%20%20%20%20%20%20%20%20%2071.97%2C%0A%20%20%20%20%20%20%20%20%20%2053.96%2C%0A%20%20%20%20%20%20%20%20%20%2057.22%2C%0A%20%20%20%20%20%20%20%20%20%2065.09%2C%0A%20%20%20%20%20%20%20%20%20%2062.06%2C%0A%20%20%20%20%20%20%20%20%20%2056.91%2C%0A%20%20%20%20%20%20%20%20%20%2060.52%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22D4%22%2C%0A%20%20%20%20%20%20%20%20%22fill%22%3A%20%22-1%22%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(153%2C%20102%2C%20255%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(153%2C%20102%2C%20255)%22%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%2073.33%2C%0A%20%20%20%20%20%20%20%20%20%2080.78%2C%0A%20%20%20%20%20%20%20%20%20%2068.05%2C%0A%20%20%20%20%20%20%20%20%20%2068.59%2C%0A%20%20%20%20%20%20%20%20%20%2076.79%2C%0A%20%20%20%20%20%20%20%20%20%2077.24%2C%0A%20%20%20%20%20%20%20%20%20%2066.08%2C%0A%20%20%20%20%20%20%20%20%20%2072.37%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22D5%22%2C%0A%20%20%20%20%20%20%20%20%22fill%22%3A%20%22-1%22%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%5D%0A%20%20%7D%2C%0A%20%20%22options%22%3A%20%7B%0A%20%20%20%20%22maintainAspectRatio%22%3A%20true%2C%0A%20%20%20%20%22spanGaps%22%3A%20false%2C%0A%20%20%20%20%22elements%22%3A%20%7B%0A%20%20%20%20%20%20%22line%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22tension%22%3A%200.000001%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22plugins%22%3A%20%7B%0A%20%20%20%20%20%20%22filler%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22propagate%22%3A%20false%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%22samples-filler-analyser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22target%22%3A%20%22chart-analyser%22%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D]"}
```


### Language/Locale Formatting Examples
---


| Language Name | Code | ISO Code | Number Output                                 | Date Output                                                      |
|---------------|------|----------|-----------------------------------------------|------------------------------------------------------------------|
| English       |      |          | `<<{numFormat(myVal,'#,###.##')}>>`           | `<<{dateFormat(myDate , 'EEEE, dd MMMM yyyy' , 'ddMMyyyy')}>>`   |
| French        | FR   | FRA      | `<<{numFormat(myVal,'# ###,##','fr','false')}>>` | `<<{dateFormat(myDate , 'EEEE, dd MMMM yyyy' , 'ddMMyyyy', 'FR')}>>` |
| Danish        | DA   | DAN      | `<<{numFormat(myVal,'#.###,##','da','false')}>>` | `<<{dateFormat(myDate , 'EEEE, dd MMMM yyyy' , 'ddMMyyyy', 'DA')}>>` |
| Portuguese    | PT   | POR      | `<<{numFormat(myVal,'#.###,##','pt','false')}>>` | `<<{dateFormat(myDate , 'EEEE, dd MMMM yyyy' , 'ddMMyyyy', 'PT')}>>` |
| Spanish       | ES   | SPA      | `<<{numFormat(myVal,'#.###,##','es','false')}>>` | `<<{dateFormat(myDate , 'EEEE, dd MMMM yyyy' , 'ddMMyyyy', 'ES')}>>` |
| Dutch         | NL   | NLD      | `<<{numFormat(myVal,'#.###,##','nl','false')}>>` | `<<{dateFormat(myDate , 'EEEE, dd MMMM yyyy' , 'ddMMyyyy', 'NL')}>>` |
| German        | DE   | DEU      | `<<{numFormat(myVal,'#.###,##','de','false')}>>` | `<<{dateFormat(myDate , 'EEEE, dd MMMM yyyy' , 'ddMMyyyy', 'DE')}>>` |

## Input Data (JSON)
```json
{
  "myVal": "1,234,567.89",
  "myDate": "27012024"
}
```

## More Dates
```json
{
"myDate": "2024-09-16T18:11:00"
}

###Examples

If the Input Format is ISO 8601 (yyyy-MM-dd'T'HH:mm:ss)
For input like 2024-09-16T18:11:00Z:
<<{dateFormat(myDate, 'M/d/yy, h:mm a', ‘yyyy-MM-dd'T'HH:mm:ss’)}>> 
If the Input Format is yyyy-MM-dd
For input like 2024-09-16:

<<{dateFormat('2024-09-16', 'M/d/yy', 'yyyy-MM-dd')}>> 
To include the time, you’d need a combined input format, such as 2024-09-16 18:11 (assuming yyyy-MM-dd HH:mm):

<<{dateFormat('2024-09-16 18:11', 'M/d/yy, h:mm a', 'yyyy-MM-dd HH:mm')}>> 
If the Input Format is Milliseconds Since Epoch (<<$nowMS>>)
To convert milliseconds since epoch to the desired format:

<<{dateFormat($nowUTC, 'M/d/yy, h:mm a')}>> 
If the Input is UTC (<<$nowUTC>>)
For current UTC date and time:

<<{dateFormat($nowUTC, 'M/d/yy, h:mm a', ‘yyyy-MM-dd'T'HH:mm:ssX’)}>> 
Breaking Down the Output Format
M → Month without leading zero (e.g., 9 for September)
d → Day without leading zero (e.g., 16)
yy → Two-digit year (e.g., 24 for 2024)
h → Hour in 12-hour format (e.g., 6)
mm → Minutes with leading zeros if necessary (e.g., 11)
a → AM/PM marker (e.g., PM)

```

## Barcodes

`<<barcode:barcode1:ABC123:code128>>`

specifies barcode1 to have a value of
ABC123 and be of type code128.

So ABC123 =default data to display if name (barcode1) returns null
value
Assuming that you wish to supply a value in your data that is used throughout the
document - for every barcode in the document.
``` js
{
 "data" : "12345678"
 }
 ```

A suggested solution is to create your image bookmarks using variables (note: due to
restrictions in MS Word
we are unable to use the $ symbol in bookmarks, so we use _VAR in the name)

For example name our barcode bookmarks : img_var_barcode1, img_var_barcode2 etc

In our template we create variables which we populate with data  :
```js
<<$barcode1=data>>
<<$barcode2=data>> ... etc
```

We then call the barcode function with this data and fontsize, format etc

`<<barcode:$barcode1:code39:fontSize=2:ec=false>>`

we do this for every barcode bookmark.

## Conditionals

Filter data and show in table with headers if matched data found, don't print blank lines if nothing matches.

```json
{

  "list": [
    {
      "typeID": "1",
      "description": "value2"
    },
    {
      "typeID": "2",
      "description": "value4"
    },
    {
      "typeID": "12",
      "description": "value6"
    }
  ]
}
```

Template
```
<<$showheaders=false>>
<<rs_list:filter(typeID=‘1’)>>
<<$showheaders=true>>
<<es_>>

table
<<cr_$showheaders>>	
TYPE	DESCRIPTION
<<er_>>	
<<rr_list:filter(typeID=‘1’)>>	
<<typeID>> 	<<description>>
<<er_>>	

end table
```

## Merge Fields

The key combination of 
`ALT + F9`
 will toggle the hidden fields for you.

Also `CTRL + A (select all)` followed by `F9` will update the display text for all merge fields and this will make the problem fields more obvious.

## dateFormat and dateAdd
```
<<$formattedDate = {dateFormat(decisionDateTime, ' d-MMM-yyyy', ‘yyyy-MM-dd'T'HH:mm:ss’)}>>
<<$formattedDate>>

With 60 days added: <<{dateAdd($formattedDate, 60, ‘day’)}>> 

OneStep:
<<$date01 = {dateAdd(decisionDateTime,60,’day’, 'd-MMM-yyyy' ,‘yyyy-MM-dd'T'HH:mm:ss’)}>>
<<$date01>>

Data :
{
  "decisionDateTime": "2021-05-25T14:47:03"
}

In Template

<<$datePlus60 = {dateAdd(decisionDateTime,60,’day’, 'd-MMM-yyyy' ,‘yyyy-MM-dd'T'HH:mm:ss’)}>>

After adding 60 Days <<$datePlus60>>
```

### Checkboxes
https://resources.docmosis.com/example-templates/generate-disclosure-form-from-template

Use windings - word-insert-symbols ---

```
Happy	<<cs_isHappy>><<else>><<es_>> Yes	<<cs_isHappy>><<else>><<es_>> No
On leave	<<cs_isOnLeave>><<else>><<es_>> Yes	<<cs_isOnLeave>><<else>><<es_>> No
Ordered	<<cs_isOrdered>><<else>><<es_>> Yes	<<cs_isOrdered>><<else>><<es_>> No
Backordered	<<cs_isBackordered>><<else>><<es_>> Yes	<<cs_isBackordered>><<else>><<es_>> No

{
  "isHappy": "true",
  "isOnLeave": "true",
  "isOrdered": "false",
  "isBackordered": "true"
}

```
## Alternating Table Row Colors

Docmosis has a feature for easily implementing alternating table row colors. If a cell of a row inside a set of repeating rows has a background color different to that of the corresponding cell of the starting row, then the background color for that cell will alternate between that of the starter row and its own background color.
 
This can be disabled with the <<noTableRowAlternate>> field. If the field is placed anywhere in a table, the alternating color is disabled for the specific table. If the field is placed anywhere in the body text of the template, outside of any table, the all the following tables will have no alternating row colors.
 
Uniformly coloring the whole table in the template would also prevent the row alternating.

```
With rr loop

<<noTableRowAlternate>>
<<rr_entries>>
<<cr_{ price != ’’ && discount != ’’ }>>
			<<price>>
<<discount>>
<<er_{ price != ’’ && discount != ’’ }>>
<<er_entries>>


With rs loop

<<rs_entries>>
<<cr_{ price != ’’ && discount != ’’ }>>
			<<price>>
<<discount>>
<<er_{ price != ’’ && discount != ’’ }>>
<<es_entries>>



```