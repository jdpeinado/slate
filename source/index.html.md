---
title: Platzi API

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - python

toc_footers:
  - <a href='#'>More information in https://platzi.com/business</a>

includes:
  - licenses
  - activations
  - reports

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for Platzi API
---

# Introducción

Bienvenido a la documentación de la API de Platzi. Aquí encontrarás toda la información necesaria para integrar tu aplicación con Platzi.

Esta API está solo disponibles para empresas que tengan un contrato con Platzi. Una vez se inicie el contrato solo basta contactar con Platzi para proporcionar las credenciales de acceso.

Tenemos ejemplos en python y javascript, dos de los lenguajes más usados en el mundo.

Cualquier mejora por favor contactar a [Platzi](https://platzi.com/contacto).

# Authentication

Para la authorización, todas las llamadas deben ir con dos headers obligatoriamente.

`x-platzi-company-api-key: platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`

`User-Agent: XXXXXXXXXX`

Ambos valores serán proporcionados por Platzi.

Tambien se deberá conocer tu company_id, este valor es un entero que identifica a tu empresa en Platzi. Será proporcionado por Platzi junto a su API Key.


<aside class="notice">
Debes reemplazar <code>platzi-xxxxxxxx.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</code> por tu API Key
</aside>
