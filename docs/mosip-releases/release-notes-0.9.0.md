# Release Notes 0.9.0

## Table Of Contents

* [Scope](release-notes-0.9.0.md#scope-)
* [Documentation](release-notes-0.9.0.md#documentation-)
* [Key Points](release-notes-0.9.0.md#key-points-)
* [Code](release-notes-0.9.0.md#code-)
* [Test Reports](release-notes-0.9.0.md#test-reports-)
  * [1. In scope](release-notes-0.9.0.md#1-in-scope-)
  * [2. Not in scope](release-notes-0.9.0.md#2-Not-in-scope-)
  * [3. Executive Summary – Consolidated Quality Status](release-notes-0.9.0.md#3-executive-summary--consolidated-quality-status-)
  * [4. Types of Testing](release-notes-0.9.0.md#4-types-of-testing-)
  * [5. Test Execution Summary](release-notes-0.9.0.md#5-test-execution-summary-)
* [Known Issues](release-notes-0.9.0.md#known-issues-)
* [List Of Acronyms](release-notes-0.9.0.md#list-of-acronyms-)

## Scope [**\[↑\]**](release-notes-0.9.0.md#table-of-contents)

This release is with **proxy biometrics**. This means that the implementation of Print system, SDK, MDM \(MOSIP Device Manager\), ABIS \(Automated Biometrics Identification System\) and Biometric devices has been stubbed. Also, this version is tested for functionality. Non-functional requirements \(Performance, Scale and Security\) will be taken up in subsequent releases.

* Features included – Pre-Registration, Registration Client, Registration Processor, ID Authentication, Reference GUI implementation of Pre-Registration and Registration Client. 
* Features not included – Administration, Partner Management, Resident Services

## Documentation [**\[↑\]**](release-notes-0.9.0.md#table-of-contents)

### Platform Documentation

Includes Functional requirements, Process flows, Architecture and High level design, Getting started and Deployment guide, Developer documentation etc.  
[**Link to Platform Documentation**](https://docs.mosip.io/platform)

### Detailed Documentation

#### Low Level design

* [Admin](https://github.com/mosip/admin-services/tree/master/design)
* [Pre Registration](https://github.com/mosip/pre-registration/tree/master/design)
* [Registration](https://github.com/mosip/registration/tree/master/design)
* [ID Authentication](https://github.com/mosip/id-authentication/tree/master/design)
* [Commons](https://github.com/mosip/commons/tree/master/design)

### Test cases

* [Functional Test Case](https://github.com/mosip/mosip-functional-tests/tree/0.9.0)

## Key Points [**\[↑\]**](release-notes-0.9.0.md#table-of-contents)

| Key Points | Details |
| :--- | :--- |
| Pre Registration - Browser support | Chrome 74.0.3729\) |
| Deployment Script Environment | Microsoft Azure |
| Registration Client – OS version | Windows 10 \(English version\)  with TPM 2.0 |
| Camera | Logitech / Default windows camera |
| Scanner | Canon lide 120 |
| GPS | GlobalSat BU-353-S4 |
| Biometrics standard | CBEFF format \(Version - 0.9.0\) |
| SMS gateway | MSG91, Infobip |
| Registration Client – face capture | OpenImaj - This is licensed for demo purpose only |
| Keystore | SoftHSM |
| Antivirus | ClamAV |
| Maps | OpenstreetMap |
| Supporting key based digital signatures, not using digital certificates |  |
| Transliteration | ICU4J \(Library with French, Arabic languages\) |

## Code [**\[↑\]**](release-notes-0.9.0.md#table-of-contents)

The code and [automation tests](https://github.com/mosip/mosip-functional-tests/tree/0.9.0) are available on [GitHub](https://github.com/mosip). The code needs to be built and deployed as per the procedure documented in [**Building And Deploying MOSIP**](../build-and-deploy/build-and-deploy.md). We will actively support System Integrators during their first deployment.

## Tests [**\[↑\]**](release-notes-0.9.0.md#table-of-contents)

**Testing Scope**

### In Scope

| Title | Description |
| :--- | :--- |
| Modules Tested |  Pre-registration \(UI & Server\)  Registration Client \(UI & APIs\)  Kernel \(APIs\)  Registration Processor \(Server\)  ID Authentication \(APIs\)  ID Repo \(APIs\) |
| Version Tag Tested | 0.9.0 |
| Test Methodology |   Manual   Test Automation |
| Types of testing |      Smoke  Functional   Integration      Regression |
| Testing Levels | ![Image](../.gitbook/assets/image1.jpg) |
| Configuration Parameters tested for | Refer to QA env properties file with suffix ‘qa’ in the filename, at [**Link**](https://github.com/mosip/mosip-config/tree/0.9.1_23092019) |
| Browser Support | **Pre-Registration**     Chrome – 74.0.3729.169 |
| OS Support | **Registration Client**     Windows 10 |
| Language Support | French, Arabic, English |

### Not in Scope

| Title | Description |
| :--- | :--- |
| NFR Testing |  Scalability Testing  Performance Testing  Security Testing |
| Configuration Testing |  Testing is done for one set of approved production configuration  Changing the configuration parameters for various values \(boundary values\) and testing the impact of each such value on the platform code will be taken up in subsequent releases. |

### Executive Summary – Consolidated Quality Status

| Sl. No. | Module / Activity | Test Methodology | Test Status |
| :--- | :--- | :--- | :--- |
| 1 | Kernel |  Test Automation | PASS |
| 2 | Pre-Registration |  Tested Manually  Test Automation | PASS |
| 3 | Registration Client |  Tested Manually  Test Automation | PASS |
| 4 | Registration Processor |  Tested Manually  Test Automation | PASS |
| 5 | ID Authentication |   Test Automation | PASS |
| 6 | ID Repo |  Test Automation | PASS |
| 7 | Pre-Registration to Registration Client integration testing |  Tested Manually | PASS |
| 8 | Registration Client to Registration Processor integration testing |  Tested Manually | PASS |
| 9 | Registration Processor to Pre-Registration integration testing |   Tested Manually | PASS |
| 10 | Registration Processor to Registration Client integration testing |      Tested Manually | PASS |
| 11 | Registration Client to IDA integration testing |      Tested Manually | PASS |
| 12 | Registration Processor to IDA integration testing |      Tested Manually | PASS |
| 13 | IDA to ID Repo |      Tested Manually | PASS |
| 14 | Kernel API integration |  Tested Manually  Test Automation | PASS |
| 15 | End to end functional testing |  Tested Manually | PASS |

### Types of Testing

| Testing Type | Description |
| :--- | :--- |
| Smoke Testing | Tests to ensure basic workflows work fine |
| Functional Testing | Tests to ensure functionality of each module and overall system work fine in accordance with the given requirements |
| Integration Testing | Tests to ensure the inter module functionality works fine and in accordance with the integration requirements |
| Regression Testing | Tests to ensure that any change doesn't break existing functionality |

### Test Execution Summary

![Image](../.gitbook/assets/ExecutionSummary_0.9.0.jpg)

## Known Issues [**\[↑\]**](release-notes-0.9.0.md#table-of-contents)

![Image](../.gitbook/assets/KnownIssues_0.9.0.jpg)

## List Of Acronyms [**\[↑\]**](release-notes-0.9.0.md#table-of-contents)

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

