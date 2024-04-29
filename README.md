# HomeDots API Endpoints

### APIs for Device

<!-- Get License -->
<details>
 <summary><code>POST</code> <code><b>/getLicense</b></code> <code>Returns the token of a device</code></summary>

_Requires Device Authorization:_ `No` \
_Requires User Authorization:_ `Yes`

##### Body Parameters

> | name         | type     | data type | description                   |
> |--------------|----------|-----------|-------------------------------|
> | `mac`        | required | string    | The mac address of the device |
> | `user_name`  | required | string    | The name of the user          |

##### Responses

> | http code | content-type       | response                                                           |
> |-----------|--------------------|--------------------------------------------------------------------|
> | `200`     | `application/json` | `{"result": {"status": 1,"token": "1234"}}`                        |
> | `404`     | `application/json` | `{"result": {"status": 0}}`                                        |
> | `400`     | `application/json` | `{'result': {'message': "Invalid MAC address (or other errors)"}}` |
> | `401`     | `application/json` | `{'result': {'message': "Unauthorized"}}`                          |

##### Example cURL

> ```bash
> curl --location 'https://homedots.us:3425/getLicense' \
> --header 'Authorization: mySecREtToK3n' \
> --header 'Content-Type: application/json' \
> --data '{
> "mac": "00:00:00:00:00:88",
> "user_name": "adminofhomedot"
> }'
> ```

---
</details>

### APIs for User

<!-- Read Vital -->
<details>
 <summary><code>POST</code> <code><b>/readVital</b></code> <code>Returns the average values of a vital at a specific time for the device</code></summary>

_Requires Device Authorization:_ `Yes` \
_Requires User Authorization:_ `No`

##### Body Parameters

> | name              | type     | data type | description                                                                |
> |-------------------|----------|-----------|----------------------------------------------------------------------------|
> | `mac`             | required | string    | The mac address of the device                                              |
> | `vital_name`      | required | string    | Name of the vital ('heartrate', 'respiratoryrate', 'systolic', 'diastolic' |
> | `timestamp`       | optional | integer   | Start of range in UNIX (i.e. 1686885098)  Default: Current Time - 5        |
> | `start_timestamp` | optional | integer   | Same as above                                                              |
> | `end_timestamp`   | optional | integer   | End of range in UNIX   (i.e. 1686985098)  Default: Start Time + 5          |
> | `interval`        | optional | integer   | Interval in seconds to average over. Default: End - Start Time             |

##### Responses

> | http code | content-type       | response                                                                                 |
> |-----------|--------------------|------------------------------------------------------------------------------------------|
> | `200`     | `application/json` | `{"result": [80.22, 93.24, ...], ["2024-04-02T15:18:50Z", "2024-04-02T15:19:00Z", ...]}` |
> | `404`     | `application/json` | `{"message": "No data with 5 seconds of timestamp"}`                                     |
> | `400`     | `application/json` | `{'result': {'message': "Invalid MAC address (or other errors)"}}`                       |
> | `401`     | `application/json` | `{'result': {'message': "Unauthorized"}}`                                                |

##### Example cURL

> ```bash
> curl --location 'https://homedots.us:3425/readVital' \
> --header 'Authorization: 1234' \
> --header 'Content-Type: application/json' \
> --data '{
> "mac": "00:00:00:00:00:88",
> "vital_name": "heartrate",
> "timestamp": 1686893432 }'
> ```

Example
{
  "mac": "b8:27:eb:96:cb:fc",
  "version": "2020/09/06 22:58:46",
  "vital_name": "heartrate",
  "timestamp": 1686893432
 }
The vital_name are based on the schematics below
{
 "vitalMapping": {
       "occupancy": ["vitals", "occupancy"],
       "heartrate": ["vitals", "heartrate"],
       "respirationrate": ["vitals", "respiratoryrate"],
       "systolic": ["vitals", "systolic"],
       "diastolic": ["vitals", "diastolic"],
       "quality": ["vitals", "quality"],
       "movement": ["vitals", "movement"],
 }
}

---
</details>

### Example: Entering Device Authorization in Postman
#### Authorization is done with a token that corresponds the MAC address

Headers Field:

![img_1.png](assets/img_1.png)

Body and Response:

![img.png](assets/img.png)

---

### Example: Entering User Authorization in Postman
#### Authorization is done with a token that corresponds to their username

Headers Field:

<img width="836" alt="image" src="https://github.com/BedDot/API/assets/21161935/762eb050-b2cf-471a-9fc0-c9a5a553b761">

Body and Response:

<img width="841" alt="image" src="https://github.com/BedDot/API/assets/21161935/5d15371b-8cea-475b-95e3-32b8823e1272">

<img width="846" alt="image" src="https://github.com/BedDot/API/assets/21161935/d89b7434-0187-453b-999d-f7bb549da7ef">

---
