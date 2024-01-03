# Reportes

Para obtener reportes de los estudiantes de una compañia.
Se pueden obtener a traves de APIs en GrpahQL o REST.

## GraphQL Endpoints

Se puede explorar nuestra API usando alguna herramienta de graphiql

- Online grpahiql explorer: [GraphiQL](https://www.npmjs.com/package/graphiql) 
- Endpoint: https://api.platzi.com/reports/v1/graphql

<aside class="success">
Recuerda añadir el header <code>x-platzi-company-api-key</code> con tu API Key
</aside>

## CompanyProgressReport

```shell
curl REPORTS_URL \
  -X POST \
  -H "x-platzi-company-api-key: COMPANY_APIKEY" \
  -H "user-agent: USER_AGENT" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "query MyQuery($end_date: Date, $start_date: Date) { companyProgressReport(endDate: $end_date, startDate: $start_date) { companyReport { activeStudents totalApproved totalMinutes } students { name email active activeCourses approvedCourses totalMinutes logDate } } }",
    "variables": {
      "start_date": "2022-01-01",
      "end_date": "2022-12-31"
    }
  }'
```

```python
import requests
from pprint import pprint


print(REPORTS_URL)

headers = {
    'x-platzi-company-api-key': COMPANY_APIKEY,
    'user-agent': USER_AGENT
}

variables = {
  'start_date': '2022-01-01',
  'end_date': '2022-12-31'
}

body = """
query MyQuery($end_date: Date, $start_date: Date) {
  companyProgressReport(endDate: $end_date, startDate: $start_date) {
    companyReport {
      activeStudents
      totalApproved
      totalMinutes
    }
    students {
      name
      email
      active
      activeCourses
      approvedCourses
      totalMinutes
      logDate
    }
  }
}
"""

payload = {'query': body, 'variables': variables}

response = requests.post(url=REPORTS_URL, json=payload, headers=headers)

data = response.json()
if 'errors' in data:
  print('An error occurred:')
pprint(data)
```

Obtiene el progreso de la company

## StudentCoursesReport

```shell
curl REPORTS_URL \
  -X POST \
  -H "x-platzi-company-api-key: COMPANY_APIKEY" \
  -H "user-agent: USER_AGENT" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "query studentCoursesReport($email: String, $start_date: Date, $end_date: Date) { studentCoursesReport(email: $email, startDate: $start_date, endDate: $end_date) { students { name email active lastProgress studentCourses { courseId title status approvedDate time totalTime progress totalProgress logDate } } } }",
    "variables": {
      "email": "john@doe.com",
      "start_date": "2022-01-01",
      "end_date": "2022-12-31"
    }
  }'
```

```python
import requests
from pprint import pprint


print(REPORTS_URL)

headers = {
    'x-platzi-company-api-key': COMPANY_APIKEY,
    'user-agent': USER_AGENT
}

variables = {
  'email': 'john@doe.com', #this filter is optional, see below for more info
  'start_date': '2022-01-01',
  'end_date': '2022-12-31'
}

body = """
query studentCoursesReport($email: String, $start_date: Date, $end_date: Date) {
  studentCoursesReport(email: $email, startDate: $start_date, endDate: $end_date) {
    students {
      name
      email
      active
      lastProgress
    studentCourses {
      courseId
      title
      status
      approvedDate
      time
      totalTime
      progress
      totalProgress
      logDate
      }
    }
  }
}
"""

payload = {'query': body, 'variables': variables}

response = requests.post(url=REPORTS_URL, json=payload, headers=headers)

data = response.json()
if 'errors' in data:
  print('An error occurred:')
pprint(data)
```

Obtiene el progreso por estudiante y cursos.

Hay otras opciones que podrías elegir para agregar a las variables de la solicitud.

- 'emails' es un filtro donde puedes introducir una lista de correos electrónicos para limitar la respuesta. Esta opción es incompatible con el filtro singular 'email' mostrado en el ejemplo anterior, y los intentos de usar ambos serían fallidos.
- 'userIds' es similar, pero en lugar de correos electrónicos, puedes introducir una lista de userIds. Estos son los identificadores que identifican al usuario en nuestra base de datos. Puedes obtener estos ids a partir de la respuesta del endpoint anterior, CompanyProgressReport.

Estas dos opciones, 'emails' y 'userIds', no son incompatibles entre sí, sin embargo, debes tener en cuenta que si incluyes ambas al mismo tiempo, solo aparecerán en la respuesta los usuarios cuyo id y correo electrónico coincidan con ambos filtros.

## StudentStatsReport

```shell
curl REPORTS_URL \
  -X POST \
  -H "x-platzi-company-api-key: COMPANY_APIKEY" \
  -H "user-agent: USER_AGENT" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "query studentStatsReport($user_ids: [Int]!, $start_date: Date, $end_date: Date) { studentStatsReport(userIds: $user_ids, endDate: $end_date, startDate: $start_date) { userId summary { userId activeCourses approvedCourses totalTime totalMaterials logDate } learningAreas { categoryId categoryName share } } } }",
    "variables": {
      "user_ids": [1233456, 987654],
      "start_date": "2022-01-01",
      "end_date": "2022-12-31"
    }
  }'
```

```python
import requests
from pprint import pprint


print(REPORTS_URL)

headers = {
    'x-platzi-company-api-key': COMPANY_APIKEY,
    'user-agent': USER_AGENT
}

variables = {
  'email': 'john@doe.com', #this filter is optional, see below for more info
  'start_date': '2022-01-01',
  'end_date': '2022-12-31'
}

body = """
query studentCoursesReport($email: String, $start_date: Date, $end_date: Date) {
  studentCoursesReport(email: $email, startDate: $start_date, endDate: $end_date) {
    students {
      name
      email
      active
      lastProgress
    studentCourses {
      courseId
      title
      status
      approvedDate
      time
      totalTime
      progress
      totalProgress
      logDate
      }
    }
  }
}
"""

payload = {'query': body, 'variables': variables}

response = requests.post(url=REPORTS_URL, json=payload, headers=headers)

data = response.json()
if 'errors' in data:
  print('An error occurred:')
pprint(data)
```

Obtiene el progreso por estudiante.