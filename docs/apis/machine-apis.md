# Machine APIs

This section contains detail about the service APIs in the Machine Master data module

* [Machines API](machine-apis.md#machines-master-api)

  These APIs includes create, update and fetch APIs. Create and Update API is used by the Administrator Portal for the Create and Update Machine functionality. Fetch APIs are used by Registration Processor to validate the Machine data received in packet to make sure the packet is generated in an authorized Machine.

* [Machine Types Master API](machine-apis.md#machine-types-master-api)

  These APIs includes Create, Update, Search and Filter API which are used by the Administrator Portal. Create and Update API is used for the Create and Update Machine Type functionality. Search API is used by the portal to fetch the list of Machine Types based on a filter criterion to display the list of Machine Types on the UI and Filter API is used by the portal to populate Machine Type Filter Drop downs on the Portal UI.

* [Machine Specification API](machine-apis.md#machine-specification)

  These APIs include Create, Update, Search and Filter API which are used by the Administrator Portal. Create and Update API is used for the Create and Update Machine Specification functionality. Search API is used by the portal to fetch the list of Machine Specification based on a filter criterion to display the list of Machine Specification on the UI and Filter API is used to populate Machine Specification Filter Drop downs on the Portal UI.

## Machines Master API

* [POST /machines](machine-apis.md#post-machines)
* [GET /machines](machine-apis.md#get-machines)
* [GET /machines/{languagecode}](machine-apis.md#get-machines-languagecode)
* [GET /machineshistory/{id}/{languagecode}/{eff\_dtimes}](machine-apis.md#get-machineshistory-id-languagecode-eff_dtimes)
* [DELETE /machines/{id}](machine-apis.md#delete-machines-id)
* [PUT /machines](machine-apis.md#put-machines)
* [POST /machines/search](machine-apis.md#post-machines-search)
* [POST /machines/filtervalues](machine-apis.md#post-machines-filtervalues)
* [GET /machines/mappedmachines/{regCenterId}](machine-apis.md#get-machines-mappedmachines-regcenterid)

### POST /machines

This service will create the list of Machines which are used in the MOSIP platform. The record needs to be created in primary and secondary language with the same ID so that it becomes active.

#### Resource URL

`POST https://{base_url}/v1/masterdata/machines`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| id | Yes | Id of the machine |  |  |
| ipAddress | No | IP Address of the machine |  |  |
| isActive | Yes | Is the machine active? |  |  |
| langCode | Yes | Language code of the machine |  |  |
| macAddress | No | Mac Address of the machine |  |  |
| machineSpecId | Yes | Machine specification Id of the machine |  |  |
| name | Yes | Name of the machine |  |  |
| publicKey | Yes | Public Key of the machine |  |  |
| serialNum | Yes | Serial number of the machine |  |  |
| validityDateTime | No | Validity date of machine |  |  |
| zoneCode | Yes | Zone code of machine |  |  |

#### Example Request

```javascript
{
  "id": "string",
  "metadata": {},
  "request": {
    "id": "string",
    "ipAddress": "192.168.0.150",
    "isActive": true,
    "langCode": "eng",
    "macAddress": "E8-6A-64-1F-27-E7",
    "machineSpecId": "1001",
    "name": "a2ml30847",
    "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAq5TnNAD1FMWWektYigmUMGw+MtNqjqLWaOZU9focDPT+nwMdw9vOs6S+Szw9Vd+zKVQ3AWkRSyfVD0qxHsPX5N6M6eS/UXvz72WF336MbbInfwzNP+uGfkprMQMt5qg21/rPSqWPU1NA9xN8lO2uPmUH4JNRBGRyvq6X1ETTDhqPsuKDwl9ciBScCMJxf/0bv2Dx7yI8lvYUaApqpoHNbBGVgDcq4f/KRZIU2kO0Ng1ESbj6D5fm0F8ZmFx3NVCKaSbBC8NUeltIRJ6+c9Csw1o23WSFTotViWeIDelsfQDq+tMmx9i9qlX3bcPZdcb7g2wm+4cywK1K5oOf3BEBxwIDAQAB",
    "regCenterId": "10005",
    "serialNum": "NM5328114630",
    "validityDateTime": "2020-10-01T05:47:13.367Z",
    "zoneCode": "CST"
  },
  "requesttime": "2018-12-10T06:12:52.994Z",
  "version": "string"
}
```

**Response Code : 200 \(OK\)**

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "responsetime": "2020-10-01T05:52:44.871Z",
  "metadata": null,
  "response": {
    "isActive": false,
    "createdBy": "110005",
    "createdDateTime": "2020-10-01T05:52:44.894Z",
    "updatedBy": null,
    "updatedDateTime": null,
    "isDeleted": null,
    "deletedDateTime": null,
    "id": "10000",
    "name": "a2ml30847",
    "serialNum": "NM5328114630",
    "macAddress": "E8-6A-64-1F-27-E7",
    "ipAddress": "192.168.0.150",
    "machineSpecId": "1001",
    "langCode": "eng",
    "validityDateTime": "2020-10-01T05:47:13.367Z"
  },
  "errors": null
}
```

**Response Code : 200 \(OK\)**

## GET /machines

This service will provides the service to fetch the complete List of machines with the machine details.

#### Resource URL

`GET https://{base_url}/v1/masterdata/machines`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |


-NA-

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "machines": [
      {
        "id": "10001",
        "name": "a2ml30846",
        "serialNum": "NM5328114630",
        "macAddress": "E8-6A-64-1F-27-E6",
        "ipAddress": "192.168.0.150",
        "machineSpecId": "1001",
        "regCenterId": "10001",
        "langCode": "eng",
        "isActive": true,
        "validityDateTime": null
      }
    ]
  }
}
```

**Response Code : 200 \(OK\)**

### GET /machines/{languagecode}

This service will provides the service to fetch the List of machines with the machine details based on the language.

#### Resource URL

`GET https://{base_url}/v1/masterdata/machines/{lang_Code}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| languagecode | Yes | Machine Languge Code |  |  |

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "machines": [
      {
        "id": "10001",
        "name": "a2ml30846",
        "serialNum": "NM5328114630",
        "macAddress": "E8-6A-64-1F-27-E6",
        "ipAddress": "192.168.0.150",
        "machineSpecId": "1001",
        "regCenterId": "10001",
        "langCode": "eng",
        "isActive": true,
        "validityDateTime": null
      }
    ]
  }
}
```

**Response Code : 200 \(OK\)**

### GET /machineshistory/{id}/{languagecode}/{eff\_dtimes}

This service will provides the service will verify if a machine \(id\) was active at a particular time \(eff\_dtime\).

#### Resource URL

`GET https://{base_url}/v1/masterdata/machineshistories/{id}/{lang_code}/{eff_dtimes}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| ID | Yes | Machine History Id |  |  |
| languagecode | Yes | Language code for the Machine |  |  |
| eff\_dtimes | Yes | Effective Date and Time of the Machine |  |  |

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "machineHistoryDetails": [
      {
        "id": "10001",
        "name": "a2ml30846",
        "serialNum": "NM5328114630",
        "ipAddress": "192.168.0.150",
        "macAddress": "E8-6A-64-1F-27-E6",
        "machineSpecId": "1001",
        "langCode": "eng",
        "isActive": true,
        "effectDateTime": "2020-10-01T04:21:44.587Z",
        "validityDateTime": null
      }
    ]
  }
}
```

**Response Code : 200 \(OK\)**

### DELETE /machines/{id}

This service will delete the machines.

#### Resource URL

`DELETE https://dev.mosip.net/v1/masterdata/machines/decommission/{id}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| machineId | Yes | The machineId |  |  |

#### Example Response

```javascript
{
  "id": null,
  "version": null,
  "responsetime": "2020-10-04T17:14:36.127Z",
  "metadata": null,
  "response": {
    "id": "10001"
  },
  "errors": null
}
```

**Response Code : 200 \(OK\)**

### PUT /machines

This service will update existing machines.

#### Resource URL

`PUT /machines`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| id | Yes | Id of the machine |  |  |
| name | Yes | Name of the machine |  |  |
| machineSpecId | Yes | Machine specification Id of the machine |  |  |
| serialNum | Yes | Serial number of the machine |  |  |
| langCode | Yes | Language code of the machine |  |  |
| ipAddress | No | Ip Address of the machine |  |  |
| isActive | Yes | Is the machine active? |  |  |
| validityDateTime | Yes | Validity date of machine |  |  |
| zoneCode | Yes | Zone code of machine |  |  |

#### Example Request

```javascript
{
  "id": "string",
  "metadata": {},
  "request": {
    "id": "10000",
    "ipAddress": "192.168.0.150",
    "isActive": true,
    "langCode": "ara",
    "macAddress": "E8-6A-64-1F-27-E7",
    "machineSpecId": "1001",
    "name": "a2ml30847",
    "regCenterId": "10005",
    "serialNum": "string",
    "validityDateTime": "2020-10-01T05:47:13.367Z",
    "zoneCode": "BSN"
  },
  "requesttime": "2018-12-10T06:12:52.994Z",
  "version": "string"
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "responsetime": "2020-10-01T06:04:48.156Z",
  "metadata": null,
  "response": {
    "isActive": true,
    "createdBy": "110005",
    "createdDateTime": "2020-10-01T05:52:44.894Z",
    "updatedBy": "110005",
    "updatedDateTime": "2020-10-01T06:04:48.176Z",
    "isDeleted": null,
    "deletedDateTime": null,
    "id": "10000",
    "name": "a2ml30847",
    "serialNum": "string",
    "macAddress": "E8-6A-64-1F-27-E7",
    "ipAddress": "192.168.0.150",
    "machineSpecId": "1001",
    "langCode": "ara",
    "validityDateTime": "2020-10-01T05:47:13.367Z"
  },
  "errors": null
}
```

**Response Code : 200 \(OK\)**

#### Failure Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": null
}
```

**Response Code : 200 \(OK\)**

#### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| KER-MSD-029 | Error occured while fetching Machines | Fetch Issue |
| KER-MSD-063 | Error occurred while inserting Machine details | Insertion Issue |
| KER-MSD-030 | Machine not Found | Data Not Found |
| KER-MSD-087 | Error occurred while updating Machine details | Update Issue |
| KER-MSD-088 | Error occurred while deleting Machine details | Deletion Issue |
| KER-MSD-148 | Cannot delete as dependency found | Deletion Issue because of dependency |

### POST /machines/search

This service is for the machine search functionality. All the filter parameters are passed and the machines are searched and the matching results are returned.

#### Resource URL

`POST /machines/search`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| filters | No | Array of the filter applied. In case of "list" screen, this array will be empty | -NA- |  |
| columnName | No | The column name in the JSON response | -NA- |  |
| type | No | The value have to be in \["contains","equals",”startsWith”,"between"\] | -NA- |  |
| value | No | Value or id selected in the filter by the end user | -NA- |  |
| fromValue | No | If the type is "between", this field is the value of the start range | -NA- |  |
| toValue | No | If the type is "between", this field is the value of the end range | -NA- |  |
| languagecode | Yes | Language code in Language code in ISO 639-2 format |  |  |
| sort | No | This is an array of the sort field and type |  |  |
| sortfield | The field on which the sort is applied |  | modifiedDate |  |
| sorttype | This should be either of \['ASC','DESC'\] |  | ASC |  |
| pagination | The pagination parameter object |  |  |  |
| pageStart | This is the start index | 0 | 0 |  |
| pageFetch | This is the amount of records to be fetched | 10 | 10 |  |

#### Filter Values

Please find the filter columns used in search 1\) name 2\) id 3\) macAddress 4\) serialNum 5\) machineSpecId 6\) ipAddress 7\) langCode 8\) regCenterId

#### Example Request

```javascript
{
  "id": "string",
  "metadata": {},
  "request": {
    "filters": [
      {
        "columnName": "id",
        "fromValue": null,
        "toValue": null,
        "type": "equals",
        "value": "10000"
      }
    ],
    "languageCode": "ara",
    "pagination": {
      "pageFetch": 10,
      "pageStart": 0
    },
    "sort": [
      {
        "sortField": "name",
        "sortType": "ASC"
      }
    ]
  },
  "requesttime": "2018-12-10T06:12:52.994Z",
  "version": "string"
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "responsetime": "2020-10-01T06:08:35.133Z",
  "metadata": null,
  "response": {
    "fromRecord": 1,
    "toRecord": 1,
    "totalRecord": 1,
    "data": [
      {
        "isActive": true,
        "createdBy": "110005",
        "createdDateTime": "2020-10-01T05:54:02.667Z",
        "updatedBy": "110005",
        "updatedDateTime": "2020-10-01T06:08:20.040Z",
        "isDeleted": null,
        "deletedDateTime": null,
        "id": "10000",
        "name": "a2ml30847",
        "serialNum": "string",
        "macAddress": "E8-6A-64-1F-27-E7",
        "ipAddress": "192.168.0.150",
        "machineSpecId": "1001",
        "langCode": "ara",
        "validityDateTime": "2020-10-01T05:47:13.367Z",
        "regCenterId": "10005",
        "zoneCode": "BSN",
        "zone": "بنسليمان",
        "machineTypeName": "الحاسوب",
        "mapStatus": "مركز مهدية"
      }
    ]
  },
  "errors": null
}
```

**Response Code : 200 \(OK\)**

### POST /machines/filtervalues

This service returns the filter values which are required in the dropdown entries of the filter screen.

#### Resource URL

`POST /machines/filtervalues`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| filters | No | Array of the filter applied. In case of "list" screen, this array will be empty | -NA- |  |
| columnName | No | The column name in the JSON response | -NA- |  |
| type | No | The value have to be in \["unique","all"\] | unique | unique |
| languagecode | Yes | Language code in Language code in ISO 639-2 format |  |  |

#### Example Request

```javascript
{
  "id": "string",
  "metadata": {},
  "request": {
    "filters": [
      {
        "columnName": "zoneCode",
        "text": "S",
        "type": "unique"
      }
    ],
    "languageCode": "eng"
  },
  "requesttime": "2018-12-10T06:12:52.994Z",
  "version": "string"
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "responsetime": "2020-10-01T06:14:25.624Z",
  "metadata": null,
  "response": {
    "filters": [
      {
        "fieldID": "zoneCode",
        "fieldValue": "BSN",
        "fieldCode": "10000"
      },
      {
        "fieldID": "zoneCode",
        "fieldValue": "CST",
        "fieldCode": "10005"
      }
    ]
  },
  "errors": null
}
```

**Response Code : 200 \(OK\)**

### GET /machines/mappedmachines/{regCenterId}

This service will fetch all the machines mapped to a registration center.

#### Resource URL

`POST https://{base_url}/v1/masterdata/machines/mappedmachines/{reg_center_id}?direction=DESC&orderBy={field_name}&pageNumber=1&pageSize=10`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Query Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| direction | No | ASC or DESC |  |  |
| orderBy | No | Column Name |  |  |
| pageNumber | No | Page Number | 1 |  |
| pageSize | No | Page Size | 10 |  |

#### Request Body

-NA-

#### Response Body

**Success Response**

```javascript
{
  "id": null,
  "version": null,
  "responsetime": "2020-10-04T17:34:33.334Z",
  "metadata": null,
  "response": {
    "pageNo": 1,
    "pageSize": 10,
    "sort": {
      "sorted": true,
      "unsorted": false
    },
    "totalItems": 1,
    "totalPages": 1,
    "data": [
      {
        "isActive": true,
        "createdBy": "superadmin",
        "createdDateTime": "2020-10-01T04:21:44.266Z",
        "updatedBy": null,
        "updatedDateTime": null,
        "isDeleted": null,
        "deletedDateTime": null,
        "regCentId": "10002",
        "id": "10032",
        "name": "a2ml29106",
        "serialNum": "FB5962911665",
        "macAddress": "38-BA-F8-53-C7-8F",
        "ipAddress": "192.168.0.358",
        "machineSpecId": "1001",
        "langCode": "fra"
      }
    ]
  },
  "errors": null
}
```

**Response Code : 200 \(OK\)**

**Failure Response**

```javascript
{
  "id": null,
  "version": null,
  "responsetime": "2020-10-04T17:36:11.928Z",
  "metadata": null,
  "response": null,
  "errors": [
    {
      "errorCode": "KER-MSD-030",
      "message": "Machine not Found"
    }
  ]
}
```

## Machine Types Master API

* [POST /machinetypes](machine-apis.md#post-machinetypes)
* [PUT /machinetypes](machine-apis.md#put-machinetypes)
* [GET /machinetypes](machine-apis.md#get-machinetypes)
* [GET /machinetypes/{languagecode}](machine-apis.md#get-machinetypes-languagecodee)
* [POST /machinetypes/search](machine-apis.md#post-machinetypes-search)
* [POST /machinetypes/filtervalues](machine-apis.md#post-machinetypes-filtervalues)

### POST /machinetypes

This service will create the list of Machine types which are used in the MOSIP platform.

#### Resource URL

`POST /machinetypes`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| machinetypecode | Yes | Code of the machine type |  |  |
| machinename | Yes | Name of the machine type |  |  |
| description | Yes | Description of the machine type |  |  |
| languagecode | Yes | Language code of the machine type |  |  |
| isactive | Yes | Is the machine type active? |  |  |

#### Example Request

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "code": "string",
    "description": "string",
    "isActive": true,
    "langCode": "string",
    "name": "string"
  }
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "code": "string",
    "langCode": "string"
  }
}
```

**Response Code : 200 \(OK\)**

**Failure details**

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| KER-MSD-061 | Error occurred while inserting Machine Type details | Insertion Issue |

### PUT /machinetypes

This service will update the list of Machine types which are used in the MOSIP platform.

#### Resource URL

`PUT /machinetypes`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| machinetypecode | Yes | Code of the machine type |  |  |
| machinename | Yes | Name of the machine type |  |  |
| description | Yes | Description of the machine type |  |  |
| languagecode | Yes | Language code of the machine type |  |  |
| isactive | Yes | Is the machine type active? |  |  |

#### Example Request

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "code": "123",
    "description": "test123",
    "isActive": false,
    "langCode": "eng",
    "name": "test"
  }
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "code": "123",
    "langCode": "eng"
  }
}
```

#### Response codes

**Response Code : 200 \(OK\)**

**Failure details**

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| KER-MSD-063 | Machine Type Not Found | Data Not Found |
| KER-MSD-064 | Error occurred while updating Machine Type details | updation Issue |

### GET /machinetypes

This service will provides the service to fetch the complete List of machine types with the machine details.

#### Resource URL

`GET /machinetypes`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |


-NA-

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":{
    "machinetypes": [
      { 
        "machinetypecode":"string",
        "machinename":"string",    
        "description":"string",
        "languagecode":"boolean",
        "isactive":"string" 
      }, 
      { 
        "machinetypecode":"string",
        "machinename":"string",    
        "description":"string",
        "languagecode":"boolean",
        "isactive":"string" 
      }
    ]
  }
}
```

**Response Code : 200 \(OK\)**

### GET /machinetypes/{languagecode}

This service will provides the service to fetch the List of machines with the machine details based on the language code.

#### Resource URL

`GET /machinetypes/{languagecode}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |


-NA-

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":  {
    "machines": [
      { 
        "machinetypecode":"string",
        "machinename":"string",    
        "description":"string",
        "languagecode":"boolean",
        "isactive":"string" 
      }, 
      { 
        "machinetypecode":"string",
        "machinename":"string",    
        "description":"string",
        "languagecode":"boolean",
        "isactive":"string" 
      }
    ]
  }
}
```

**Response Code : 200 \(OK\)**

#### Failure Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  null
 }
```

**Response Code : 200 \(OK\)**

#### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| KER-MSD-061 | Error occurred while inserting Machine Type details | Insertion Issue |
| KER-MSD-062 | Error occurred while fetching Machine Type details | Fetch Issue |
| KER-MSD-063 | Machine Type Not Found | Data Not Found |

### POST /machinetypes/search

This service is for the machine type search functionality. All the filter parameters are passed and the machines types are searched and the matching results are returned.

#### Resource URL

`POST /machinetypes/search`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| filters | No | Array of the filter applied. In case of "list" screen, this array will be empty | -NA- |  |
| columnName | No | The column name in the JSON response | -NA- |  |
| type | No | The value have to be in \["contains","equals",”startsWith”,"between"\] | -NA- |  |
| value | No | Value or id selected in the filter by the end user | -NA- |  |
| fromValue | No | If the type is "between", this field is the value of the start range | -NA- |  |
| toValue | No | If the type is "between", this field is the value of the end range | -NA- |  |
| languagecode | Yes | Language code in Language code in ISO 639-2 format |  |  |
| sort | No | This is an array of the sort field and type |  |  |
| sortfield | The field on which the sort is applied |  | modifiedDate |  |
| sorttype | This should be either of \['ASC','DESC'\] |  | ASC |  |
| pagination | The pagination parameter object |  |  |  |
| pageStart | This is the start index | 0 | 10 |  |
| pageFetch | This is the amount of records to be fetched | 10 | 10 |  |

#### Filter Values

Please find the filter columns used in search 1\) name 2\) status

#### Example Request

```javascript
{
  "id": "string",
  "metadata": {},
  "requesttime": "2018-12-10T06:12:52.994Z",
  "version": "string",
  "request": {
    "filters" : [
      {
        "columnName": "",
        "type": "in",
        "value": "",  
        "fromValue": "",    
        "toValue": ""
      }
    ],
    "sort":[
      {
        "sortfield":"string",
        "sorttype":"ASC"
      }
    ],
    "pagination":{
      "pageStart":"number",
      "pageFetch":"number"
    },
    "languageCode":""    
  }
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "machineTypes": [
      {
        "code": "string",
        "description": "string",
        "isActive": true,
        "langCode": "string",
        "name": "string"  
      }
    ],
    "fromRecord" : "number",
    "toRecord":"number",
    "totalRecord":"number"
  }
}
```

**Response Code : 200 \(OK\)**

### POST /machinetypes/filtervalues

This service returns the filter values which are required in the dropdown entries of the filter screen.

#### Resource URL

`POST /machinetypes/filtervalues`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| filters | No | Array of the filter applied. In case of "list" screen, this array will be empty | -NA- |  |
| columnName | No | The column name in the JSON response | -NA- |  |
| type | No | The value have to be in \["unique","all"\] | unique | unique |
| languagecode | Yes | Language code in Language code in ISO 639-2 format |  |  |

#### Example Request

```javascript
{
  "id": "string",
  "metadata": {},
  "requesttime": "2018-12-10T06:12:52.994Z",
  "version": "string"
  "request": {
    "filters" : [
      {
        "columnName": ""
        "type": "unique"
      }
    ],
    "languageCode": "string",
  }
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "filters": [
      {
        "fieldID": "string",
        "fieldValue": "string"
      }
    ]
  }
}
```

**Response Code : 200 \(OK\)**

## Machine Specifications

* [POST /machinespecifications](machine-apis.md#post-machinespecifications)
* [PUT /machinespecifications](machine-apis.md#put-machinespecifications)
* [DELETE /machinespecifications/{id}](machine-apis.md#delete-machinespecifications-id)
* [GET /machinespecifications](machine-apis.md#get-machinespecifications)
* [GET /machinespecifications/{lang\_code}](machine-apis.md#get-machinespecifications-lang_code)
* [POST /machinespecifications/search](machine-apis.md#post-machinespecifications-search)
* [POST /machinespecifications/filtervalues](machine-apis.md#post-machinespecifications-filtervalues)

### POST /machinespecifications

This service will create a Machine Specification which are used in the MOSIP platform.

#### Resource URL

`POST /machinespecifications`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| id | Yes | ID of the Machine Specification |  |  |
| name | Yes | Name of the machine Specification |  |  |
| brand | Yes | Brand of the machine specification |  |  |
| model | Yes | Model of the machine specification |  |  |
| mtyp\_code | Yes | Machine type code of the machine specification |  |  |
| min\_driver\_ver | Yes | Minimum driver version required for the machine specification |  |  |
| descr | Yes | Description of the machine specification |  |  |
| lang\_code | Yes | Language of the machine specification |  |  |
| is\_active | Yes | Is the Machine Specification active |  |  |

#### Example Request

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "brand": "string",
    "description": "string",
    "id": "string",
    "isActive": true,
    "langCode": "string",
    "machineTypeCode": "string",
    "minDriverversion": "string",
    "model": "string",
    "name": "string"
  }
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "id": "string"
  }
}
```

**Response Code : 200 \(OK\)**

### PUT /machinespecifications

This service will update a Machine Specification which are used in the MOSIP platform.

#### Resource URL

`PUT /machinespecifications`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| id | Yes | ID of the Machine Specification |  |  |
| lang\_code | Yes | Language code of the Machine Specification |  |  |

#### Example Request

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
    "brand": "string",
    "description": "string",
    "id": "string",
    "isActive": true,
    "langCode": "string",
    "machineTypeCode": "string",
    "minDriverversion": "string",
    "model": "string",
    "name": "string"
  }
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":  {
    "id": "string"
  }
}
```

**Response Code : 200 \(OK\)**

### DELETE /machinespecifications/{id}

This service deletes a Machine Specification from the Machine Specifications master module.

#### Resource URL

`DELETE /machinespecifications/{id}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| id | Yes | ID of the Machine Specification |  |  |

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":  {
    "id": "string"
  }
}
```

### GET /machinespecifications

This service will provides the list of all Machine Specifications in all languages.

#### Resource URL

`GET /machinespecifications`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |


-NA-

#### Example Request

```javascript
-NA-
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":  {
    "id":"KJDS9",
    "name":"Laptop",
    "brand":"Hewlett Packard",
    "model":"L34-324",
    "mtyp_code":"GEW8",
    "min_driver_ver":"1.4",
    "descr":"This is a medium configuration",
    "lang_code":"eng",
    "is_active":true
  }
}
```

### GET /machinespecifications/{lang\_code}

This service will provides the list of all Machine Specifications in a specific language.

#### Resource URL

`GET /machinespecifications/{lang_code}`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |


-NA-

#### Example Request

```javascript
-NA-
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":   {
    "id":"KJDS9",
    "name":"Laptop",
    "brand":"Hewlett Packard",
    "model":"L34-324",
    "mtyp_code":"GEW8",
    "min_driver_ver":"1.4",
    "descr":"This is a medium configuration",
    "lang_code":"eng",
    "is_active":true
  }
}
```

**Response Code : 200 \(OK\)**

#### Failure Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":   null
}
```

**Response Code : 200 \(OK\)**

#### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| KER-MSD-062 | Error occurred while inserting Machine Specification details | Insertion Issue |
| KER-MSD-117 | Machine Specification not Found | Data Not Found |
| KER-MSD-085 | Error occurred while updating Machine Specification details | Update Issue |
| KER-MSD-086 | Error occurred while deleting Machine Specification details | Deletion Issue |
| KER-MSD-122 | Cannot delete dependency found | Deletion Issue because of dependency |
| KER-MSD-087 | Error occurred while fetching Machine Specification details | Fetch Issue |

### POST /machinespecifications/search

This service is for the machine specifications search functionality. All the filter parameters are passed and the machines specifications are searched and the matching results are returned.

#### Resource URL

`POST /machinespecifications/search`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| filters | No | Array of the filter applied. In case of "list" screen, this array will be empty | -NA- |  |
| columnName | No | The column name in the JSON response | -NA- |  |
| type | No | The value have to be in \["contains","equals",”startsWith”,"between"\] | -NA- |  |
| value | No | Value or id selected in the filter by the end user | -NA- |  |
| fromValue | No | If the type is "between", this field is the value of the start range | -NA- |  |
| toValue | No | If the type is "between", this field is the value of the end range | -NA- |  |
| languagecode | Yes | Language code in Language code in ISO 639-2 format |  |  |
| sort | No | This is an array of the sort field and type |  |  |
| sortfield | The field on which the sort is applied |  | modifiedDate |  |
| sorttype | This should be either of \['ASC','DESC'\] |  | ASC |  |
| pagination | The pagination parameter object |  |  |  |
| pageStart | This is the start index | 0 | 10 |  |
| pageFetch | This is the amount of records to be fetched | 10 | 10 |  |

#### Filter Values

Please find the filter columns used in search 1\) name 2\) isActive 3\) brand 4\) model 5\) machineTypeName

#### Example Request

```javascript
{
  "id": "string",
  "metadata": {},
  "requesttime": "2018-12-10T06:12:52.994Z",
  "version": "string",
  "request": {
    "filters" : [
      {
        "columnName": "",
        "type": "in",
        "value": "",  
        "fromValue": "",  
        "toValue": ""
      }
    ],
    "sort":[
      {
        "sortfield":"string",
        "sorttype":"ASC"
      }
    ],
    "pagination":{
      "pageStart":"number",
      "pageFetch":"number"
    },
    "languageCode":""    
  }
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "machineSpecifications": [
      {
        "brand": "string",
        "description": "string",
        "id": "string",
        "isActive": true,
        "langCode": "string",
        "machineTypeCode": "string",
        "minDriverversion": "string",
        "model": "string",
        "name": "string"  
      }
    ],
    "fromRecord" : "number",
    "toRecord":"number",
    "totalRecord":"number"
  }
}
```

**Response Code : 200 \(OK\)**

### POST /machinespecifications/filtervalues

This service returns the filter values which are required in the dropdown entries of the filter screen.

#### Resource URL

`POST /machinespecifications/filtervalues`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| filters | No | Array of the filter applied. In case of "list" screen, this array will be empty | -NA- |  |
| columnName | No | The column name in the JSON response | -NA- |  |
| type | No | The value have to be in \["unique","all"\] | unique | unique |
| languagecode | Yes | Language code in Language code in ISO 639-2 format |  |  |

#### Example Request

```javascript
{
    "id": "string",
    "metadata": {},
    "requesttime": "2018-12-10T06:12:52.994Z",
    "version": "string"
    "request": {
        "filters" : [
            {
                "columnName": ""
                "type": "unique"
            }
        ],
        "languageCode": "string",
    }
}
```

#### Example Response

```javascript
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "filters": [
    {
        "fieldCode": "string",
        "fieldID": "string",
        "fieldValue": "string"
    }
   ]
 }
}
```

