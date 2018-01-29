# Inmemori Http REST API  

### Server

| Env        | Url                              |
|------------|----------------------------------|
| production | `https://api.inmemori.com`       |
| dev        | `https://api.inmemori-dev.com`   |

<br/>
This Api accepts only `json`.

### Authentification

Ajoutez votre `apikey` dans le `body` ou la `query` à chaque requête. 

exemple: `/endpoint?token={yourapikey}`
  
  
<br/>

## Créer une page  

### `POST /users`

| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| firstname       | `string`       |                     |                                |
| lastname        | `string`       |                     |                                |
| email           | `string`       |                     |sophiedupont1289@mail.com       |
| gender          | `string`       | `m` or `f`          |                                |
| dob             | `isodate`      | date of birth       | 1986-12-19T00:00:00.000Z       |
| dod             | `isodate`      | date of death       | 2018-12-19T00:00:00.000Z       |
| places          | `array(place)` |                     | see **place** schema           |
| contacts        | `array(contact)`|                    | see **contact** schema         |
| meta            | `object`       |                     | see **meta** schema            |


#### Place Schema : récupération des informations sur les différentes étapes des obsèques

| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| date            | `isodate`      | date et heure       | 2018-12-19T11:45:00.000Z       |
| name            | `string`       | nom du lieu         | Cimetière de Montparnasse      |
| address         | `string`       | adresse du lieu     | 3 rue de Rivoli, 75014 Paris   |
| type            | `string`       | `ceremony`, `contemplation`, `interment` or `cremation`|     |


#### Contact Schema : récupération des informations sur l'organisateur des obsèques

| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| name            | `string `      | prénom et nom       | Sophie Dupont                  |
| phone           | `string `      |                     | 0601020304                     |


#### Meta Schema : récupération des informations sur les agences qui créent des pages

| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| author          | `string `      | nom du conseiller   | Marc Leblanc                   |
| agency          | `string `      | nom de l'agence     | Pompes Funèbres République     |


### Exemple

  ```curl
    curl -X POST 'https://api.inmemori-dev.com/users' \
      -H 'content-type: application/json' \
      -d '{ 
              "firstname": "paul"
            , "lastname": "cezane"
            , "email" : "sophiedupont1289@mail.com"
            , "dod" : "2018-12-19T00:00:00.000Z"
            , "places": [
                { 
                    "name": "Cimetière de Montparnasse"
                  , "address": "3 rue de Rivoli, 75014 Paris"
                  , "type": "ceremony"
                  , "date": "2018-12-19T11:45:00.000Z"
                }
              ]
            , "contacts": [
                { 
                    "name" : "Sophie Dupont"
                  , "phone" : "0601020304"
                }
              ] 
            , "meta": {
                  "author" : "Marc Leblanc"
                , "agency" : "Pompes Funèbres République"
              } 
          }'
  ```
