FORMAT: 1A
HOST: http://api.qlear.build/

# QLEAR
QLEAR provides a RESTful that enables customers, partners and others to both push data to and retrieve data from QLEAR. Below describes some of the various scenarios that a API user may fall into.

*Note: We are still actively enhancing our public API endpoints and should not be considered stable. However, we will make every effort to avoid breaking changes and give our best effort to alert users any breaking changes that may arise.*


## Root [/]
### Get list of API Endpoints Available [GET]

|          Name           | Type                  |                                                       Description                                             | Required |
|-------------------------|-----------------------|---------------------------------------------------------------------------------------------------------------|----------|
| `token`                 | `string`              |  user's QLEAR API token                                                                                       | true     |

+ Request (application/json)
 
    + Header
    
            Authorization: Bearer <user_auth_token>


+ Response 200 (application/json)

    + Body

           {
               "data": {
                   "locations": "http://api.qlear.build/v2/locations",
               }
           }

# Group Locations
Locations are the physical structure or area that contain monitors and other data sources.

### Fields

|          Name         | Returns  |                                                       Description                                             |
|-----------------------|----------|---------------------------------------------------------------------------------------------------------------|
| `id`                  | `string` | The unique id for the `location`                                                                              |           
| `url`                 | `string` | The URL to this `location` in the API                                                                         |
| `name`                | `string` | `location`'s full name                                                                                        |

## List Locations [/v2/locations/]


+ Model (application/json)

    + Body

           {
               "meta": {
               },
               "data": [
                   {
                       "id": "14221",
                       "url": "http://api.qlear.build/locations/123",
                       "name": "Cafe On Air",
                   },
                                      {
                       "id": "14221",
                       "url": "http://api.qlear.build/v2/locations/123",
                       "name": "Cafe On Air",
                   }
               ]
             }
           }

## Retrieve List of Existing Locations [GET]
A list of `locations` that the current user has access to view and/or read

|          Name           | Type                  |                                                       Description                                             | Required |
|-------------------------|-----------------------|---------------------------------------------------------------------------------------------------------------|----------|
| `token`                 | `string`              |  user's QLEAR API token                                                                                       | true     |


+ Parameters

+ Request (application/json)
    
    + Header
    
            Authorization: Bearer <user_auth_token>
    
+ Response 200

    [List Locations][]

## Retrive a Location [/v2/locations/{id}]
A single `location` resource

+ Model (application/json)

    + Body
    
           {
               "meta": {
               },
               "data": {
                   "id": "123",
                   "url": "http://api.qlear.build/v2/location/123",
                   "name": "Cafe On Air"
               }
           }

## Get a Location [GET]
Returns a single `location` object

+ Parameters
    + id (required, String, `123`) ... `id` of the location.

+ Request (application/json)
    
    + Header
            
            Authorization: Bearer <user_auth_token>

+ Response 200

    [Retrive a Location][]
    
# Group Monitors
Monitors (datasources) are the physical or digital devices that collect data from sensors

### Fields

|          Name         | Returns  |                                                       Description                                             |
|-----------------------|----------|---------------------------------------------------------------------------------------------------------------|
| `id`                  | `string` | The unique id for the location                                                                                |           
| `url`                 | `string` | The URL to this resource in the API                                                                           |
| `name`                | `string` | Monitor full name                                                                                             |

## List Monitors [/v2/monitors/]
A list of `monitors` that the current user has access to view and/or read

+ Model (application/json)

    + Body

           {
               "meta": {
               },
               "data": [
                   {
                       "id": "123",
                       "url": "http://api.qlear.build/v2/monitor/123",
                       "name": "TSI 123",
                   },
                                      {
                       "id": "124",
                       "url": "http://api.qlear.build/v2/monitor/124",
                       "name": "Laser Egg Floor One",
                   }
               ]
             }
           }

## Retrieve List of Existing Monitors [GET]

+ Parameters

+ Request (application/json)
    
    + Header
    
            Authorization: Bearer <user_auth_token>
    
+ Response 200

    [List Monitors][]

## Retrieve a Monitor [/v2/monitor/{id}]
A single `monitor` resource

+ Model (application/json)

    + Body
    
           {
               "meta": {
               },
               "data": {
                   "id": "124",
                   "url": "http://api.qlear.build/v2/monitor/124",
                   "name": "Laser Egg Floor One"
               }
           }

## Get a Monitor [GET]
Returns a single `Monitor` object

|          Name         | Type     |                                                       Description                                             | Required |
|-----------------------|----------|---------------------------------------------------------------------------------------------------------------|----------|
| `id`                  | `string` | The unique id for the location                                                                                |true      |

