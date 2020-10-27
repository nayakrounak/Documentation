# Release Notes 1.0.6

## Table Of Contents

* [Scope](release-notes-1.0.6.md#scope-)
* [Documentation](release-notes-1.0.6.md#documentation-)
* [Key Points](release-notes-1.0.6.md#key-points-)
* [Code](release-notes-1.0.6.md#code-)
* [Test Reports](release-notes-1.0.6.md#test-reports-)
  * [1. In scope](release-notes-1.0.6.md#1-in-scope-)
  * [2. Not in scope](release-notes-1.0.6.md#2-Not-in-scope-)
  * [3. Executive Summary – Consolidated Quality Status](release-notes-1.0.6.md#3-executive-summary--consolidated-quality-status-)
  * [4. Types of Testing](release-notes-1.0.6.md#4-types-of-testing-)
  * [5. Test Execution Summary](release-notes-1.0.6.md#5-test-execution-summary-)
* [Known Issues](release-notes-1.0.6.md#known-issues-)
* [List Of Acronyms](release-notes-1.0.6.md#list-of-acronyms-)

## Scope [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

Version **1.0.6** of MOSIP Platform is a feature and stability release.

This release is with **real biometrics**. This means that MOSIP Platform is now integrated with SDK, MDS \(MOSIP Device Service\), ABIS \(Automated Biometrics Identification System\) and Biometric devices.Non-functional requirements \(Performance, Scale and Security\) will be taken up in subsequent releases.

Release Date: February 11, 2020

Highlights of the 1.0.6 release include:

* New Module is added – [Resident Services](release-notes-1.0.0/release-notes-1.0.0-features.md#residnet-services)
* [New features added to MOSIP platform](release-notes-1.0.0/release-notes-1.0.0-features.md) 
* UI/UX refinements for Administration Module
* Bug Fixes across all modules
* Repository structure changes

Module-wise features released as part of this release can be found [here](https://github.com/nayakrounak/documentation/tree/4f2723f5f3c02a9b74329ac70a3d7bf39914858e/docs/_files/release/1.0.6/MOSIP_Feature_Release_v1.0.6.xlsx)

## Documentation [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

### 1. Platform Documentation

Includes Functional requirements, Process flows, Architecture and High level design, Getting started and Deployment guide, Developer documentation etc. Please find the [link to Platform Documentation](https://docs.mosip.io/platform/).

### 2. Detailed Documentation

Low level design documents for respective modules is found below:

* [Pre-Registration](https://github.com/mosip/pre-registration/tree/master/design/pre-registration)
* [Registration Client](https://github.com/mosip/registration/tree/master/design/registration)
* [Registration Processor](https://github.com/mosip/registration/tree/master/design/registration-processor)
* [Authentication](https://github.com/mosip/id-authentication/tree/master/design/authentication)
* {Administration\]\([https://github.com/mosip/admin-services/tree/master/design/admin](https://github.com/mosip/admin-services/tree/master/design/admin)\)
* [ID Repository](https://github.com/mosip/commons/tree/master/design/kernel)
* [Kernel](https://github.com/mosip/commons/tree/master/design/idrepository)
* [Resident Services](https://github.com/mosip/resident-services/tree/master/design/resident-service)

### 3. Platform Configuration for RBR

MOSIP Platform can be configured to be used for Real Biometrics. Please find the [guide to configure MOSIP for biometrics](../modules/registration-client/guide-to-configure-mosip-for-biometrics.md).

## Key Points [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

| Key Points | Details |
| :--- | :--- |
| Pre Registration - Browser support | Chrome 74.0.3729 |
| Deployment Script Environment | Microsoft Azure |
| Registration Client – OS version | Windows 10 \(English version\)  with TPM 2.0 |
| Camera | Logitech / Default windows camera |
| Scanner | Canon lide 120 |
| GPS | GlobalSat BU-353-S4 |
| Biometrics standard | CBEFF format \(Version - 2.0\) |
| MOSIP Device Service \(MDS\) | Version - 0.9.1 |
| SMS gateway | MSG91, Infobip |
| Registration Client – face capture | OpenImaj - This is licensed for demo purpose only |
| Keystore | SoftHSM |
| Antivirus | ClamAV |
| Maps | OpenstreetMap |
| Supporting key based digital signatures, not using digital certificates |  |
| Transliteration | ICU4J \(Library with French, Arabic languages\) |
| ABIS | TECH5 abis version v2.0.5 |
| SDK | Identy SDK version v0.0.0.9 |

## Code [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

The code and [automation tests](https://github.com/mosip/mosip-functional-tests) are available on [GitHub](https://github.com/mosip/). The code needs to be built and deployed as per the procedure documented in [Building And Deploying MOSIP](../build-and-deploy/build-and-deploy.md). We will actively support System Integrators during their first deployment.

## Test Reports [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

#### 1. In scope [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

| Title | Description |
| :--- | :--- |
| Modules Tested |  Pre-registration \(UI & Server\)  Registration Client \(UI & APIs\)  Kernel \(APIs\)  Registration Processor \(Server\)  ID Authentication \(APIs\)  ID Repo \(APIs\)  Administration \(UI & APIs\)  Resident Services \(APIs\) |
| Version Tag Tested | 1.0.6 |
| Test Methodology |   Manual   Test Automation |
| Types of testing |      Smoke  Functional   Integration      Regression |
| Testing Levels | ![Image](../.gitbook/assets/image1.jpg) |
| Configuration Parameters tested for | Refer to properties file at [**Link**](https://github.com/mosip/mosip-config/tree/1.0.6-rc/config-templates) |
| Browser Support | **Pre-Registration**     Chrome – 78.0.3904.108 |
| OS Support | **Registration Client**     Windows 10 |
| Language Support | French, Arabic, English |

#### 2. Not in scope [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

| Title | Description |
| :--- | :--- |
| NFR Testing |  Scalability Testing  Performance Testing  Security Testing |
| Configuration Testing |  Testing is done for one set of approved production configuration  Changing the configuration parameters for various values \(boundary values\) and testing the impact of each such value on the platform code will be taken up in subsequent releases. |

#### 3. Executive Summary – Consolidated Quality Status [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

| Sl. No. | Module / Activity | Test Methodology | Test Status |
| :--- | :--- | :--- | :--- |
| 1 | Kernel |  Test Automation | PASS |
| 2 | Pre-Registration |  Test Automation | PASS |
| 3 | Registration Client |  Tested Manually  Test Automation | PASS |
| 4 | Registration Processor |  Tested Manually  Test Automation | PASS |
| 5 | ID Authentication |   Test Automation | PASS |
| 6 | ID Repo |  Test Automation | PASS |
| 7 | Resident Services |  Test Automation | PASS |
| 8 | Pre-Registration to Registration Client integration testing |  Tested Manually | PASS |
| 9 | Registration Client to Registration Processor integration testing |  Tested Manually | PASS |
| 10 | Registration Processor to IDA integration testing |      Tested Manually | PASS |
| 11 | IDA to ID Repo |      Tested Manually | PASS |

#### 4. Types of Testing [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

| Testing Type | Description |
| :--- | :--- |
| Smoke Testing | Tests to ensure basic workflows work fine |
| Functional Testing | Tests to ensure functionality of each module and overall system work fine in accordance with the given requirements |
| Integration Testing | Tests to ensure the inter module functionality works fine and in accordance with the integration requirements |
| Regression Testing | Tests to ensure that any change doesn't break existing functionality |

#### 5. Test Execution Summary [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

![](../.gitbook/assets/ExecutionSummary_1.0.6.jpg)

## Known Issues [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

![](../.gitbook/assets/KnownIssues_1.0.6.jpg)

## List Of Acronyms [**\[↑\]**](release-notes-1.0.6.md#table-of-contents)

| Acronym | Expanded Form |
| :--- | :--- |
| ABIS | Automated Biometric Identification System |
| API | Application Programming Interface |
| ID | Identity |
| IDA | Identity Authentication |
| MOSIP | Modular Open Source Identity Platform |
| NFR | Non-Functional Requirements |
| OTP | One Time Password |
| SDK | Software Development Kit |
| TBD | To Be Determined |
| TOTP | Temporary One Time Password |
| UIN | Unique Identification Number |
| WIP | Work In Progress |
| CBEFF | Common Biometric Exchange Formats Framework |
| HSM | Hardware Security Module |
| TPM | Trusted Platform Module |

