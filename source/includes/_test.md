# Platzi Core API

**Version:** 1.0.0

Monolith API for Platzi

## /api/b2b-v1/activations/{company_id}/

### `GET /api/b2b-v1/activations/{company_id}/`

#### `api_b2b_v1_activations_list`

- **Parameters:**
  - `company_id` (path) - (integer, required)
  - `page` (query) - A page number within the paginated result set. (integer)
  - `page_size` (query) - Number of results to return per page. (integer)

- **Tags:** api

- **Security:**
  - tokenAuth
  - cookieAuth

- **Responses:**
  - `200 OK`
    - Content-Type: application/json
    - Schema: [PaginatedCompanyUserList](#components/schemas/PaginatedCompanyUserList)

### `POST /api/b2b-v1/activations/{company_id}/`

#### `api_b2b_v1_activations_create`

- **Parameters:**
  - `company_id` (path) - (integer, required)

- **Tags:** api

- **Request Body:**
  - Content-Type: application/json
    - Schema: [CompanyUser](#components/schemas/CompanyUser)
  - Content-Type: application/x-www-form-urlencoded
    - Schema: [CompanyUser](#components/schemas/CompanyUser)
  - Content-Type: multipart/form-data
    - Schema: [CompanyUser](#components/schemas/CompanyUser)

- **Security:**
  - tokenAuth
  - cookieAuth

- **Responses:**
  - `200 OK`
    - Content-Type: application/json
    - Schema: [CompanyUser](#components/schemas/CompanyUser)

### `PATCH /api/b2b-v1/activations/{company_id}/`

#### `api_b2b_v1_activations_partial_update`

- **Parameters:**
  - `company_id` (path) - (integer, required)

- **Tags:** api

- **Request Body:**
  - Content-Type: application/json
    - Schema: [PatchedCompanyUser](#components/schemas/PatchedCompanyUser)
  - Content-Type: application/x-www-form-urlencoded
    - Schema: [PatchedCompanyUser](#components/schemas/PatchedCompanyUser)
  - Content-Type: multipart/form-data
    - Schema: [PatchedCompanyUser](#components/schemas/PatchedCompanyUser)

- **Security:**
  - tokenAuth
  - cookieAuth

- **Responses:**
  - `200 OK`
    - Content-Type: application/json
    - Schema: [CompanyUser](#components/schemas/CompanyUser)

### `DELETE /api/b2b-v1/activations/{company_id}/`

#### `api_b2b_v1_activations_destroy`

- **Parameters:**
  - `company_id` (path) - (integer, required)

- **Tags:** api

- **Security:**
  - tokenAuth
  - cookieAuth

- **Responses:**
  - `204 No Content`

## /api/b2b-v1/activations/{company_id}/csv/

### `GET /api/b2b-v1/activations/{company_id}/csv/`

#### `api_b2b_v1_activations_csv_retrieve`

- **Parameters:**
  - `company_id` (path) - (integer, required)

- **Tags:** api

- **Security:**
  - tokenAuth
  - cookieAuth

- **Responses:**
  - `200 OK`
    - No response body

### `POST /api/b2b-v1/activations/{company_id}/csv/`

#### `api_b2b_v1_activations_csv_create`

- **Parameters:**
  - `company_id` (path) - (integer, required)

- **Tags:** api

- **Security:**
  - tokenAuth
  - cookieAuth

- **Responses:**
  - `200 OK`
    - No response body

## /api/b2b-v1/activations/{company_id}/csv/{csv_activations_id}/

### `GET /api/b2b-v1/activations/{company_id}/csv/{csv_activations_id}/`

#### `api_b2b_v1_activations_csv_retrieve_2`

- **Parameters:**
  - `company_id` (path) - (integer, required)
  - `csv_activations_id` (path) - (integer, required)

- **Tags:** api

- **Security:**
  - tokenAuth
  - cookieAuth

- **Responses:**
  - `200 OK`
    - No response body

## /api/b2b-v1/activations/{company_id}/licenses/

### `GET /api/b2b-v1/activations/{company_id}/licenses/`

#### `api_b2b_v1_activations_licenses_retrieve`

- **Description:** Return Response with data containing company licenses, invited quantity, registered quantity, and pending quantity
- **Parameters:**
  - `company_id` (path) - (integer, required)

- **Tags:** api

- **Security:**
  - tokenAuth
  - cookieAuth

- **Responses:**
  - `200 OK`
    - No response body
