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

** AZURE BLOB and Docker

To configure Tornado to talk to Azure Blobs follow the information below.

Create the Blob Store in Azure
---------------------------
1. create a Blob Store to hold Docmosis Templates
2. upload templates to a folder in that store called "templates"
3. upload images to a folder in that store called "images" (optional) if you want to have
"stock images" uploaded

The blob needs to have read permissions available to the Tornado instance. If Tornado is
running within an azure instance this can be done via a Storage Data Blob Reader role,
otherwise can be done via explicit azure credentials.

Configure Tornado to use the Blob Store
-----------------------------------
1. configure Tornado "Source Templates From" as either:
a. azureblob:<containerName>;<prefix>;<storageAccountName>
- if Tornado is running on an azure instance with a role permitted to read from the blob
store created above.
OR
b. azureblob:<containerName>;<prefix>;<storageAccountName>;<accessKey> - if Tornado is to
be provided with credentials to reach the blob store from anywhere. The accessKey for the
storage account will need to be provided.
2. save the changes (if using the Tornado UI console)
3. restart Tornado (the Java process running it).

## Libreoffice version

` soffice --version`
