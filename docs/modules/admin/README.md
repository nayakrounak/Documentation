# Administration

## Overview

The MOSIP platform is configured via the Admin application. This application can be accessed only by the privileged group of administration personnel. When the MOSIP platform gets initialized, there are default configurations and seed data are setup. Post installation, following operations can be done using the Admin application:

* Configuration entry changes 
* Master data management
* User management 
* Mapping of the master data to various resources

The module provides a single user interface to administer the MOSIP platform. On initial platform installation, data and configurations may be uploaded from CSV files.

Admin application contains UI layer and Service layer. All the components in both Services and UI are secure and authenticated. Every component should be defined with the authorization module plugged in. For example, if a component's data is not supposed to be viewed except authorized personnel, no user will be able to view it. So is for creating, editing and deleting functionalities.

## Detailed functionality

[Admin Services Functionality](admin-services-functionality.md)

## Logical view

![Logical Diagram](../../.gitbook/assets/admin_logical_diagram.jpg)

## Backend Services

The administrator uses many services available as part of Kernel in [commons repository](https://github.com/mosip/commons). There are a few administrator specific services available in [admin repository](https://github.com/mosip/admin-services). The code and design documentation is available in the repositories.

## Frontend - Admin portal

Reference implementation of Admin portal is available in [ref impl repo](https://github.com/mosip/mosip-ref-impl)

## Build and Deploy

Build and deploy instructions available in the above repositories.

## APIs

APIs from multiple services are used for Admin as follows:

* [Admin APIs](../../apis/admin-apis.md) 
* [Document APIs](../../apis/document-apis.md)
* [Register Center APIs](../../apis/registration-center-apis.md)
* [Device APIs](../../apis/device-apis.md)
* [Machine APIs](../../apis/machine-apis.md)
* [Common APIs](../../apis/common-apis.md)
* [Zone APIs](../../apis/zone-apis.md) 
* [Device Management APIs](../../apis/device-management-apis.md)

