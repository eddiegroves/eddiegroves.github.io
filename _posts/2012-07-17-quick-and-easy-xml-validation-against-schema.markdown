---
layout: post
title:  Quick And Easy XML Validation Against Schema
date:   2012-07-17 00:00:00
---

By using `xmllint`, validating XML against a given schema is easy. `Libxml` is a XML processor which includes several tools, one being `xmllint`.

### Installing xmllint on Windows

Currently binaries are available at [zlatkovic.com][1].

Required packages:

* libxml2
* iconv

To install, simply extract the files from the bin directories into somewhere your [PATH][2] can see.

### Validating

    xmllint --noout --schema .\doc\request.xsd .\doc\request.xml
    .\doc\request.xml validates

### Tip for an Validity Error

I'm not an XML expert (and I don't want to be) but I was commonly getting this validation error:

    xmllint --noout --schema .\doc\request.xsd .\doc\request.xml
    ./doc/request.xml:3: element token: Schemas validity error :
        Element '{some_namespace}some_element': This element is not expected.
        Expected is ( some_element ).
    .\doc\request.xml fails to validate                                                                                                                                       

To fix this, I added `elementFormDefault="qualified"` to the XSD root element.

[1]: http://www.zlatkovic.com/libxml.en.html
[2]: https://en.wikipedia.org/wiki/PATH_(variable)

