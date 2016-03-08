
# Senate Lobbying stuff


## Test

(just want to try out xmltodict)

~~~py
from shutil import unpack_archive
from os.path import basename
import requests
import xmltodict
import json
from glob import glob

url = 'http://soprweb.senate.gov/downloads/2015_1.zip'
fname = basename(url)
resp = requests.get(url)
with open(fname, 'wb') as f:
    f.write(resp.content)
unpack_archive(fname)

xmlfiles = glob("*.xml")
xname = xmlfiles[0]
xmltxt = open(xname, 'r', encoding='utf-16').read()
# namespacedata = xmltodict.parse(xmltxt, process_namespaces=True)

data = xmltodict.parse(xmltxt)
jname = xname + '.json'
with open(jname, 'w') as j:
  j.write(json.dumps(data, indent=2))
~~~
