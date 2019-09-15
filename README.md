### sarge
---
https://bitbucket.org/vinay.sajip/sarge/src/default/

https://sarge.readthedocs.io/en/latest/


```py
// sarge/test_feeder.py
import os
import subprocess
import sys
import time

import sarge

try:
  text_type = unicode
except NameError:
  text_type = str
  
def main(args=None):
  feeder = sarge.Feeder()
  p = sarge.run([sys.excutable, 'echoer.py'], input=feeder, async_=True)
  try:
    lines = ('hello', 'goobye')
    gen = iter(lines)
    while p.commands[0].returncode is None:
      try:
        data = next(gen)
      except StopIteration:
        break
      feeder.feed(data + '\n')
      p.commands[0].poll()
      time.sleep(0.05)
  finally:
    p.commands[0].terminate()
    feeder.close()
  
if __name__ == '__main__':
  try:
    rc = main()
  except Exception as e:
    print(e)
    rc = 9
  sys.exit(rc)
```

```
```

```
```
