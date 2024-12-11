# DWS4 General


### Docmosis – Language/Locale Formatting Examples
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
