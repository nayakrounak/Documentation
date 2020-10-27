# Release Notes 1.1.0

## Table Of Contents

* [Scope](./#scope)
* [Documentation](./#documentation)
* [Key Points](./#key-points)
* [Code](./#code)
* [Tests](./#tests)
  * [a. In scope](./#a-in-scope)
  * [b. Not in scope](./#b-not-in-scope)
  * [c. Test Metrics](./#c-test-metrics)
  * [d. Test Execution Report](./#d-test-execution-report)
* [List of Known Issues](./#list-of-known-issues)
* [Acronyms](./#acronyms)

## Scope

MOSIP Version **1.1.0** has several enhancements. It has additional security features and is performance-tuned and feature-rich.

**Release Date:** July 03, 2020

**Key Highlights**

* Includes Partner Management
* [New features added to MOSIP platform](release-notes-1.1.0-features.md)
* [Bug Fixes across all modules](release-notes-1.1.0-bug-fixes.md)
* Engineering Changes
  * Automated deployment scripts based on docker, ansible and kubernetes.
  * Open build process using Travis and Github Actions.
  * Git commit-ids in builds helps in traceability from binary to code.
  * Built docker images are published into Maven and docker hub.
  * Documentation now uses Gitbook \(docs.mosip.io\)
* Technology Changes
  * ApacheDS has been replaced with Keycloak for secure identity and access management.
  * Prometheus end points for all MOSIP services for health monitoring
  * Network HSM for strong security and data protection

## Documentation

### 1. Platform

Includes functional requirements, process flows, architecture and high level design.

[Link to documentation](https://docs.mosip.io/platform/modules).

### 2. APIs

All APIs are documented [here](https://docs.mosip.io/platform/apis).

### 3. Design

Low level design documents for each module are available in the respective github repos.

### 4. Code and Automated Tests

* [Commons](https://github.com/mosip/commons/tree/v1.1.0)
* [Pre-registration](https://github.com/mosip/pre-registration/tree/v1.1.0)
* [Registration](https://github.com/mosip/registration/tree/v1.1.0)
* [Authentication](https://github.com/mosip/id-authentication/tree/v1.1.0)
* [Partner Management Services](https://github.com/mosip/partner-management-services/tree/v1.1.0)
* [Resident Services](https://github.com/mosip/resident-services/tree/v1.1.0)
* [Reference Implementation](https://github.com/mosip/mosip-ref-impl/tree/v1.1.0)
* [Automation tests](https://github.com/mosip/mosip-functional-tests/tree/v1.1.0)

The details related to artifactory versions is available [here](release-notes-1.1.0-artifact-version.md).

{% hint style="info" %}
Code needs to be deployed as per the procedure depicted in [Sandbox Installer](https://github.com/mosip/mosip-infra/tree/v1.1.0/deployment/sandbox-v2).
{% endhint %}

## Tests

### a. In scope

<table>
  <thead>
    <tr>
      <th style="text-align:left">Title</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Functional Testing</td>
      <td style="text-align:left">
        <p>Pre-registration (UI &amp; APIs)</p>
        <p>Registration Client</p>
        <p>Kernel (APIs)</p>
        <p>Registration Processor (Server)</p>
        <p>ID Authentication (APIs)</p>
        <p>Partner Management (APIs)</p>
        <p>ID Repo (APIs)</p>
        <p>Resident Services (APIs)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Non-Functional Testing</td>
      <td style="text-align:left">
        <p>Early Performance Testing</p>
        <p>Security Testing</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Configuration Testing</td>
      <td style="text-align:left">Testing is done for default configuration. Changing the configuration
        parameters with various values will be taken up in subsequent releases.</td>
    </tr>
    <tr>
      <td style="text-align:left">Version Tag Tested</td>
      <td style="text-align:left">v1.1.0</td>
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
      <td style="text-align:left">Browser Support</td>
      <td style="text-align:left"><b>Pre-Registration</b> (Latest Versions of Chrome, Edge &amp; Firefox)</td>
    </tr>
    <tr>
      <td style="text-align:left">OS Support</td>
      <td style="text-align:left"><b>Registration Client</b> (Windows 10)</td>
    </tr>
  </tbody>
</table>

| Areas | Technology used |
| :--- | :--- |
| Deployment Script Environment | Microsoft Azure and VMs deployed in on-premise hardware |
| Registration Client with TPM 2.0 | Windows 10 |
| Document Scanner | Canon lide 120 |
| GPS | GlobalSat BU-353-S4 |
| Biometrics Standard | CBEFF format \(Version - 2.0\) |
| MOSIP Device Service \(MDS\) | MDS v0.9.5 |
| ABIS | ABIS Spec Version v0.9 |
| SDK | SDK Spec Version v0.9 |
| SMS gateway | MSG91, Infobip |
| Registration Client – face capture | OpenImaj - This is licensed for demo purpose only |
| Keystore | SoftHSM |
| Antivirus | ClamAV |
| Maps | OpenstreetMap |
| Supporting key based digital signatures, not using digital certificates |  |
| Transliteration | ICU4J \(Library with French, Arabic languages\) |

### b. Not in scope

<table>
  <thead>
    <tr>
      <th style="text-align:left">Title</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Non-Functional Testing</td>
      <td style="text-align:left">
        <p>Detailed Performance Testing</p>
        <p>Reliability and Disaster recovery Testing</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Admin</td>
      <td style="text-align:left">
        <p>Admin UI</p>
        <p>Admin APIs</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UI</td>
      <td style="text-align:left">Dynamic UI</td>
    </tr>
  </tbody>
</table>

### c. Test Metrics

| Key | Value |
| :--- | :--- |
| Test Coverage | Pre-Registration \(100%\), Registration Client \(95%\), Registration Processor \(100%\), Authentication \(100%\), Partner Management \(100%\), Resident Services \(100%\) |
| Code Coverage | 70% to 80% |
| Automation Coverage | 80% |
| Number of Test Cases | Total Run \(2818\), Pass \(2526\), Pass Rate \(90%\) |
| Number of Bugs Found | 797 \(Since December 2019\) |
| Number of Open Defects | Total \(77\), Blocker or Critical: 10 \(7 fixed & 3 open for patch release\) |
| Number of Immediate Fixes | 10 to 15 |

### d. Test Execution Report

| Test Execution | Version | Test Cases | Executed Tests | Pass | Fail | Pending Execution | Pass% | Fail% |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Kernel | 1.0.10 | 372 | 372 | 341 | 31 | 0 | 91.7% | 8.3% |
| Pre-Registration | 1.0.10 | 829 | 802 | 774 | 28 | 27 | 96.5% | 3.5% |
| Registration | 1.0.10 | 316 | 271 | 263 | 8 | 45 | 97.0% | 3.0% |
| Authnetication | 1.0.10 | 1081 | 1081 | 1033 | 48 | 0 | 95.6% | 4.4% |
| ID Repository | 1.0.10 | 152 | 152 | 142 | 10 | 0 | 93.4% | 6.6% |
| Resident Services | 1.0.10 | 38 | 33 | 33 | 0 | 5 | 100% | 0.0% |
| Partner Management | 1.0.10 | 84 | 84 | 84 | 0 | 0 | 100% | 0.0% |
| **Total** | 1.0.10 | 2872 | 2795 | 2670 | 125 | 77 | 95.5% | 4.5% |

## List of Known Issues

| JIRA ID | Module | Description |
| :--- | :--- | :--- |
| MOSIP-7999 | Pre-registration | Notification is not sent when an booked appointment is canceled |
| MOSIP-29972 | Pre-registration | Application Allows to send multiple otp for a single user |
| MOSIP-7676 | Pre-registration | User is allowed to discard the application with in 24 hours i.e. the configured time |
| MOSIP-7704 | Pre-registration | On the Pre Registration UI, a page reload results in session time-out discarding the data entered |
| MOSIP-7704 | Pre-registration | User is not able to copy the documents of his/her choice |
| MOSIP-7817 | Pre-registration | Pre-registration application is allowing Cross Origin Resource Sharing \(CORS\) |
| MOSIP-531 | Pre-registration | User is navigated to blank page for center with no slots and date available for center selected |
| MOSIP-7942 | ID Authentication | Device details are not validated against the biomertic type |
| MOSIP-7993 | ID Authentication | Arabic data displayed as junk characters in ekyc response |
| MOSIP-7907 | ID Authentication | Able to do OTP authentication with invalid transaction id |
| MOSIP-7842 | Registration Client | Device details are not stored in Packet |
| MOSIP-7915 | Registration Client | Navigation issues in registration client UI |
| MOSIP-7970 | Registration Client | Able to authenticate with devices registered for 'REGISTRATION' |
| MOSIP-31341 | Registration Client | Streaming of device stays turned on when registration flow is abruptly closed |
| MOSIP-7726 | Registration Client | Operator should not be able to perform any registration activities when Center, User or Machine is In-Active |
| MOSIP-7995 | Registration Client | Registration data is not displayed when supervisor selects the option informed/can't informed |
| MOSIP-7814 | Registration Client | Multiple issues in the contents displayed in the registration  acknowledgement preview page |
| MOSIP-8006 | Registration Client | Unable to go back to username field from password field in the registration client login window |
| MOSIP-275 | Registration Processor | Registration processor stages aren't working properly after restarting the K8 cluster |

## Acronyms

| Achronyms | Full Form |
| :--- | :--- |
| MOSIP | Modular Open Source Identity Platform |
| ABIS | Automated Biometric Identification System |
| API | Application Programming Interface |
| ID | Identity |
| IDA | Identity Authentication |
| NFR | Non-Functional Requirements |
| OTP | One Time Password |
| SDK | Software Development Kit |
| JWT | Java Web Token |
| K8 | Kubernetes |
| UIN | Unique Identification Number |
| VID | Virtual ID |
| CBEFF | Common Biometric Exchange Formats Framework |
| CORS | Cross Origin Resource Sharing |
| HSM | Hardware Security Module |
| TPM | Trusted Platform Module |
| SDK | Software Development Kit |
| MDS | MOSIP Device Service |
| ICU4J | International Components for Unicode for Java |
| WIP | Work In Progress |
| TBD | To Be Determined/Done |

