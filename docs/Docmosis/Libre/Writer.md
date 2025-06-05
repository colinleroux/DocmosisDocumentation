# Libre Writer

## Font stuff

C:\Users\Colin\AppData\Roaming\LibreOffice\4\user\temp\embeddedfonts\fromsystem

C:\Users\Colin\AppData\Roaming\LibreOffice\4\user\temp\embeddedfonts\fromdocs

### Command Line install

```
C:\Users\Colin\Documents\LibreOffice_versions>

msiexec /a C:\Users\Colin\Documents\LibreOffice_versionsLibO_3.6.7.2_Win_x86_install_multi.msi TARGETDIR="c:\Program Files (x86)\Libre Office3.6.7.2"


msiexec /a ./LibreOffice_24.8.3.1_Win_x86-64.msi TARGETDIR="c:\Program Files(x86)\LibreOffice24.8.3.1

msiexec /a LibreOffice_6.2.8.2_Win_x64.msi "TARGETDIR=c:\program files\LibreOffice6.2.8.2"
```


Take a pop file and convert it to pdf via command line 

`C:\Users\Colin\Documents\Customers\leo-dmirs>"\Program Files\LibreOffice24.8.3.1.new\program\soffice.exe" --convert-to pdf dm_9053388711178713391pop`

this is asycronous so keep looking for the PDF file to appear in the folder : this will run until complete and not be stopped by docmosis after 30seconds

