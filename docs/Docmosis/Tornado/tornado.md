# Tornado

## Copy files from Windows PC to Linux Tornado Host

```sh title="copy template to tornado server"
C:\Users\Username\Desktop>scp ./alternatingTemplate.docx usern@10.1.1.15:/home/user/docmosisTemplates/
```

## Whitelist images

If the server is running in a docker container this web interface is of little use as the values to be saved 
are lost on server reload which is required for them to take effect.

A work around is to pass the variable through to the container on initial load.

```
$ sudo docker run -p 8080:8080   -v  /home/user/docmosisTemplates:/home/docmosis/templates   -e DOCMOSIS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -e DOCMOSIS_CUSTOMSETTINGS="docmosis.external.resources.whitelist=https://quickchart.io/" -e DOCMOSIS_SITE="Free Trial Tornado"   -e DOCMOSIS_ADMINPW=password   docmosis/tornado
```

Similarly modifying the Dockerfile achieves the same outcome:

`ENV DOCMOSIS_CUSTOMSETTINGS=docmosis.external.resources.whitelist=https://quickchart.io/`

## Foreign Characters 

Adding the following to the dockerfile fixes the problem:

`ENV LANG=C.UTF-8`