# Activaciones de estudiantes

## Get List Students

```shell
curl --location "https://platzi.com/api/b2b-v1/activations/<COMPANY_ID>/" \
  -H "x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "User-Agent: XXXXXXXXXX"
```

```python
import requests
from pprint import pprint

path = f'/api/b2b-v1/activations/{COMPANY_ID}/'
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
    "data": [
        {
            "company_user_id": 123456,
            "user_id": 987654,
            "name": "John Doe",
            "email": "john@test.com",
            "start_date": "2021-01-01T00:00:00",
            "end_date": "2025-12-31T23:59:59.999999",
            "state": "processing",
            "error_code": null
        }
    ],
    "metadata": {
        "count": 5,
        "pages": 1,
        "current_page": 1
    }
}
```

Este endpoint obtiene la lista de estudiantes de la compañia.
Tienen los siguientes estados:

* active
* inactive
* matriculate
* processing
* error

### HTTP Request

`GET https://platzi.com/api/b2b-v1/activations/<company_id>/`

<aside class="success">
Recuerda — sustituir company_id por su identificador.
</aside>

## Create Students

```shell
curl --location "https://platzi.com/api/b2b-v1/activations/<COMPANY_ID>/" \
  -X POST \
  -H "x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "User-Agent: XXXXXXXXXX" \
  --data-raw '{
        "students": [
            {
                "name": "Test Post1",
                "email": "post1@test.com",
                "end_date": "2024-01-01",
                "is_admin": False
            },
            {
                "name": "Test Post2",
                "email": "post2@test.com",
                "end_date": "2023-04-01",
                "is_admin": True
            }
        ]
    }'
```

```python
import requests
from pprint import pprint

path = f'/api/b2b-v1/activations/{COMPANY_ID}/'
url = f'{PLATZI_HOST}{path}'
print(f'URL: {url}')

headers = {
    'x-platzi-company-api-key': COMPANY_APIKEY,
    'user-agent': USER_AGENT,
    'content-type': 'application/json'
}

payload = {
    "students": [
        {
            "name": "Test Post1",
            "email": "post1@test.com",
            "end_date": "2024-01-01",
            "is_admin": False
        },
        {
            "name": "Test Post2",
            "email": "post2@test.com",
            "end_date": "2023-04-01",
            "is_admin": True
        }
    ]
}

response = requests.post(url, json=payload, headers=headers)

if response.status_code == 200:
    pprint(response.json())
else:
    print('An error occurred:', response.status_code)
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "company_user_id": 123456,
            "user_id": 987654,
            "name": "Test Post1",
            "email": "post1@test.com",
            "start_date": "2021-01-01T00:00:00",
            "end_date": "2024-01-01T23:59:59.999999",
            "state": "active",
            "error_code": null
        },
        {
            "company_user_id": 369258,
            "user_id": 258147,
            "name": "Test Post2",
            "email": "post2@test.com",
            "start_date": "2021-01-01T00:00:00",
            "end_date": "2023-04-011T23:59:59.999999",
            "state": "inactive",
            "error_code": null
        }
    ],
    "errors": []
}
```

Este endpoint crea e invita (envía correo de activación) a la lista de estudiantes que se pasen en el payload.

### HTTP Request

`POST https://platzi.com/api/b2b-v1/activations/<company_id>/`

<aside class="success">
Recuerda — sustituir company_id por su identificador.
</aside>

#### Request Payload

<aside class="pre">
{
    "students": [
        {
            "name": "Test Post1",
            "email": "post1@test.com",
            "end_date": "2024-01-01",
            "is_admin": False
        },
        {
            "name": "Test Post2",
            "email": "post2@test.com",
            "end_date": "2023-04-01",
            "is_admin": True
        }
    ]
}
</aside>

El campo end_date debe ser un campo válido y no superior a la fecha de fin de contrato de la compañia.
is_admin es opcional, por defecto es False. Para activar un admin que tenga acceso al dashboard.
