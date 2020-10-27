# Registration Processor APIs

This section details about the service APIs in the Registration-Processor modules

1. [Packet receiver API](registration-processor-apis.md#1-packet-receiver-api)
2. [Registration status API](registration-processor-apis.md#2-registration-status-api)
3. [Sync Registration API](registration-processor-apis.md#3-sync-registration-api)
4. [Manual Adjudication APIs](registration-processor-apis.md#4-manual-adjudication-apis)
5. [Bio Dedupe API](registration-processor-apis.md#5-bio-dedupe-api)
6. [Packet Generator API](registration-processor-apis.md#6-packet-generator-api)
7. [Packet Uploader API](registration-processor-apis.md#7-packet-uploader-api)
8. [Request Handler API](registration-processor-apis.md#8-request-handler-api)
9. [Registration Transaction API](registration-processor-apis.md#9-registration-transaction-api)
10. [UIN Card API](registration-processor-apis.md#10-uin-card-api)
11. [Lost UIN Or RID API](registration-processor-apis.md#11-lost-uin-or-rid-api)
12. [Update UIN API](registration-processor-apis.md#12-update-uin-api)

## 1 Packet Receiver API

This API receives registration packet from reg-client. Before moving packet to landing zone virus scan is performed and then trustworthiness of the packet is validated using hash value and size.

`POST /registrationprocessor/v1/packetreceiver/registrationpackets`

### Resource URL

`https://{base_url}/registrationprocessor/v1/packetreceiver/registrationpackets`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | MULTIPART |
| Response format | JSON |
| Requires Authentication | Yes |

### Request Path Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| MultipartFile | Yes | The encrypted zip file |  |

### Request

![](../.gitbook/assets/packet_receiver_sample_input.PNG)

### Response

#### Response Header

**Response-Signature** = `<the response signature>`

#### Success response

**Status Code**: 200

**Description**: Packet is in PACKET\_RECEIVED status

```javascript
{
    "id" : "mosip.registration.packet",
    "version" : "1.0",
    "responsetime" : "2019-02-02T06:12:25.288Z",
    "response" : {
        "status" : "Packet is in PACKET_RECEIVED status"
    },
    "errors": null
}
```

#### Failure response

**Status Code**: 200

**Description**: The request received is a duplicate request to upload a Packet

```javascript
{
  "id" : "mosip.registration.packet",
  "version" : "1.0",
  "responsetime": "2019-02-02T06:12:25.288Z",
  "response": null,
  "errors" : [{
        "errorcode": "RPR-PKR-005",
        "message": "The request received is a duplicate request to upload a Packet"
    }]
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-PKR-005 | Duplicate Request Received | Duplicate Packet |
| RPR-PKR-006 | Packet Not Available in Request | Packet missing |
| RPR-PKR-003 | Invalid Packet Format | Format doesnot match configuration |
| RPR-PKR-002 | Invalid Packet Size | Size more then configured |
| RPR-RGS-001 | Unable to Access Registration Table | Database error |
| RPR-SYS-005 | Timeout Error | Timeout Error |
| RPR-SYS-001 | Unexpected exception | Unexpected exception |
| RPR-PKR-004 | Packet Validation Failed | Packet Validation Failed |
| RPR-AUT-01 | Invalid Token Present | Invalid Token Present |
| RPR-AUT-02 | Access Denied | Access Denied |
| RPR-DBE-001 | Data integrity violation exception | Data integrity violation exception |
| RPR-PKR-001 | Packet Not Found in Sync Table | Packet Not Found in Sync Table |
| RPR-PKR-007 | Unknown Exception Found | Unknown Exception Found |
| RPR-PKR-013 | Packet Size is Not Matching | Packet Size is Not Matching |
| RPR-PKR-010 | Virus was Found in Packet | Virus was Found in Packet |
| RPR-PKR-008 | Virus Scan Service is Not Responding | Virus Scan Service is Not Responding |
| RPR-PKR-009 | Packet HashSequence did not match | Packet HashSequence did not match |

## 2 Registration Status API

This API return the registration current status for list of registration ids.

`POST /registrationprocessor/v1/registrationstatus/search`

### Resource URL

`https://{base_url}/registrationprocessor/v1/registrationstatus/search`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | JSON |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| registrationIds | Yes | List of registration ids |  |

### Request

```javascript
{
  "id" : "mosip.registration.status",
  "version" : "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request" : [
    {
        "registrationId" : "2018701130000410092012345678"
    },
    {
        "registrationId" : "2018701130000410092012345678"
    }
  ]
}
```

### Response

**Scenario**: Record Found

**Status Code**: 200

**Description**: Successfully retrieved information

```javascript
{
  "id" : "mosip.registration.status",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : [
    {
      "registrationId": "2018701130000410092012345678",
      "statusCode": "PROCESSING"
    },
    {
      "registrationId": "2018701130000410092018110735",
      "statusCode": "PROCESSED"
    }
  ],
  "errors": null
}
```

**Scenario**: Record not found

**Status Code**: 200

**Description**: Successfully retrieved information

```javascript
{
  "id": "mosip.registration.status",
  "version": "1.0",
  "responsetime": "2019-12-06T04:16:07.070Z",
  "response": [],
  "errors": [
    {
      "registrationId": "10014100180046820190619064012",
      "errorCode": "RPR-RGS-031",
      "errorMessage": "RID Not Found"
    },
    {
      "registrationId": "10006100420001120190613130943",
      "errorCode": "RPR-RGS-031",
      "errorMessage": "RID Not Found"
    }
  ]
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-AUT-002 | Access Denied | Access Denied for the role |
| RPR-RGS-001 | Unable to Access Registration Table | Unable to Access Registration Table |
| RPR-RGS-016 | JSON Mapping Failed | JSON Mapping Failed |
| RPR-RGS-017 | JSON Parsing Failed | JSON Parsing Failed |
| RPR-SYS-002 | Bad Gateway | Bad Gateway |
| RPR-DBE-001 | Data integrity violation exception | Data integrity violation exception |
| RPR-AUT-01 | Invalid Token Present | Invalid Token Present |
| RPR-RGS-015 | Invalid Request Value - Input Data is Incorrect | Invalid Request Value - Input Data is Incorrect |
| RPR-RGS-031 | RID Not Found | RID Not Found |

## 3 Sync registration API

The registration ids has to be synced with server before uploading packet to landing zone. This API is used to sync registration ids.

`POST /registrationprocessor/v1/registrationstatus/sync`

### Resource URL

`https://{base_url}/registrationprocessor/v1/registrationstatus/sync`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | JSON |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| id | Yes | the id for sync | mosip.registration.sync |
| version | Yes | the version for sync | 1.0 |
| requesttime | Yes | the requesttime for sync | 2019-02-14T12:40:59.768Z |
| request | Yes | the request object | 1.0 |
| registrationId | Yes | the registration id | 80006444440002520181208094000 |
| registrationType | Yes | the type of the registration | NEW, UPDATE, LOST, ACTIVATE, DEACTIVATE, RES\_UPDATE |
| packetHashValue | Yes | the hash value of the encrypted packet | D7C87DC5D3A759D77433B02B80435CFAB5087F1A942543F51A5075BC441BF7EB |
| packetSize | Yes | size of encrypted packet in bytes | 5242880 |
| supervisorStatus | Yes | supervisor decision | APPROVED, REJECTED |
| supervisorComment | No | supervisor comments | rejected because of error |
| optionalValues | No | additional values to be passed during sync | key, value pair |
| langCode | Yes | language code used | eng or ara |

### Request Header

**Center-Machine-RefId** = `10011_10011`

**timestamp** = `2019-02-14T12:40:59.768Z`

### Request

```javascript
// NOTE : the actual request will be an encrypted json. This is an example of decrypted request json.
{
  "id": "mosip.registration.sync",
  "version": "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request": [
    {
      "registrationId": "80006444440002520181208094000",
      "registrationType": "NEW",
      "packetHashValue": "D7C87DC5D3A759D77433B02B80435CFAB5087F1A942543F51A5075BC441BF7EB",
      "packetSize": 5242880,
      "supervisorStatus": "APPROVED",
      "supervisorComment": "Approved, all good",
      "langCode": "eng",
      "optionalValues": [
        {
          "key": "CNIE",
          "value": "122223456"
        }
      ]
    },
    {
      "registrationId": "10011100110002520181208094000",
      "registrationType": "UPDATE",
      "packetHashValue": "D7C87DC5D3A759D77433B02B80435CFAB5087F1A942543F51A5075BC441BF7EB",
      "packetSize": 4242880,
      "supervisorStatus": "REJECTED",
      "supervisorComment": "Rejected due to error",
      "langCode": "eng",
      "optionalValues": [
        {
          "key": "CNIE",
          "value": "3456789o"
        }
      ]
    }
  ]
}
```

### Response

#### Response Header

**Response-Signature** = `<the response signature>`

#### Success response

**Response Code**: 200

**Description**: Successfully synced

```javascript
{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "errors": null,
  "response" : [
    {
      "registrationId": "80006444440002520181208094000",
      "status": "SUCCESS"
    },
    {
      "registrationId": "10011100110002520181208094000",
      "status": "SUCCESS"
    }
  ]
}
```

#### Failure response

```javascript
// response 1 : decryption failed
{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response": null,
  "errors" : [
    {
      "status": "FAILURE",
      "errorCode": "RPR-RGS-001",
      "errorMessage": "Decryption failed"
    }
  ]
}

// response 2 : validation failed
{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response": null,
  "errors" : [
    {
      "registrationId": "1234575",
      "status": "FAILURE",
      "errorCode": "RPR-RGS-009",
      "errorMessage": "RegistrationId Length Must Be 29"
    },
    {
      "registrationId": "12345678901234567890123456789",
      "status": "FAILURE",
      "errorCode": "RPR-RGS-007",
      "errorMessage": "Invalid Time Stamp Found in RegistrationId"
    },
    {
      "registrationId": "27847657360002520181208183052",
      "status": "FAILURE",
      "errorCode": "RPR-RGS-012",
      "errorMessage": "Parent RegistrationId Length Must Be 29"
    }
  ]
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-AUT-002 | Access Denied | Access Denied for the role |
| RPR-RGS-001 | Unable to Access Registration Table | Unable to Access Registration Table |
| RPR-RGS-016 | JSON Mapping Failed | JSON Mapping Failed |
| RPR-RGS-017 | JSON Parsing Failed | JSON Parsing Failed |
| RPR-SYS-002 | Bad Gateway | Bad Gateway |
| RPR-DBE-001 | Data integrity violation exception | Data integrity violation exception |
| RPR-AUT-01 | Invalid Token Present | Invalid Token Present |
| RPR-RGS-015 | Invalid Request Value - Input Data is Incorrect | Invalid Request Value - Input Data is Incorrect |

## 4 Manual Adjudication APIs

### 4.1 Manual Adjudication Assignment API

This API is used to assign one single unassigned applicant record to the manual adjudicator.

`POST /registrationprocessor/v1/manualverification/assignment`

#### Resource URL

`https://{base_url}/registrationprocessor/v1/manualverification/assignment`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| String | Yes | The user id |  |

#### Request

```javascript
{
  "id" : "mosip.manual.verification.assignment",
  "version" : "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request" : {
    "userId": "mono29",
        "matchType" : "all"
  }
}
```

#### Response

**Success response**

**Status Code**: 200

**Description**: response code is always 200 if server receives the request.

```javascript
{
   "id":"mosip.manual.verification.assignment",
   "version":"1.0",
   "responsetime":"2019-02-14T12:40:59.768Z",
   "response":{
      "regId":"27847657360002520181208123456",
      "url":"<datashare url for regid>",
      "mvUsrId":"mono29",
      "statusCode":"ASSIGNED",
      "gallery":[
         {
            "matchedRegId":"27847657360002520181208123451",
            "url":"<data share for matchedRegId>",
            "matchedRefType":"RID",
            "reasonCode":null
         },
         {
            "matchedRegId":"27847657360002520181208123452",
            "url":"<data share for matchedRegId>",
            "matchedRefType":"RID",
            "reasonCode":null
         }
      ],
   },
   "errors":null
}
```

**Failure response**

```javascript
{
  "id" : "mosip.manual.verification.assignment",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response": null,
  "errors" : [
    {
      "errorCode" : "RPR-FAC-003",
      "message" : "Cannot find the Registration Packet"
    }
  ]
}
```

#### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-MVS-005 | fields can not be empty | fields can not be empty |
| RPR-MVS-004 | No Assigned Record Found | No Assigned Record Found |
| RPR-MVS-006 | Missing Input Parameter - requesttime | Missing Input Parameter - requesttime |
| RPR-MVS-007 | Missing Input Parameter - id | Missing Input Parameter - id |
| RPR-MVS-008 | Invalid Input Parameter - version | Invalid Input Parameter - version |
| RPR-MVS-011 | Invalid Argument Exception | Invalid Argument Exception |
| RPR-MVS-012 | Unknown Exception | Unknown Exception |
| RPR-MVS-013 | Request Decoding Exception | Request Decoding Exception |
| RPR-MVS-017 | User Id should not empty or null | User Id should not empty or null |
| RPR-MVS-015 | User is not in ACTIVE status | User is not in ACTIVE status |
| RPR-MVS-020 | Match Type is Invalid | Match Type is Invalid |
| RPR-MVS-022 | TablenotAccessibleException in Manual verification | TablenotAccessibleException in Manual verification |

### 4.2 Manual Adjudication Decision API

This API is used to get the decision from manual adjudicator for an applicant and update the decision in table. The packet is sent for further processing based on decision.

`POST /registrationprocessor/v1/manualverification/decision`

#### Resource URL

`https://{base_url}/registrationprocessor/v1/manualverification/decision`

#### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | JSON |
| Requires Authentication | Yes |

#### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| ManualVerificationDTO | Yes | Dto containing manual adjudication info |  |

#### Request

```javascript
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request" : {
      "matchedRefType": "RID",
      "mvUsrId": "mono",
      "reasonCode": "Problem with biometrics",
      "regId": "27847657360002520181208123456",
      "statusCode": "APPROVED"
    }
}
```

#### Response

**Status Code**: 200

**Description**: response code is always 200 if server receives the request.

**Success response**

```javascript
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : {
    "regId": "27847657360002520181208123456",
    "mvUsrId": "mono",
    "statusCode": "APPROVED",
    "matchedRefType": "RID",
    "reasonCode": "Problem with biometrics"
  },
  "errors": null
}
```

**Failure response**

```javascript
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response": null,
    "errors" : [{
        "errorCode" : "RPR-MVS-003",
        "message" : "Invalid status update"
    }]
}
```

#### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-MVS-003 | Invalid status update | Invalid status update |
| RPR-MVS-005 | fields can not be empty | fields can not be empty |
| RPR-MVS-004 | No Assigned Record Found | No Assigned Record Found |
| RPR-MVS-018 | Packet Not Found in Packet Store | Packet Not Found in Packet Store |
| RPR-MVS-006 | Missing Input Parameter - requesttime | Missing Input Parameter - requesttime |
| RPR-MVS-007 | Missing Input Parameter - id | Missing Input Parameter - id |
| RPR-MVS-008 | Invalid Input Parameter - version | Invalid Input Parameter - version |
| RPR-MVS-011 | Invalid Argument Exception | Invalid Argument Exception |
| RPR-MVS-012 | Unknown Exception | Unknown Exception |
| RPR-MVS-013 | Request Decoding Exception | Request Decoding Exception |
| RPR-MVS-017 | User Id should not empty or null | User Id should not empty or null |
| RPR-MVS-015 | User is not in ACTIVE status | User is not in ACTIVE status |
| RPR-MVS-016 | Reg Id should not be null or empty | Reg Id should not be null or empty |
| RPR-MVS-021 | Manual verification rejected | Manual verification rejected |
| RPR-MVS-022 | TablenotAccessibleException in Manual verification | TablenotAccessibleException in Manual verification |

## 5 Bio Dedupe API

The abis would call bio-dedupe callback API to get the biometric cbeff file.

`GET /registrationprocessor/v1/bio-dedupe/biometricfile/{referenceid}`

### Resource URL

`https://{base_url}/registrationprocessor/v1/bio-dedupe/biometricfile/{referenceid}`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | byte\[\] |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| byte\[\] | Yes | byte array of CBEFF file |  |

### Response

**Status codes**: 200

**Description**: response code is always 200 if server receives the request.

#### Success Response

```javascript
// byte array of CBEFF xml file
```

#### Failure Response

```javascript
{
  "id" : "mosip.registration.biometrics",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response": null,
  "errors" : [
    {
      "errorCode" : "RPR-MVS-001",
      "message" : "Access Denied"
    }
  ]
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-MVS-001 | Access Denied | Access Denied for the role |
| RPR-AUT-01 | Invalid Token Present | Invalid Token Present |

## 6 Packet Generator API

The residence service portal would call packet generator API to activate or deactivate uin.

`POST /registrationprocessor/v1/requesthandler/packetgenerator`

### Resource URL

`https://{base_url}/registrationprocessor/v1/requesthandler/packetgenerator`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | JSON |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| PacketGeneratorRequestDto | Yes | Dto containing information required for activate or deactivate packet |  |

### Request

```javascript
{
  "id": "mosip.registration.packetgenerator",
  "version": "1.0",
  "requesttime": "2019-02-02T06:12:25.288Z",
  "request": {
    "centerId": "10031",
    "machineId": "10011",
    "reason": "something",
    "registrationType": "DEACTIVATED",
    "uin": "4215839851"
  }
}
```

### Response

**Status Code**:200

**Description**: response code is always 200 if server receives the request.

#### Success Response

```javascript
{
  "id": "mosip.registration.packetgenerator",
  "version": "1.0",
  "responsetime": "2019-02-02T06:12:25.288Z",
  "response": {
    "registrationId": "10031100110005020190313110030",
    "status": "SUCCESS",
    "message": "Packet created and uploaded"
  },
  "errors": null
}
```

#### Failure Response

```text
{
  "id": "mosip.registration.packetgenerator",
  "version": "1.0",
  "responsetime": "2019-02-02T06:12:25.288Z",
  "response": null,
  "errors": [
    {
      "errorCode": "RPR-MVS-001",
      "message": "Access Denied"
    }
  ]
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-MVS-001 | Access Denied | Access Denied for the role |
| RPR-AUT-01 | Invalid Token Present | Invalid Token Present |
| RPR-PGS-001 | The Packet store set by the System is not accessible | The Packet store set by the System is not accessible |
| RPR-PGS-002 | The key is invalid or illegal argument | The key is invalid or illegal argument |
| RPR-PGS-003 | The Api resource is not available | The Api resource is not available |
| RPR-PGS-004 | reg Based checked exception | reg Based checked exception |
| RPR-PGS-005 | Exception while parsing object to JSON | Exception while parsing object to JSON |
| RPR-PGS-007 | Exception occurred while encrypting the packet Invalid data | Exception occurred while encrypting the packet Invalid data |
| RPR-PGS-008 | Exception occurred while encrypting the packet Invalid Key | Exception occurred while encrypting the packet Invalid Key |
| RPR-PGS-009 | Packet meta info converter error | Packet meta info converter error |
| RPR-PGS-010 | Missing Input Parameter | Missing Input Parameter |
| RPR-PGS-011 | Invalid Input Parameter | Invalid Input Parameter |
| RPR-PGS-012 | Input Data Validation Failed | Input Data Validation Failed |

## 7 Packet Uploader API

The dmz camel-bridge calls packet uploader API to upload the packet in file system\(Hdfs, ceph etc\). This service is a bridge between dmz and secure network. It accepts json request and connects to dmz VM to get the packet and move it to archive location.

`POST /registrationprocessor/v1/uploader/securezone`

### Resource URL

`https://{base_url}/registrationprocessor/v1/uploader/securezone`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | String |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| MessageDto | Yes | Dto being transferred in each and every stage of reg-proc |  |

### Request

```javascript
{
  "rid": "10003100030000420190625111842",
  "reg_type" : "NEW",
  "isValid": true,
  "internalError": false,
  "messageBusAddress": "packet-receiver-bus-out",
  "retryCount": 0
}
```

### Response

**Status Code**:200

**Description**: response code is always 200 if server receives the request.

#### Success Response

```javascript
Packet with registrationId 10003100030000420190625111842 has been forwarded to next stage
```

#### Failure Response

```javascript
Packet with registrationId 10003100030000420190625111842 has not been uploaded to file System
```

## 8 Request Handler API

The residence service portal would call this api to reprint uin card upon receiving request from the applicant.

`POST /registrationprocessor/v1/requesthandler/reprint`

### Resource URL

`https://{base_url}/registrationprocessor/v1/requesthandler/reprint`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | JSON |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| id | Yes | reprint id | mosip.uincard.reprint |
| version | Yes | the version for sync | 1.0 |
| requesttime | Yes | the requesttime for sync | 2019-02-14T12:40:59.768Z |
| request | Yes | the request object | 1.0 |
| cardType | Yes | the type of the card | 'UIN' OR 'MASKED\_UIN' |
| idType | Yes | type of id provided | 'UIN' OR 'VID' |
| id | Yes | the id provided | 5647294083 |
| registrationType | Yes | This indicates the registration type in registration processor. The camel route is decided based on this | RES\_REPRINT |
| centerId | Yes | center id required to create packet | 10003 |
| machineId | Yes | machine id required to create packet | 10003 |
| reason | No | The reason for reprint | Any string |

### Request

```javascript
{
  "id": "mosip.uincard.reprint",
  "request": {
    "cardType": "UIN",
    "centerId": "10003",
    "id": "5647294083",
    "idType": "UIN",
    "machineId": "10003",
    "reason": "testing",
    "registrationType": "RES_REPRINT"
  },
  "requesttime": "2019-09-13T11:34:13.827Z",
  "version": "1.0"
}
```

### Response

**Status Code**:200

**Description**: response code is always 200 if server receives the request.

#### Success Response

```javascript
{
  "id": "mosip.uincard.reprint",
  "version": "1.0",
  "responsetime": "2019-09-13T11:54:55.313Z",
  "response": {
    "registrationId": "10003100030000120190913115453",
    "status": "Packet has reached Packet Receiver",
    "message": "Packet created and uploaded"
  },
  "errors": null
}
```

#### Failure response

```text
{
  "id": "mosip.uincard.reprint",
  "version": "1.0",
  "responsetime": "2019-09-13T11:49:56.180Z",
  "response": null,
  "errors": [
    {
      "errorCode": "RPR-PGS-011",
      "message": "Invalid Input Parameter - requesttime"
    },
    {
      "errorCode": "RPR-RGS-015",
      "message": "Invalid Request Value - Input Data is Incorrect"
    }
  ]
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-MVS-001 | Access Denied | Access Denied for the role |
| RPR-AUT-01 | Invalid Token Present | Invalid Token Present |
| RPR-PGS-001 | The Packet store set by the System is not accessible | The Packet store set by the System is not accessible |
| RPR-PGS-002 | The key is invalid or illegal argument | The key is invalid or illegal argument |
| RPR-PGS-003 | The Api resource is not available | The Api resource is not available |
| RPR-PGS-004 | reg Based checked exception | reg Based checked exception |
| RPR-PGS-005 | Exception while parsing object to JSON | Exception while parsing object to JSON |
| RPR-PGS-007 | Exception occurred while encrypting the packet Invalid data | Exception occurred while encrypting the packet Invalid data |
| RPR-PGS-008 | Exception occurred while encrypting the packet Invalid Key | Exception occurred while encrypting the packet Invalid Key |
| RPR-PGS-009 | Packet meta info converter error | Packet meta info converter error |
| RPR-PGS-010 | Missing Input Parameter | Missing Input Parameter |
| RPR-PGS-011 | Invalid Input Parameter | Invalid Input Parameter |
| RPR-PGS-012 | Input Data Validation Failed | Input Data Validation Failed |

## 9 Registration Transaction API

This API is used to find all the transactions for a registration id. This service accepts a registration id and returns all transactions associated with it.

### Resource URL

`GET /registrationprocessor/v1/registrationtransaction/search/{langcode}/{rid}`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Response format | JSON |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| langcode | Yes | The language code |  |
| registrationId | Yes | The registration id |  |

### Request

```javascript
-NA-
```

### Response

**Scenario**: Record found

**Status Code**: 200

**Description**: Successfully retrieved information

```javascript
{
  "id" : "mosip.registration.transaction",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : [
  {
    "id" : "810e43c3-cc89-4581-84f0-5ee535bf7e3a",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "PACKET_RECEIVER",
    "parentTransactionId" : null,
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-PKR-SUCCESS-001",
    "statusComment" : "Packet is in PACKET_RECEIVED status",
    "createdDateTimes" : "2019-06-19 10:42:15.04"
  },
  {
    "id" : "76796d41-3c42-40a8-8842-02fe87bf4aab",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "PACKET_RECEIVER",
    "parentTransactionId" : "810e43c3-cc89-4581-84f0-5ee535bf7e3a",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-PKR-SUCCESS-002",
    "statusComment" : "Packet is in PACKET_UPLOADED_TO_LANDING_ZONE status",
    "createdDateTimes" : "2019-06-19 10:42:16.285"
  },
  {
    "id" : "d04b74cc-7364-407f-aa40-058daa774136",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "UPLOAD_PACKET",
    "parentTransactionId" : "76796d41-3c42-40a8-8842-02fe87bf4aab",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-PKU-SUCCESS-001",
    "statusComment" : "Packet 10006100067159820190618081137 is uploaded in file system.",
    "createdDateTimes" : "2019-06-19 10:42:21.507"
  },
  {
    "id" : "19be9e8f-1740-4b6e-8b07-2ea5628abc12",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "VALIDATE_PACKET",
    "parentTransactionId" : "d04b74cc-7364-407f-aa40-058daa774136",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-PKV-SUCCESS-001",
    "statusComment" : "Packet structural validation is successful",
    "createdDateTimes" : "2019-06-19 10:42:34.265"
  },
  {
    "id" : "72d8099d-37e1-4bcc-a772-a4c86b441acf",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "QUALITY_CHECK",
    "parentTransactionId" : "19be9e8f-1740-4b6e-8b07-2ea5628abc12",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-QCS-SUCCESS-001",
    "statusComment" : "All Quality Scores are more than threshold",
    "createdDateTimes" : "2019-06-19 10:42:35.677"
  },
  {
    "id" : "0a7baa01-2d64-4e82-89cd-a6e2bdcebe72",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "OSI_VALIDATE",
    "parentTransactionId" : "72d8099d-37e1-4bcc-a772-a4c86b441acf",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-OSI-SUCCESS-001",
    "statusComment" : "OSI Validation is successful",
    "createdDateTimes" : "2019-06-19 10:42:35.677"
  },
  {
    "id" : "dd7d8892-1cdd-4af7-99fc-9b2ef59d207c",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "BIOMETRIC_AUTHENTICATION",
    "parentTransactionId" : "0a7baa01-2d64-4e82-89cd-a6e2bdcebe72",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-BAS-SUCCESS-001",
    "statusComment" : "Biometric Authentication Success",
    "createdDateTimes" : "2019-06-19 10:42:35.677"
  },
  {
    "id" : "247eb4b2-3abc-4f2d-9200-01a4c6b76217",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "DEMOGRAPHIC_VERIFICATION",
    "parentTransactionId" : "dd7d8892-1cdd-4af7-99fc-9b2ef59d207c",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-DDS-SUCCESS-001",
    "statusComment" : "Demographic Authentication Success",
    "createdDateTimes" : "2019-06-19 10:42:35.677"
  },
  {
    "id" : "c478ba68-64a0-4b8d-8e50-a59c12926de6",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "BIOGRAPHIC_VERIFICATION",
    "parentTransactionId" : "247eb4b2-3abc-4f2d-9200-01a4c6b76217",
    "statusCode": "IN_PROGRESS",
    "statusCommentCode" : "RPR-BDS-SUCCESS-001",
    "statusComment" : "Packet biodedupe Inprogress",
    "createdDateTimes" : "2019-06-19 10:43:22.758"
  },
  {
    "id" : "faaaf60f-a591-40a7-b5fa-b6b7fa5894bd",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "BIOMETRIC_AUTHENTICATION",
    "parentTransactionId" : "c478ba68-64a0-4b8d-8e50-a59c12926de6",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-BDS-SUCCESS-002",
    "statusComment" : "Packet biodedupe successful",
    "createdDateTimes" : "2019-06-19 10:43:34.845"
  },
  {
    "id" : "66d87a75-a32e-4651-bb64-23a552a8dd69",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "UIN_GENERATOR",
    "parentTransactionId" : "faaaf60f-a591-40a7-b5fa-b6b7fa5894bd",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-UIN-SUCCESS-001",
    "statusComment" : "Data updated successfully for regId  for registration Id:  10006100067159820190618081137",
    "createdDateTimes" : "2019-06-19 10:43:42.709"
  },
  {
    "id" : "42df348d-6f9f-49c2-830b-4da8e1f6123c",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "PRINT_POSTAL_SERVICE",
    "parentTransactionId" : "66d87a75-a32e-4651-bb64-23a552a8dd69",
    "statusCode": "PROCESSED",
    "statusCommentCode" : "RPR-PPS-SUCCESS-001",
    "statusComment" : "Pdf added to the mosip queue for printing",
    "createdDateTimes" : "2019-06-19 10:42:35.677"
  },
 {
    "id" : "0039b5fd-fe6a-4cb7-9456-5f2f25977bb4",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "PRINT_POSTAL_SERVICE",
    "parentTransactionId" : "66d87a75-a32e-4651-bb64-23a552a8dd69",
    "statusCode": "PROCESSED",
    "statusCommentCode" : "RPR-PPS-SUCCESS-002",
    "statusComment" : "Print and Post Completed for the regId : 10006100067159820190618081137",
    "createdDateTimes" : "2019-06-19 10:42:35.677"
  },
 {
    "id" : "53b573fd-349d-4171-ba7f-29a926345ded",
    "registrationId": "10006100067159820190618081137",
    "transactionTypeCode" : "NOTIFICATION",
    "parentTransactionId" : "66d87a75-a32e-4651-bb64-23a552a8dd69",
    "statusCode": "SUCCESS",
    "statusCommentCode" : "RPR-MSS-SUCCESS-001",
    "statusComment" : "Notification sent successfully for registrationId 10006100067159820190618081137",
    "createdDateTimes" : "2019-06-19 10:43:56.823"
  }
],
"errors": null
}
```

**Scenario**: Record not found

**Status Code**: 200

**Description**: Successfully retrieved information

```javascript
{
  "id" : "mosip.registration.transaction",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : null,
  "errors" : [
    {
        "status": "FAILURE",
      "errorCode": "RPR-RTS-001",
      "errorMessage": "Invalid RID"
    }
  ]
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-MVS-001 | Access Denied | Access Denied for the role |
| RPR-AUT-01 | Invalid Token Present | Invalid Token Present |
| RPR-RTS-001 | RID Not Found | RID Not Found |
| RPR-RTS-002 | Unknown Exception occurred | Unknown Exception occurred |
| RPR-RTS-003 | Invalid request | Invalid request |
| RPR-RTS-004 | globalMessages not found for input langCode | globalMessages not found for input langCode |

## 10 UIN Card API

The residence service portal would call this API to get uin card upon receiving request from the applicant.

`POST /registrationprocessor/v1/print/uincard`

### Resource URL

`https://{base_url}/registrationprocessor/v1/print/uincard`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | application/pdf |
| Error Response format | JSON |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| id | Yes | reprint id | mosip.print |
| version | Yes | the version | 1.0 |
| requesttime | Yes | the requesttime | 2019-02-14T12:40:59.768Z |
| request | Yes | the request object | 1.0 |
| cardType | Yes | the type of the card | 'UIN' OR 'MASKED\_UIN' |
| idType | Yes | type of id provided | 'UIN' OR 'VID' OR 'RID' |
| idValue | Yes | the id provided | 5647294083 |

### Request

```javascript
{
  "id": "mosip.registration.print",
  "request": {
    "cardType": "UIN",
    "idValue": "5647294083",
    "idType": "UIN"
  },
  "requesttime": "2019-09-13T11:34:13.827Z",
  "version": "1.0"
}
```

### Response

**Status Code**:200

**Description**: response code is always 200 if server receives the request.

#### Success response

```javascript
// PDF bytes
```

#### Failure response

```text
{
  "id": "mosip.registration.print",
  "version": "1.0",
  "responsetime": "2019-09-18T06:28:55.676Z",
  "errors": [
    {
      "errorCode": "RPR-PRT-011",
      "message": "UIN length should be as per configured digit."
    }
  ],
  "response": null
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-MVS-001 | Access Denied | Access Denied for the role |
| RPR-AUT-01 | Invalid Token Present | Invalid Token Present |
| RPR-PRT-001 | Error while generating PDF for UIN Card | Error while generating PDF for UIN Card |
| RPR-PRT-002 | UIN not found in database | UIN not found in database |
| RPR-PRT-003 | PDF Generation Failed | PDF Generation Failed |
| RPR-PRT-004 | Queue connection is null | Queue connection is null |
| RPR-PRT-005 | Error while generating QR Code | Error while generating QR Code |
| RPR-PRT-006 | Error while setting applicant photo | Error while setting applicant photo |
| RPR-PRT-007 | Error while setting qrCode for uin card | Error while setting qrCode for uin card |
| RPR-PRT-008 | ID Repo response is null | ID Repo response is null |
| RPR-PRT-009 | ID Repo response has no documents | ID Repo response has no documents |
| RPR-PRT-011 | Error while print data validation | Error while print data validation |
| RPR-PRT-012 | Invalid CardType : Enter UIN or MASKED\_UIN | Invalid CardType : Enter UIN or MASKED\_UIN |
| RPR-PRT-013 | Invalid IdType : Enter UIN or VID or RID | Invalid IdType : Enter UIN or VID or RID |
| RPR-PRT-014 | UIN is not valid | UIN is not valid |
| RPR-PRT-015 | VID is not valid | VID is not valid |
| RPR-PRT-016 | RID is not valid | RID is not valid |
| RPR-PRT-017 | Error while creating VID | Error while creating VID |
| RPR-PRT-018 | Could not generate/regenerate VID as per policy,Please use existing VID | Could not generate/regenerate VID as per policy,Please use existing VID |
| RPR-PRT-019 | Invalid Input Parameter | Invalid Input Parameter |

## 11 Lost UIN Or RID API

The residence service portal would call this api to search lost uin OR rid. The request type is post since request json is expected in request body.

`POST /registrationprocessor/v1/requesthandler/lost`

### Resource URL

`https://{base_url}/registrationprocessor/v1/requesthandler/lost`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | JSON |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Comment |
| :--- | :--- | :--- | :--- |
| id | Yes | the id | mosip.registration.lost |
| version | Yes | the version | 1.0 |
| requesttime | Yes | the requesttime | 2019-02-14T12:40:59.768Z |
| request | Yes | the request object | 1.0 |
| idType | Yes | the type of id | 'UIN' OR 'RID' |
| name | Yes | Fullname of the resident | resident name |
| postalCode | Yes | the pincode or postalcode | postalcode of resident address |
| contactType | Yes | contact type of applicant | "EMAIL" or "PHONE" |
| contactValue | Yes | contact value | the email id or phone number |
| langCode | Yes | Language Code | Primary or secondary language as configured by country |

### Request

```javascript
{
  "id": "mosip.registration.lost",
  "requesttime": "2019-09-13T11:34:13.827Z",
  "version": "1.0",
  "request": {
    "idType": "UIN",
    "name": "Monobikash Das",
    "postalCode": "14022",
    "contactType": "EMAIL",
    "contactValue": "monobikash.das@mindtree.com"
  }
}
```

### Response

**Status Code**:200

**Description**: response code is always 200 if server receives the request.

#### Success response

```javascript
{
  "id": "mosip.registration.lost",
  "version": "1.0",
  "responsetime": "2019-09-13T11:54:55.313Z",
  "response": {
    "idValue": "8787567820"
  },
  "errors": null
}
```

#### Failure response

```text
{
  "id": "mosip.registration.lost",
  "version": "1.0",
  "responsetime": "2019-09-18T06:28:55.676Z",
  "errors": [
    {
      "errorCode": "RPR-SER-001",
      "message": "No Records Found."
    }
  ],
  "response": null
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| RPR-PGS-021 | No Records Found | No Records Found |
| RPR-PGS-022 | Multiple Records Found | Multiple UIN is found |
| RPR-PGS-016 | Invalid Input Value - ID Type | Invalid ID Type |
| RPR-PGS-018 | Invalid Input Value - Name cannot be NULL or Empty | Name is Empty or NULL |
| RPR-PGS-017 | Invalid Input Value - Contact Type | Invalid Contact Type |

## 12 Update UIN API

The residence service portal would call this api to update demographic information along with documents.

`POST /registrationprocessor/v1/requesthandler/update`

### Resource URL

`https://{base_url}/registrationprocessor/v1/requesthandler/update`

### Resource details

| Resource Details | Description |
| :--- | :--- |
| Request format | JSON |
| Response format | JSON |
| Requires Authentication | Yes |

### Parameters

| Name | Required | Description | Default Value | Example |
| :--- | :--- | :--- | :--- | :--- |
| id | Y | API Id |  | mosip.resident.uin |
| version | Y | API version |  | v1 |
| requestTime | Y | Time when Request was captured |  | 2018-12-09T06:39:04.683Z |
| request: idValue | Y | UIN |  | 9830872690593682 |
| request: idType | Y | Allowed Type of Individual ID - VID, UIN | UIN |  |
| request: identityJson | Y | Demographic data of an Individual |  |  |
| request: proofOfAddress | Y | address document of an Individual |  |  |
| request: proofOfIdentity | Y | Identity document of an Individual |  |  |
| request: proofOfRelationship | Y | Relationship proof document of an Individual |  |  |
| request: proofOfDateOfBirth | Y | DOB proof document of an Individual |  |  |
| request: centerId | Y | Constant center Id of resident service portal to generate rid |  |  |
| request: machineId | Y | Constant machine id of resident service portal to generate rid |  |  |

### Request

```javascript
{
  "id": "mosip.registration.update",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
    "idValue": "9830872690593682",
    "idType": "UIN",
    "centerId": "1234",
    "machineId": "12345678",
    "identityJson": "<base 64 encoded string>",
    "proofOfAddress": "<base 64 encoded string>",
    "proofOfIdentity": "<base 64 encoded string>",
    "proofOfRelationship": "<base 64 encoded string>",
    "proofOfDateOfBirth": "<base 64 encoded string>"
  }
}
```

### Response

**Status Code**:200

**Description**: response code is always 200 if server receives the request.

#### Success response

```javascript
{
  "id": "mosip.registration.update",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {
    "registrationId": "10031100110005020190313110030",
    "status": "SUCCESS",
    "message": "Update request received"
  },
  "errors": null
}
```

#### Failure response

```text
{
  "id": "mosip.registration.update",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": null,
  "errors": [
    {
      "errorCode": "XXX-XXX-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```

### Failure details

| Error Code | Error Message | Error Description |
| :--- | :--- | :--- |
| Invalid UIN | Invalid UIN |  |
| Invalid Request type | Invalid Request type |  |

