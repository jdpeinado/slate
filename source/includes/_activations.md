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

## Modify Students end date

```shell
curl --location "https://platzi.com/api/b2b-v1/activations/<COMPANY_ID>/" \
  -X PATCH \
  -H "x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "User-Agent: XXXXXXXXXX" \
  --data-raw '{
        "company_user_ids": [123456],
        "end_date": "2025-01-01"
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
    'company_user_ids': [123456],
    'end_date': '2025-01-01'
}

response = requests.patch(url, json=payload, headers=headers)

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
            "company_user_id": 369258,
            "user_id": 123456,
            "name": "Peter Parker",
            "email": "123@test.com",
            "start_date": "2021-01-01T00:00:00",
            "end_date": "2025-12-31T23:59:59.999999",
            "state": "active",
            "error_code": null
        },
        {
            "company_user_id": 369258,
            "user_id": 123456,
            "name": "Mary Jane",
            "email": "123@test.com",
            "start_date": "2021-01-01T00:00:00",
            "end_date": "2025-12-31T23:59:59.999999",
            "state": "active",
            "error_code": null
        }
    ],
    "errors": []
}
```

Este endpoint modifica la fecha de fin de acceso de los estudiantes pasados en company_users_ids, el cual es una lista, y se modificará para todos los que vayan en esa lista.
La fecha no debe ser mayor a la fecha de fin de contrato de la compañia.

### HTTP Request

`PATCH https://platzi.com/api/b2b-v1/activations/<company_id>/`

<aside class="success">
Recuerda — sustituir company_id por su identificador.
</aside>

#### Request Payload

<aside class="pre">
{
    "company_user_ids": [123456],
    "end_date": "2025-01-01"
}
</aside>

El campo end_date debe ser un campo válido y no superior a la fecha de fin de contrato de la compañia.

## Delete Students

```shell
curl --location "https://platzi.com/api/b2b-v1/activations/<COMPANY_ID>/" \
  -X DELETE \
  -H "x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "User-Agent: XXXXXXXXXX" \
  --data-raw '{
        "company_user_ids": [123456],
    }'
```

```python
import requests
from pprint import pprint

path = f'/api/b2b-v1/activations/{COMPANY_ID}/'
url = f'{PLATZI_HOST}{path}'

headers = {
    'x-platzi-company-api-key': COMPANY_APIKEY,
    'user-agent': USER_AGENT,
    'content-type': 'application/json'
}

payload = {
    'company_user_ids': [123445],
}

response = requests.delete(url, json=payload, headers=headers)

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
        'company_user_id': 123456,
        'deleted': True
      }
    ],
    "errors": []
}
```

Este endpoint elimina a los estudiantes de la compañia. El campo company_user_ids es una lista de los estudiantes que se desean eliminar.

### HTTP Request

`DELETE https://platzi.com/api/b2b-v1/activations/<company_id>/`

<aside class="success">
Recuerda — sustituir company_id por su identificador.
</aside>

#### Request Payload

<aside class="pre">
{
    "company_user_ids": [123456]
}
</aside>

## CSV Activations Info

```shell
curl --location "https://platzi.com/api/b2b-v1/activations/<COMPANY_ID>/csv/" \
  -X GET \
  -H "x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "User-Agent: XXXXXXXXXX"
```

```python
import requests
from pprint import pprint

path = f'/api/b2b-v1/activations/{COMPANY_ID}/csv/'
url = f'{PLATZI_HOST}{path}'

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
            "csv_activations_id": 1,
            "created_at": "2023-04-01T02:46:46.859907Z"
        }
    ]
}
```

Se pueden realizar activaciones de manera masiva a traves de archivo CSV.
Este endpoint obtiene la lista de activaciones de CSV que se han realizado.
Con el id se puede consultar el estado concreto de esa activación

### HTTP Request

`GET https://platzi.com/api/b2b-v1/activations/<company_id>/csv/`

<aside class="success">
Recuerda — sustituir company_id por su identificador.
</aside>

## CSV Activations Deatil

```shell
curl --location "https://platzi.com/api/b2b-v1/activations/<COMPANY_ID>/csv/<csv_activations_id>/" \
  -X GET \
  -H "x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "User-Agent: XXXXXXXXXX"
```

```python
import requests
from pprint import pprint

path = f'/api/b2b-v1/activations/{COMPANY_ID}/csv/<csv_activations_id>/'
url = f'{PLATZI_HOST}{path}'

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
        "global_status": "pending",
        "results": [
            {
                "status": "ok",
                "email": "correo@mail.com",
                "company_user_id": 123456
            },
            {
                "status": "pending",
                "email": "correo2@mail.com",
                "company_user_id": null
            }
        ]
    }
}
```

Para una activación realizada a través de CSV, se puede consultar el estado de cada uno de los estudiantes que se han pasado en el CSV y su estado.

### HTTP Request

`GET https://platzi.com/api/b2b-v1/activations/<company_id>/csv/<csv_activations_id>/`

<aside class="success">
Recuerda — sustituir company_id por su identificador.
</aside>

## CSV Activations Create

```shell
curl --location "https://platzi.com/api/b2b-v1/activations/<COMPANY_ID>/csv/" \
 -X POST \
 -H "x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
 -H "User-Agent: XXXXXXXXXX" \
 -H "content-type: text/csv" \
 -H "Content-Disposition: attachment;filename=template.csv" \
 --data-binary "@./template.csv"
```

```python
import pandas as pd
import requests
from pprint import pprint

path = f'/api/b2b-v1/activations/{COMPANY_ID}/csv/'
url = f'{PLATZI_HOST}{path}'
print(f'URL: {url}')

headers = {
    'x-platzi-company-api-key': COMPANY_APIKEY,
    'user-agent': USER_AGENT,
    'content-type': 'text/csv'  ,
    'Content-Disposition': 'attachment;filename=template.csv',
}

csv_data = [
    {
        'name': 'Test One',
        'email': 'test@one.com',
        'is_admin': False,
        'end_date': '2025-01-01'
    },
    {
        'name': 'Test Two',
        'email': 'test@two.com',
        'is_admin': True,
        'end_date': '2025-01-01'
    },
]

df = pd.DataFrame(csv_data)
file_path = './template.csv'
df.to_csv(file_path, index=False, encoding='utf-8')
data = open(file_path, 'rb').read()
response = requests.post(url, data=data, headers=headers)

if response.status_code == 202:
    pprint(response.json())
else:
    print('An error occurred:', response.json())
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "csv_activations_id": 1
    }
}
```

Para realizar una activación masiva a través de CSV, se debe enviar un archivo CSV con los datos de los estudiantes.
El archivo debe tener el siguiente formato:

<aside class="pre">
NOMBRE,CORREO
Maria Perez,correo@mail.com
</aside>

### HTTP Request

`GET https://platzi.com/api/b2b-v1/activations/<company_id>/csv/`

<aside class="success">
Recuerda — sustituir company_id por su identificador.
</aside>