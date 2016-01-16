# python-pprint-json
Pretty print in json-format from stdin to stdout

```
#!/usr/bin/python

import json
import sys
import pprint

# http://stackoverflow.com/questions/5203105/printing-a-utf-8-encoded-string
# and http://stackoverflow.com/questions/1473577/writing-unicode-strings-via-sys-stdout-in-python
# import sys, codecs, locale
# print str(sys.stdout.encoding);
# sys.stdout = codecs.getwriter(sys.stdout.encoding)(sys.stdout);

# http://stackoverflow.com/questions/10883399/unable-to-encode-decode-pprint-output
class MyPrettyPrinter(pprint.PrettyPrinter):
  def format(self, object, context, maxlevels, level):
    if isinstance(object, unicode):
      return (object.encode('utf8'), True, False)
    return pprint.PrettyPrinter.format(self, object, context, maxlevels, level)

s = sys.stdin.read().strip()
data = json.loads(s)
# pprint.pprint(data)
MyPrettyPrinter().pprint(data)
```
