# Inmemori Http REST API
----

###Server

| Env        | Url                              |
|------------|----------------------------------|
| production | `https://api.inmemori.com`       |
| dev        | `https://api.inmemori-dev.com`   |

###Authentification

Ajoutez votre `apikey` dans le `body` ou la `query` à chaque requêtes. 

exemple: `/endpoint?token={yourapikey}`
  
  
<br/>
## Créer une page


###`POST /users`

| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| firstname       | `string`       | required            |                                |
| lastname        | `string`       | required            |                                |
| email           | `string`       |                     |                                |
| gender          | `string`       | `m` or `f`          |                                |
| dob             | `isodate`      | date of birth       | 1986-12-19T00:00:00.000Z       |
| dod             | `isodate`      | date of death       | 2018-12-19T00:00:00.000Z       |

###Exemple

  ```curl
    curl -X POST 'https://api.inmemori-dev.com/users' 
      -H 'content-type: application/json' 
      -d '{ "firstname": "paul", "lastname": "cezane" }'
  ```