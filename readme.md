# LibreOffice Headless with API in Docker

A docker image that will run [LibreOffice](https://www.libreoffice.org) in headless mode, exposing its Universal Network Objects (UNO) API on port 8100.

I use this together with 2 brilliant Java libraries ([jodconverter](https://github.com/mirkonasato/jodconverter) and [jodreports](http://jodreports.sourceforge.net)) that consume the API to convert documents and generate reports based on [ODT](https://en.wikipedia.org/wiki/OpenDocument) templates.

For convenience I also include the [Universal Office Converter (unoconv)](https://github.com/dagwieers/unoconv) tool in the image.


## Usage

### Run

`docker run -d --name libreoffice -p 8100:8100 hdejager/libreoffice-headless`

### Try out unoconv (convert a HTML file to PDF):

```
docker cp test.html libreoffice:/tmp/test.html
```

```
docker exec -ti libreoffice \
unoconv \
  --connection 'socket,host=127.0.0.1,port=8100,tcpNoDelay=1;urp;StarOffice.ComponentContext' \
  -f pdf /tmp/test.html
```

```
docker cp libreoffice:/tmp/test.pdf .
```
