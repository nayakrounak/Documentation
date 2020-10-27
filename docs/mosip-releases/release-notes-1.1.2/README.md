# Release Notes 1.1.2

## Table Of Contents

* [Scope](./#scope)
* [Documentation](./#documentation)
* [Code](./#code)
* [Tests](./#tests)
  * [a. In scope](./#a-in-scope)
  * [b. Not in scope](./#b-not-in-scope)
  * [c. Test Metrics](./#c-test-metrics)
  * [d. Test Execution Report](./#d-test-execution-report)
* [Acronyms](./#acronyms)

## Scope

MOSIP Version **1.1.2** is an interim release on top of **1.1.1** release. It has some of the new features which were planned for release **1.2** and some critical bug fixes which were identified in [Release 1.1.1](../release-notes-1.1.1/#list-of-known-issues).

**Release Date:** October 24, 2020

**Key Highlights**

We have migrated from Java 8 to Java 11 as part of this release and also incorporated some software infrastructure changes as part of paring the technical debt.

* [New features added to MOSIP are listed here](release-notes-1.1.2-features.md)
* [All the bug fixes are listed here](release-notes-1.1.2-bug-fixes.md)

## Documentation

### 1. Platform

Includes functional requirements, process flows, architecture and high level design.

[Link to documentation](https://docs.mosip.io/platform/modules).

### 2. APIs

All APIs are documented [here](https://docs.mosip.io/platform/apis).

### 3. Design

Low level design documents for each module are available in the respective github repos.

## Code

* [Commons](https://github.com/mosip/commons/tree/v1.1.2)
* [Pre-registration](https://github.com/mosip/pre-registration/tree/v1.1.2)
* [Registration](https://github.com/mosip/registration/tree/v1.1.2)
* [Authentication](https://github.com/mosip/id-authentication/tree/v1.1.2)
* [Partner Management Services](https://github.com/mosip/partner-management-services/tree/v1.1.2)
* [Resident Services](https://github.com/mosip/resident-services/tree/v1.1.2)
* [Admin Services](https://github.com/mosip/admin-services/tree/v1.1.2)
* [Reference Implementation](https://github.com/mosip/mosip-ref-impl/tree/v1.1.2)

{% hint style="info" %}
Code needs to be deployed as per the procedure depicted in [Sandbox Installer](https://github.com/mosip/mosip-infra/tree/1.1.2/deployment/sandbox-v2).
{% endhint %}

## Tests

### a. In scope

Basic integration testing was done covering the below modules.

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
        <p>Pre-registration (Dynamic UI &amp; APIs)</p>
        <p>Registration Client (Dynamic UI)</p>
        <p>Kernel (APIs)</p>
        <p>Registration Processor (Server)</p>
        <p>ID Authentication (APIs)</p>
        <p>Partner Management (APIs)</p>
        <p>ID Repository (APIs)</p>
        <p>Resident Services (APIs)</p>
        <p>Admin (UI &amp; APIs)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Configuration Testing</td>
      <td style="text-align:left">Testing is done for default configuration. Changing the configuration
        parameters with various values will be taken up in subsequent releases.</td>
    </tr>
    <tr>
      <td style="text-align:left">Version Tag Tested</td>
      <td style="text-align:left">v1.1.2</td>
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

| Areas | Technology Used |
| :--- | :--- |
| Deployment Script Environment | Microsoft Azure and VMs deployed in on-premise hardware |
| Registration Client with TPM 2.0 | Windows 10 |
| Document Scanner | Canon lide 120 |
| GPS | GlobalSat BU-353-S4 |
| Biometrics Standard | CBEFF format \(Version - 2.0\) |
| MOSIP Device Service \(MDS\) | MDS v0.9.5 |
| ABIS | ABIS Spec Version v0.9 |
| SDK | SDK Spec Version v0.9 |
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
        <p>Performance Testing</p>
        <p>Reliability and Disaster recovery Testing</p>
      </td>
    </tr>
  </tbody>
</table>

### c. Test Metrics

| Key | Value |
| :--- | :--- |
| Test Coverage | Pre-Registration \(80%\), Registration Client \(95%\), Registration Processor \(100%\), Authentication \(100%\), Partner Management \(100%\), Resident Services \(100%\), Admin \(100%\) |
| Code Coverage | 70% to 80% |
| Automation Coverage | 80% |
| Number of Test Cases | Total Run \(2804\), Pass \(2332\), Pass Rate \(83.17%\) |
| Number of Open Blocker or Critical Defects | 0 |

### d. Test Execution Report

| Test Execution | Version | Test Cases | Executed Tests | Pass | Fail | Pending Execution | Pass% | Fail% |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Kernel | 1.1.2 | 344 | 344 | 322 | 22 | 0 | 93.6% | 6.4% |
| Registration | 1.1.2 | 121 | 121 | 103 | 18 | 0 | 85.1% | 14.9% |
| Admin | 1.1.2 | 894 | 894 | 887 | 7 | 0 | 99.2% | 0.8% |
| Authnetication | 1.1.2 | 1055 | 1055 | 693 | 362 | 0 | 65.7% | 34.3% |
| ID Repository | 1.1.2 | 147 | 147 | 147 | 0 | 0 | 100% | 0.0% |
| Resident Services | 1.1.2 | 178 | 178 | 115 | 63 | 0 | 64.6% | 35.4% |
| Partner Management | 1.1.2 | 65 | 65 | 65 | 0 | 0 | 100% | 0.0% |
| **Total** | 1.1.2 | 2804 | 2804 | 2332 | 472 | 0 | 83.2% | 16.8% |

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

