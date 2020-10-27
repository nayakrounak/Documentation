# Zone APIs

This section details about the service APIs for the Zones

## Zone Master API

* [GET /zones/authorize/{rid}](zone-apis.md#get-zones-authorize-rid)
* [GET /zones/hierarchy/{langCode}](zone-apis.md#get-zones-hierarchy-langcode)
* [GET /zones/leafs/{langCode}](zone-apis.md#get-zones-leafs-langcode)
* [GET /zones/zonename](zone-apis.md#get-zones-zonename)

### GET /zones/authorize/{rid}

This service will verify if the logged-in user is authorized to view the RID history.

#### Resource URL

`GET /zones/authorize/{rid}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| rid | yes | rid for which user wants to know the history |  |  |

#### Example Response

```javascript
{
  "id": null,
  "version": null,
  "responsetime": "2020-07-08T06:08:26.654Z",
  "metadata": null,
  "response": true,
  "errors": null
}
```

### GET /zones/hierarchy/{langCode}

This service will fetch the logged-in user zone hierarchy.

#### Resource URL

`GET /zones/hierarchy/{langCode}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| langCode | yes | user language code |  |  |

#### Example Response

```javascript
{
  "id": null,
  "version": null,
  "responsetime": "2019-11-18T06:04:39.194Z",
  "metadata": null,
  "response": [
    {
      "isActive": true,
      "createdBy": "superadmin",
      "createdDateTime": "2019-08-27T12:28:10.549Z",
      "updatedBy": null,
      "updatedDateTime": null,
      "isDeleted": null,
      "deletedDateTime": null,
      "code": "STT",
      "langCode": "eng",
      "name": "Settat",
      "hierarchyLevel": 3,
      "hierarchyName": "Province",
      "parentZoneCode": "CST",
      "hierarchyPath": "MOR/NTH/CST/STT"
    }
  ],
  "errors": []
}
```

### GET /zones/leafs/{langCode}

This service will fetch the logged-in user zone hierarchy leaf zones.

#### Resource URL

`GET /zones/leafs/{langCode}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| langCode | yes | user language code |  |  |

#### Example Response

```javascript
{
  "id": null,
  "version": null,
  "responsetime": "2019-11-18T06:09:15.321Z",
  "metadata": null,
  "response": [
    {
      "isActive": true,
      "createdBy": "superadmin",
      "createdDateTime": "2019-08-27T12:28:10.549Z",
      "updatedBy": null,
      "updatedDateTime": null,
      "isDeleted": null,
      "deletedDateTime": null,
      "code": "BSN",
      "langCode": "eng",
      "name": "Benslimane",
      "hierarchyLevel": 3,
      "hierarchyName": "Province",
      "parentZoneCode": "CST",
      "hierarchyPath": "MOR/NTH/CST/BSN"
    }
  ],
  "errors": []
}
```

### GET /zones/zonename

This service will fetch the logged-in user zone hierarchy leaf zones.

#### Resource URL

`GET /zones/zonename`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| langCode | yes | user language code |  |  |
| userID | yes | user id |  |  |

#### Example Response

```javascript
{
  "id": null,
  "version": null,
  "responsetime": "2019-11-18T06:22:22.475Z",
  "metadata": null,
  "response": {
    "zoneName": "Casablanca-Settat"
  },
  "errors": []
}
```

## Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| KER-MSD-337 | Error occured while fetching zone | Fetch Issue |
| KER-MSD-339 | No zone found for the logged-in user | Data Not Found |
| KER-MSD-338 | Error Occured while fetching zone of the user | Fetch Issue |
| KER-MSD-391 | Entity for user ID specified Not Found | Data Not Found |
| KER-MSD-392 | Entity for Zone Code of user ID specified Not Found | Data Not Found |
| KER-MSD-393 | Internal Server Error | Dependency issue |

