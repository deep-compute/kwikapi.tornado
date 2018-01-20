# Use kwikapi in Tornado
## Install kwikapi for Tornado
```bash
$ pip install kwikapi[tornado]
```

## Example python script to use kwikapi with Tornado(sample.py)
```python
import tornado.ioloop
import tornado.web

from kwikapi.tornado import RequestHandler
from kwikapi import API
from logging import Logger

class BaseCalc():
    def add(self, a: int, b: int) -> int:
        return a + b

    def subtract(self, a: int, b: int) -> int:
        return a - b

api = API(Logger, default_version='v1')
api.register(BaseCalc(), 'v1')

def make_app():
    return tornado.web.Application([
        (r'^/api/.*', RequestHandler, dict(api=api)),
    ])

if __name__ == "__main__":
    app = make_app()
    app.listen(8888)
    tornado.ioloop.IOLoop.current().start()
```
## Run Tornado script
```bash
$ python sample.py
```

## Make API request
```bash
$ curl "http://localhost:8888/api/v1/add?a=10&b=10"
```
