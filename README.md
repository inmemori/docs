# InMemori API  

### Server

| Env        | Url                              |
|------------|----------------------------------|
| production | `https://api.inmemori.com`       |
| dev        | `https://api.inmemori-dev.com`   |

<br/>  

This API accepts only `json` as content type.  
There is only one endpoint (`/pages`) on this API.

### Identification

On the `dev` api, you can provide your `jwt` token in the `body` or `query` of the requests, but on the `production` api we we recommend passing the `jwt` in the request `authorization` header (see exemple at the end).

## Create a page

### Http POST request on `/pages`


| Fields          | required| Type           | Info                               | ex:                            |
|-----------------|---------|----------------|------------------------------------|--------------------------------|
| firstname       |    *    | `string`        | firstname of the deceased         | |
| lastname        |    *    | `string`        | lastname of the deceased          | |
| dod             |         | `isodate`       | date of death                     | 2018-12-19T00:00:00.000Z |
| dob             |         | `isodate`       | date of birth                     | 1946-04-11T00:00:00.000Z |
| db              |         | `string`        | database's location               | `us`or `eu` |
| zone            |         | `string`        | zone 's location                  | `fr,us,mx,de,es,be,ch` |
| gender          |         | `string`        | `m` or `f`                        | |
| places          |         | `array(place)`  |                                   | see **place** schema |
| contacts        |         | `array(contact)`|                                   | see **contact** schema |
| meta            |         | `object`        |                                   | see **meta** schema |



#### Place Schema : information on the ceremonies


| Fields          | Type           | Info                | ex:                            |
|-----------------|----------------|---------------------|--------------------------------|
| date            | `isodate`      | date of ceremony at Zulu time (UTC-0)| ex: for an event the 03 dec at 10:30AM in Paris, the correct date would be `2020-12-03T09:30:00.000Z`       |
| tz            | `string`       | time zone| a valid [timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) `Europe/Paris`, `America/Mexico_City`...  |
| name            | `string`       | location of ceremony| Trinity Cemetery ; Cimetière de Montparnasse      |
| address         | `string`       | adress of ceremony  | West 155th Street, New York, NY, USA ; 3 rue de Rivoli, 75014 Paris 
| type            | `string`       | `ceremony`, `contemplation`, `interment` or `cremation`|     |
| privacy         | `boolean`      | default `false`     |     |



#### Contact Schema : information on the contacts/managers of the page


| Fields          | Type           | Info                              | ex:                            |
|-----------------|----------------|-----------------------------------|--------------------------------|
| name            | `string `      | Fullname of the claimant          | Bob Stuart |
| phone           | `string `      | contact mobile number             | +33600000000 |
| email           | `string `      | contact email                     | bob@mail.com |
| relationship    | `string `      | relationship to the deceased      | child/parent/friend |
| address         | `string `      | contact perosnal address          | 20 rue du Louvre, 75001 Paris |



#### Meta Schema : additionnal page informations


| Fields          | Type           | Info                              | ex:                            |
|-----------------|----------------|-----------------------------------|--------------------------------|
| author          | `string `      | counselor's name                  | Marc Leblanc |
| agency          | `string `      | agency's name                     | Smith Funeral services / Pompes Funèbres République |
| agency_code     | `string `      | identification number if any      | AGC01 |
| note            | `string `      | additional information            | comments if any |
| managerName     | `string `      | primary claimant name             | Alice Smith |



### Example
- `jwt` token is `xxx`
- deceased name is `Paul Cezane`
- managers are `alice` & `bob`  

  ```curl
    curl -X POST 'https://api.inmemori-dev.com/pages' \
      -H 'authorization: JWT xxx'
      -H 'content-type: application/json' \
      -d '{ 
              "firstname": "paul"
            , "lastname": "cezane"
            , "dod": "2018-12-19T00:00:00.000Z"
            , "dob": "1964-04-12T00:00:00.000Z"
            , "places": [
                {
                    "type": "ceremony"
                  , "address": "3 rue de Rivoli, 75014 Paris"
                  , "name": "Cimetière de Montparnasse"
                  , "date": "2018-12-19T11:45:00.000Z"
                },
                {
                    "type": "internment"
                  , "address": "14 avenue des Rois, 75011 Paris"
                  , "name": "Chapelle Sixteen"
                  , "date": "2018-12-20T19:30:00.000Z"
                }
              ]
            , "contacts": [
                { 
                    "name": "alice cezane"
                  , "phone": "+33600000001"
                  , "email": "alice@mail.com"
                },
                { 
                    "name": "bob cezane"
                  , "phone": "+33600000002"
                  , "email": "bob@mail.com"
                }
              ] 
            , "meta": {
                  "author": "Marc Leblanc"
                , "agency": "Pompes Funèbres République"
              } 
          }'
  ```
  

## Delete a page

To delete a previously created page, call the endpoint  `PUT /pages/{slug}/cancel`

### Example

- `jwt` token is `xxx`
- page slug (id) is `mdaricout-ex43r`

```curl
curl -X PUT 'https://api.inmemori-dev.com/pages/mdaricout-ex43r/cancel' \
  -H 'authorization: JWT xxx'
```
