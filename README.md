### flask-api-utils
---
https://github.com/marselester/flask-api-utils

```py
from api_utils import ResponsiveFlask

app = ResponsiveFlask(__name__)

@app.route('/')
def hello_world():
  return {'hello': 'world'}

def dummy_xml_formatter(*args, **kwargs):
  return '<hello>world</hello>'
  
xml_mimetype = 'application/vnd.company+xml'
app.response_formatters[xml_mimetype] = dummy_xml_formatter

if __name__ == '__main__':
  app.run()
  
from flask import request
from api_utils import ResponsiveFlask

app = ResponseiveFlask(__name__)
def werkzeug_default_exceptions_handler(error):
  error_info_url = (
    'http://developer.example.com/errors/html#error-code-{}'
  ).format(error.code)
  
  response = {
    'code': error.code,
    'message': str(error),
    'info_url': error_info_url,
  }
  return response, error.code
  
@app.errorhandler(404)
def page_not_found(error):
  return {'error': 'This page does not exist'}, 404
  
class MyException(Exception):
  pass
  
@app.errorhandler(MyException)
def special_exeception_handler(error):
  return {'error': str(error)}
  
@app.route('/my-exc')
def hello_my_exception():
  raise MyException('Krivens!')

@app.route('/yarr')
def hello_bad_request():
  request.args['bad-key']
  
if __name__ == '__main__':
  app.run()


from flask import Flask
from api_utils import Hawk

app = Flask(__name__)
hawk = Hawk(app)

@hawk.client_key_loader
def get_client_key(client_id):
  if client_id == 'Alice':
    return 'xxx'
  else:
    raise LookupError()

@app.route('/')
@hawk.auth_required
def index():
  return 'hello world'
  
if __name__ == '__main__':
  app.run()
```

```sh
python api.py
curl http://127.0.0.1:5000/ -i
curl http://127.0.0.1:5000/ -H 'Accept: application/vnd.company+xml' -i
curl http://127.0.0.1:5000/ -H 'Accept: blah/*' -i

curl http://127.0.0.1:5000/yarr -i
curl http://127.0.0.1:5000/ -i
curl http://127.0.0.1:5000/my-exc -i

pip install mohawk

curl http://127.0.0.1:5000/ -i

pip install -r requirements.txt
tox
```

```
HAWK_ALGORITHM = 'sha256'
HAWK_ACCEPT_UNITRUSTED_CONTENT = False
HAWK_LOCALTIME_OFFSET_IN_SECONDS = 0
HAWK_TIMESTAMP_SKEW_IN_SECONDS = 60
```


