# Release Notes 1.0.5

## Table Of Contents

* [Scope](release-notes-1.0.5.md#scope-)
* [Documentation](release-notes-1.0.5.md#documentation-)
* [Key Points](release-notes-1.0.5.md#key-points-)
* [Code](release-notes-1.0.5.md#code-)
* [Test Reports](release-notes-1.0.5.md#test-reports-)
  * [1. In scope](release-notes-1.0.5.md#1-in-scope-)
  * [2. Not in scope](release-notes-1.0.5.md#2-Not-in-scope-)
  * [3. Executive Summary – Consolidated Quality Status](release-notes-1.0.5.md#3-executive-summary--consolidated-quality-status-)
  * [4. Types of Testing](release-notes-1.0.5.md#4-types-of-testing-)
  * [5. Test Execution Summary](release-notes-1.0.5.md#5-test-execution-summary-)
* [Known Issues](release-notes-1.0.5.md#known-issues-)
* [List Of Acronyms](release-notes-1.0.5.md#list-of-acronyms-)

## Scope [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

This release is with **real biometrics**. This means that MOSIP Platform is now integrated with SDK, MDS \(MOSIP Device Service\), ABIS \(Automated Biometrics Identification System\) and Biometric devices. Also, this version is tested for Biometric functionalities. Non-functional requirements \(Performance, Scale and Security\) will be taken up in subsequent releases.

* Modules included
  * Pre-Registration
  * Registration Client
  * Registration Processor
  * Authentication 
  * Administration
  * Reference GUI implementation of Pre-Registration, Registration Client and Administration
* Modules not included
  * Partner Management
  * Resident Services
* IAM - The Identity and Access Management\(IAM\) had been changed from custom implementation to Keycloak. 

Module-wise features released as part of this release can be found [here](https://github.com/nayakrounak/documentation/tree/4f2723f5f3c02a9b74329ac70a3d7bf39914858e/docs/_files/release/1.0.5/MOSIP_Feature_Release_v1.0.5.xlsx)

## Documentation [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

### 1. Platform Documentation

Includes Functional requirements, Process flows, Architecture and High level design, Getting started and Deployment guide, Developer documentation etc. Please find the [link to Platform Documentation](https://docs.mosip.io/platform/).

### 2. Detailed Documentation

Low level design documents for respective modules is found below:

* [Pre-Registration](https://github.com/mosip/pre-registration/tree/master/design/pre-registration)
* [Registration Client](https://github.com/mosip/registration/tree/master/design/registration)
* [Registration Processor](https://github.com/mosip/registration/tree/master/design/registration-processor)
* [Authentication](https://github.com/mosip/id-authentication/tree/master/design/authentication)
* [Administration](https://github.com/mosip/admin-services/tree/master/design/admin)
* [ID Repository](https://github.com/mosip/commons/tree/master/design/kernel)
* [Kernel](https://github.com/mosip/commons/tree/master/design/idrepository)

### 3. Platform Configuration for RBR

MOSIP Platform can be configured to be used for Real Biometrics. Please find the [guide to configure MOSIP for biometrics](../modules/registration-client/guide-to-configure-mosip-for-biometrics.md).

## Key Points [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

| Key Points | Details |
| :--- | :--- |
| Pre Registration - Browser support | Chrome 74.0.3729 |
| Deployment Script Environment | Microsoft Azure |
| Registration Client – OS version | Windows 10 \(English version\)  with TPM 2.0 |
| Camera | Logitech / Default windows camera |
| Scanner | Canon lide 120 |
| GPS | GlobalSat BU-353-S4 |
| Biometrics standard | CBEFF format \(Version - 0.9.0\) |
| MOSIP Device Service \(MDS\) | Version - 0.9.1 |
| SMS gateway | MSG91, Infobip |
| Registration Client – face capture | OpenImaj - This is licensed for demo purpose only |
| Keystore | SoftHSM |
| Antivirus | ClamAV |
| Maps | OpenstreetMap |
| Supporting key based digital signatures, not using digital certificates |  |
| Transliteration | ICU4J \(Library with French, Arabic languages\) |

## Code [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

The code and [automation tests](https://github.com/mosip/mosip-functional-tests/tree/1.0.5) are available on [GitHub](https://github.com/mosip/). The code needs to be built and deployed as per the procedure documented in [**Building And Deploying MOSIP**](../build-and-deploy/build-and-deploy.md). We will actively support System Integrators during their first deployment.

## Test Reports [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

#### 1. In scope [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Title</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Modules Tested</td>
      <td style="text-align:left">
        <p>Pre-registration (UI &amp; Server)</p>
        <p>Registration Client (UI &amp; APIs)</p>
        <p>Kernel (APIs)</p>
        <p>Registration Processor (Server)</p>
        <p>ID Authentication (APIs)</p>
        <p>ID Repo (APIs)</p>
        <p>Administration (UI &amp; APIs)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Version Tag Tested</td>
      <td style="text-align:left">1.0.5</td>
    </tr>
    <tr>
      <td style="text-align:left">Test Methodology</td>
      <td style="text-align:left">
        <p>Manual</p>
        <p>Test Automation</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Types of testing</td>
      <td style="text-align:left">
        <p>Smoke</p>
        <p>Functional</p>
        <p>Integration</p>
        <p>Regression</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Testing Levels</td>
      <td style="text-align:left">
        <img src="../.gitbook/assets/image1.jpg" alt="Image" />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Configuration Parameters tested for</td>
      <td style="text-align:left">Refer to properties file at <a href="https://github.com/mosip/mosip-config/tree/1.0.5"><b>Link</b></a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Browser Support</td>
      <td style="text-align:left"><b>Pre-Registration</b> 
      </td>
    </tr>
    <tr>
      <td style="text-align:left">OS Support</td>
      <td style="text-align:left"><b>Registration Client</b> 
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Language Support</td>
      <td style="text-align:left">French, Arabic, English</td>
    </tr>
  </tbody>
</table>

#### 2. Not in scope [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Title</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">NFR Testing</td>
      <td style="text-align:left">
        <p>Scalability Testing</p>
        <p>Performance Testing</p>
        <p>Security Testing</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Configuration Testing</td>
      <td style="text-align:left">
        <p>Testing is done for one set of approved production configuration</p>
        <ul>
          <li>Changing the configuration parameters for various values (boundary values)
            and testing the impact of each such value on the platform code will be
            taken up in subsequent releases.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

#### 3. Executive Summary – Consolidated Quality Status [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

| Sl. No. | Module / Activity | Test Methodology | Test Status |
| :--- | :--- | :--- | :--- |
| 1 | Kernel |  Test Automation | PASS |
| 2 | Pre-Registration |  Test Automation | PASS |
| 3 | Registration Client |  _Tested Manually_     Test Automation | PASS |
| 4 | Registration Processor |  Tested Manually  Test Automation | PASS |
| 5 | ID Authentication |   Test Automation | PASS |
| 6 | ID Repo |  Test Automation | PASS |
| 7 | Pre-Registration to Registration Client integration testing |  Tested Manually | PASS |
| 8 | Registration Client to Registration Processor integration testing |  Tested Manually | PASS |
| 9 | Registration Processor to IDA integration testing |      Tested Manually | PASS |
| 10 | IDA to ID Repo |      Tested Manually | PASS |

#### 4. Types of Testing [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

| Testing Type | Description |
| :--- | :--- |
| Smoke Testing | Tests to ensure basic work flows work fine |
| Functional Testing | Tests to ensure functionality of each module and overall system work fine in accordance with the given requirements |
| Integration Testing | Tests to ensure the inter module functionality works fine and in accordance with the integration requirements |
| Regression Testing | Tests to ensure that any change doesn't break existing functionality |

#### 5. Test Execution Summary [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

![](../.gitbook/assets/ExecutionSummary_1.0.5.jpg)

## Known Issues [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

![](../.gitbook/assets/KnownIssues_1.0.5.jpg)

## List Of Acronyms [**\[↑\]**](release-notes-1.0.5.md#table-of-contents)

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

