---
layout: post
title: "Problems with pip"
description: ""
category: Python
tags: [Python, pip]
---
{% include JB/setup %}

If you've tried installing a package with pip recently, you may have encountered this error:

    Could not fetch URL https://pypi.python.org/simple/Django/: There was a problem confirming the ssl certificate: <urlopen error [Errno 1] _ssl.c:504: error:0D0890A1:asn1 encoding routines:ASN1_verify:unknown message digest algorithm>
      Will skip URL https://pypi.python.org/simple/Django/ when looking for download links for Django==1.5.1 (from -r requirements.txt (line 1))
      Could not fetch URL https://pypi.python.org/simple/: There was a problem confirming the ssl certificate: <urlopen error [Errno 1] _ssl.c:504: error:0D0890A1:asn1 encoding routines:ASN1_verify:unknown message digest algorithm>
      Will skip URL https://pypi.python.org/simple/ when looking for download links for Django==1.5.1 (from -r requirements.txt (line 1))
      Cannot fetch index base URL https://pypi.python.org/simple/
      Could not fetch URL https://pypi.python.org/simple/Django/1.5.1: There was a problem confirming the ssl certificate: <urlopen error [Errno 1] _ssl.c:504: error:0D0890A1:asn1 encoding routines:ASN1_verify:unknown message digest algorithm>
      Will skip URL https://pypi.python.org/simple/Django/1.5.1 when looking for download links for Django==1.5.1 (from -r requirements.txt (line 1))
      Could not fetch URL https://pypi.python.org/simple/Django/: There was a problem confirming the ssl certificate: <urlopen error [Errno 1] _ssl.c:504: error:0D0890A1:asn1 encoding routines:ASN1_verify:unknown message digest algorithm>
      Will skip URL https://pypi.python.org/simple/Django/ when looking for download links for Django==1.5.1 (from -r requirements.txt (line 1))
      Could not find any downloads that satisfy the requirement Django==1.5.1 (from -r requirements.txt (line 1))
    No distributions at all found for Django==1.5.1 (from -r requirements.txt (line 1))
    Storing complete log in /Users/paul/.pip/pip.log

This seems to be an issue with an old version of OpenSSL being incompatible with pip 1.3.1. If you're using a non-stock Python distribution (notably EPD 7.3), you're very likely to have a setup that isn't going to work with pip 1.3.1 without a shitload of work.

The easy workaround for now, is to install pip 1.2.1, which does not require SSL:

    curl -o https://pypi.python.org/packages/source/p/pip/pip-1.2.1.tar.gz
    tar xvfz pip-1.2.1.tar.gz
    cd pip-1.2.1
    python setup.py install

If you are using EPD, and you're not using it for a class where things might break, you may want to consider installing the new incarnation: Enthought Canopy. I know they were aware of the issues caused by the previous version of OpenSSL, and would imagine they are using a new version now that should play nicely with pip 1.3.1.