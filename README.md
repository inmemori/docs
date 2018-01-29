# Inmemori Http REST API  

### Server

| Env        | Url                              |
|------------|----------------------------------|
| production | `https://api.inmemori.com`       |
| dev        | `https://api.inmemori-dev.com`   |

<br/>
This Api accepts only `json`.

### Authentification

Add your `apikey` in the `body` or the `query` for each query. 

example: `/endpoint?token={yourapikey}`
  
  
<br/>

## Create a page

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



#### Place Schema : information on the ceremonies


| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| date            | `isodate`      | date and time of ceremony| 2018-12-19T11:45:00.000Z       |
| name            | `string`       | location of ceremony| Cimetière de Montparnasse      |
| address         | `string`       | adress of ceremony  | 3 rue de Rivoli, 75014 Paris   |
| type            | `string`       | `ceremony`, `contemplation`, `interment` or `cremation`|     |



#### Contact Schema : information on the organizer of the memorial services


| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| name            | `string `      | first and last names| Sophie Dupont                  |
| phone           | `string `      |                     | 0601020304                     |



#### Meta Schema : information on the page creator


| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| author          | `string `      | counselor's name    | Marc Leblanc                   |
| agency          | `string `      | agency's name       | Pompes Funèbres République     |



### Example

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
