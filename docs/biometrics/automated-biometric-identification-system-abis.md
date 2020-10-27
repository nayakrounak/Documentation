# ABIS

## Overview

Providing unique identity for a resident is one of key features of any identity platform. To achieve this, MOSIP interfaces with an **Automated Biometric Identification System \(ABIS\)** to perform de-duplication of a resident's biometric data.

MOSIP is designed to integrate with multiple ABISs to leverage expertise of different ABIS providers. A country may use one ABIS for fingerprint and another for Iris or use multiple ABISs for the same biometric data and evaluate the best ABIS based on de-duplication quality.

The ABIS system never comes to know about resident's identity. Any Personally Identifiable Information \(PII\) such as demographic details or RID \(Request ID for Registration\) is not shared with the ABIS system. Internally, MOSIP maintains a mapping between the ABIS specific referenceID and RID of the resident.

{% hint style="info" %}
ABIS is used for 1:N de-duplication. For 1:1 authentication [Biometric SDK](biometric-sdk.md) is used. MOSIP does not recommend using an ABIS for 1:1 authentication.
{% endhint %}

![](../.gitbook/assets/abis_middleware.png)

## ABIS middle-ware

MOSIP's ABIS middle-ware has the following components

* MOSIP ABIS request handler 
* Request router \(based on routing policy, an ABIS request is routed to the correct ABIS system\)
* ABIS response handler

Below is the MOSIP ABIS middle-ware process flow,

![](../.gitbook/assets/abis_middleware-process_flow.png)

## MOSIP-ABIS interface

MOSIP interacts with ABIS only via message queues. JSON format is used for all control messages in the queue. MOSIP ABIS middle-ware sends requests to inbound queue address and receives responses from outbound queue address. For details refer to the [ABIS API Specifications](../apis/abis-apis.md).

ABIS must support the following types of biometric images:

* Individual fingerprint images \(segmented\)
* Iris images \(left, right\)
* Face image

Biometrics data in MOSIP is exchanged as per formats defined in [Biometric Data Specification](biometric-data-specification.md).

## ABIS deployment

* ABIS must comply to [ABIS API Specifications](../apis/abis-apis.md).
* The queues can be configured in [RegistrationProcessorAbis-env.json](https://github.com/mosip/mosip-config/blob/master/config-templates/RegistrationProcessorAbis-env.json) file.

  ABIS system connects to the queues using a pre-defined user id and password. 

* It is recommended that ABIS is deployed in the same secure zone \(military zone\) where the registration processor is deployed. 
* ABIS system is not recommended to connect to any external network.