+ Parameters
    + id (required, String, `123`) ... `id` of the location.

+ Request (application/json)
    
    + Header
            
            Authorization: Bearer <user_auth_token>

+ Response 200

    [Retrieve a Monitor][]

## Monitor Data [/v2/monitor/{id}]
### Retrieve Latest Data for a particular Monitor [GET]

+ Request (application/json)
    
    + Header
    
            Authorization: Bearer <user_auth_token>

+ Parameters
    + monitoridentifier (required, string, `123`) ... `monitor identifier` of the meter.

+ Response 200 (application/json)

    + Body
            
           {
               "meta": {
                       }
                   },
                   "resolution": {
                   }
               },
               "data": [
                   {
                       "value": 19.92683,
                       "localtime": "2013-01-01T00:00:00-06:00"
                   },
                   {
                       "value": 25.26579,
                       "localtime": "2013-02-01T00:00:00-06:00"
                   },
                   {
                       "value": 33.04743,
                       "localtime": "2013-03-01T00:00:00-06:00"
                   },
                   {
                       "value": 21.49092,
                       "localtime": "2013-04-01T00:00:00-05:00"
                   }
               ]
             }
           }

#Group Readings
A description of readings

## Create a Reading [/v2/readings]


### Create a New Reading [POST]

Create a new reading using this action.

|          Name           | Type                  |                                                       Description                                             | Required |
|-------------------------|-----------------------|---------------------------------------------------------------------------------------------------------------|----------|
| `token`                 | `string`              |  User's QLEAR API token                                                                                       | true     |
| `monitor_id`            | `string`              |  Monitor's id                                                                                                 | true     |
| `monitor_label`         | `string`              |  Monitor's label                                                                                              | false    |
| `data`                  | `object` \|\| `array` |  Reading data. Post a single reading as an object, or multiple readings as an array of objects                | true     |
| `timestamp`             | `string`              |  Time at moment of request                                                                                    | true     |

+ Request (application/json)

            {
                "token": "abc123",
                "monitor_id": '123',
                "timestamp": "",
                "data" {
                    {"pm2p5":25, "pm10":10,"reading_time":"2015-02-26 05:33:08+0800"},
                    {"pm2p5":26, "reading_time":"2015-02-26 05:34:08+0800"},
                    {"pm2p5":27, "reading_time":"2015-02-26 05:35:08+0800"}
                ]
            }

+ Response 201 (application/json)

    + Headers

            Location: /v2/readings/

    + Body

                {
                    "meta": {
                        "code": 10000,
                        message: "Success"
                    }
                }
                
# Group Workspaces
A Description of Workspaces

### Fields

|          Name         | Returns  |                                                       Description                                             |
|-----------------------|----------|---------------------------------------------------------------------------------------------------------------|
| `id`                  | `string` | The unique id for the location                                                                                |           
| `url`                 | `string` | The URL to this resource in the API                                                                           |
| `name`                | `string` | Monitor full name                                                                                             |

## List Workspaces [/v2/clients/]
A list of `workspaces` that the current user has access to view and/or read

+ Model (application/json)

    + Body

           {
               "meta": {
               },
               "data": [
                   {
                       "id": "123",
                       "url": "http://api.qlear.build/v2/monitor/123",
                       "name": "TSI 123",
                   },
                                      {
                       "id": "124",
                       "url": "http://api.qlear.build/v2/monitor/124",
                       "name": "Laser Egg Floor One",
                   }
               ]
             }
           }

## Retrieve List of Existing Workspaces [GET]

+ Parameters

+ Request (application/json)
    
    + Header
    
            Authorization: Bearer <user_auth_token>
    
+ Response 200

    [List Workspaces][]

## Retrieve a Workspace [/v2/client/{id}]
A single `monitor` resource

+ Model (application/json)

    + Body
    
           {
               "meta": {
               },
               "data": {
                   "id": "124",
                   "url": "http://api.qlear.build/v2/monitor/124",
                   "name": "Laser Egg Floor One"
               }
           }

## Get a Workspace [GET]
Returns a single `Workspace` object

|          Name         | Type     |                                                       Description                                             | Required |
|-----------------------|----------|---------------------------------------------------------------------------------------------------------------|----------|
| `id`                  | `string` | The unique id for the location                                                                                |true      |

+ Parameters
    + id (required, String, `123`) ... `id` of the location.

+ Request (application/json)
    
    + Header
            
            Authorization: Bearer <user_auth_token>

+ Response 200

    [Retrieve a Workspace][]
