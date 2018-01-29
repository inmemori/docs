# Inmemori Http REST API  

### Server

| Env        | Url                              |
|------------|----------------------------------|
| production | `https://api.inmemori.com`       |
| dev        | `https://api.inmemori-dev.com`   |

<br/>
This Api accepts only `json`.

### Authentification

Ajoutez votre `apikey` dans le `body` ou la `query` à chaque requêtes. 

exemple: `/endpoint?token={yourapikey}`
  
  
<br/>

## Créer une page  

### `POST /users`

| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| firstname       | `string`       | required            |                                |
| lastname        | `string`       | required            |                                |
| email           | `string`       | required            |                                |
| gender          | `string`       | `m` or `f`          |                                |
| dob             | `isodate`      | date of birth       | 1986-12-19T00:00:00.000Z       |
| dod             | `isodate`      | date of death       | 2018-12-19T00:00:00.000Z       |
| places          | `array(place)` |                     | see **place** schema           |
| contact         | `array(contact)`|                     | see **contact** schema         |


#### Place Schema

| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| date            | `isodate`      |                     | 2018-12-19T11:45:00.000Z       |
| name            | `string`       |                     | Cimetière de Montparnasse      |
| address         | `string`       |                     | 3 rue de Rivoli, 75014 Paris   |
| type            | `string`       | `ceremony`, `contemplation`, `interment` or `cremation`|     |


#### Contact Schema

| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| name            | `string `      |                     | Sophie Dupont                  |
| phone           | `string `      |                     | 0601020304                     |


### Exemple

  ```curl
    curl -X POST 'https://api.inmemori-dev.com/users' \
      -H 'content-type: application/json' \
      -d '{ 
              "firstname": "paul"
            , "lastname": "cezane" 
            , "places": [
                { 
                    "name": "Cimetière de Montparnasse"
                  , "address": "3 rue de Rivoli, 75014 Paris"
                  , "type": "ceremony"
                  , "date": "2018-12-19T11:45:00.000Z"
                }
              ]
           , "contact" : [
               { 
                   "name" : "Sophie Dupont"
                  ,"phone" : "0601020304"
               }
              ] 
          }'
  ```
