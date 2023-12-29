# Licencias

## Get Licenses info

```shell
curl "https://platzi.com/api/b2b-v1/activations/<COMPANY_ID>/licenses/" \
  -H "x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "User-Agent: XXXXXXXXXX"
```

```python
import requests
from pprint import pprint

path = f'/api/b2b-v1/activations/{COMPANY_ID}/licenses/'
url = f'{PLATZI_HOST}{path}'
print(f'URL: {url}')

headers = {
    'x-platzi-company-api-key': COMPANY_APIKEY,
    'user-agent': USER_AGENT
}

response = requests.get(url, headers=headers)

if response.status_code == 200:
    pprint(response.json())
else:
    print('An error occurred:', response.status_code)
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "students": {
            "total": 50,
            "pending": 2,
            "registered": 48
        },
        "licenses": {
            "active": 30,
            "available": 20,
            "total": 50
        }
    }
}
```

Este endpoint obtiene la información general de las licencias y su uso.

### HTTP Request

`GET https://platzi.com/api/b2b-v1/activations/<company_id>/licenses/`

<aside class="success">
Recuerda — sustituir company_id por su identificador.
</aside>
