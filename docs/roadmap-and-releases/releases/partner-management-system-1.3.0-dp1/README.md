# Partner Management System 1.3.0-dp.1

## Releases : 1.3.0-dp.1

**Release Name**: Partner Management System Revamp

**Release Number**: v1.3.0-dp.1

**Release Type**:**:** Developer Preview Release

**Release Date**: 3rd Sep, 2024

### Overview

We are excited to announce that Partner Management System (PMS) is undergoing a major revamp and as our first step, we will be introducing a brand new web application - Partner Management Portal to cater to the following aspects:

* Technology stack upgrade
* Introduce new partner types.
* Introduce new features.
* Enhancement of existing features.
* Improved usability and user experience.

This release marks the developer's preview release (1.3.0-dp.1) of Partner Management System which focuses on implementation of **Authentication Partner** workflow **in the new UI.** This version of PMS is designed to run on 1.2.0.1 version of MOSIP platform.

The **key features** of Authentication Partner incorporated in this release are:

* **Partner Certificate:**
  * **Upload and Re-upload:** Easily upload or re-upload Certificate Authority (CA) signed Partner Certificate.
  * **Download:** Download CA signed Partner Certificate and corresponding MOSIP Signed Certificate.
* **Policies:**
  * **Select Policy Group**: Select Policy Group to be able to request for policies
  * **Request Policies:** Request policies within selected policy group.
  * **Policy List:** View a tabular list of requested policies along with Partner Admin approval status.
  * **View Policy Details:** Access detailed views of individual policies, including status of Partner Admin approval/rejection.
* **Authentication Services:**
  * **OIDC Client:**
    * **Create OIDC Client:** Create OIDC Clients for approved policies.
    * **View OIDC Details:** Access a tabular list and individual views of submitted OIDC Client details, including OIDC Client IDs.
    * **Edit:** Edit existing OIDC Client details.
    * **Deactivate:** Deactivate OIDC Client whenever needed.
  * **API Key:**
    * **Generate API Key:** Create API Keys for approved policies.
    * **View API Key Details:** View a tabular list and individual details of submitted API Keys.
    * **Deactivate:** Deactivate API Keys when necessary.
* **Browser Support:**
  * Complete support on **Chrome, Firefox, Edge and Safari** ensures a seamless user experience across these popular browsers.
* **Language Support:**
  * Currently supports English, French and Arabic with plans to incorporate additional languages in future releases.
* **Compatibility:**
  * Optimized for standard browser sizes (laptop/desktop) with responsive UI design for laptop/desktop views.

For detailed description of the above features, refer to [Feature Documentation](../../../id-lifecycle-management/support-systems/partner-management-services/functional-overview/features.md).

**Note:** All other existing services offered by earlier version of Partner Management Portal (Version 1.2.0.2) for roles such as Partner Admin, Device Provider, FTM Chip provider etc will continue to work in the previous UI until our revamp incorporates all these features in upcoming releases.

To know more about the upcoming features planned as part of PMS Revamp for this year, please check out [Roadmap 2024](../../roadmap/roadmap-2024-2025.md).

### **Known Issues**

Below is the list of key [known issues](https://mosip.atlassian.net/issues/?jql=labels%20%3D%20%22known_issue%22%20and%20parent%3DMOSIP-32075%20AND%20affectedversion%20%3D%201.3.0-dp.1%20ORDER%20BY%20cf%5B10039%5D%20ASC%2C%20created%20DESC):

| **Jira Issue**                                                | **Issue Description**                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [MOSIP-34728](https://mosip.atlassian.net/browse/MOSIP-34728) | <p>Error messages are observed when selecting a policy group but only when Authentication Partner is registered with lengthy names, organization names, or usernames.</p><p>This will be resolved once the Keycloak is integrated with PMP in our upcoming releases.</p>                                                                                    |
| [MOSIP-34427](https://mosip.atlassian.net/browse/MOSIP-34427) | <p>On deactivating an API key from one browser , the status still remains 'Activated' on viewing the same API Key details in another browser.</p><p>This is occurring due to caching. Hence user is expected to reload the tabular page of API Keys to see the latest status in View API Key screen.</p>                                                    |
| [MOSIP-34109](https://mosip.atlassian.net/browse/MOSIP-34109) | <p>Length validation of OIDC Client name is not functioning as expected for lengthy names within the given range. This has a dependency with eSignet, where the column size needs to be increased.</p><p>Its suggested that meaningful and reasonable length be utilised for OIDC Client name.</p>                                                          |
| [MOSIP-33627](https://mosip.atlassian.net/browse/MOSIP-33627) | Date and time format in UI will be currently displayed as per user’s browser language settings instead of user’s system settings format.                                                                                                                                                                                                                    |
| [MOSIP-35085](https://mosip.atlassian.net/browse/MOSIP-35085) | <p>An error is thrown when public key in JWK format is entered, due to which unable to submit the details. This is faced only in Safari browser of Macbook.</p><p>As a workaround, the create OIDC Client functionality can be performed across Chrome/ Firefox/ Edge/ Safari in Windows OS or Chrome/ Firefox/ Edge in mac OS, until this is resolved.</p> |
| [MOSIP-34250](https://mosip.atlassian.net/browse/MOSIP-34250) | As the MOSIP Signed Certificate expires only after one year from the time of upload, testing is on hold for MOSIP Signed Certificate Expiry scenario.                                                                                                                                                                                                       |
| [MOSIP-35421](https://mosip.atlassian.net/browse/MOSIP-35421) | Add Installation scripts for each module-wise apitest.                                                                                                                                                                                                                                                                                                      |

For more details on all the open issues, please refer [here](https://mosip.atlassian.net/issues/?filter=11506\&jql=project%20%3D%20MOSIP%20AND%20issuetype%20%3D%20Bug%20AND%20%22Epic%20Link%22%20%3D%20MOSIP-32075%20and%20status%20not%20in%20%28Canceled%2C%20Closed%2C%20Fixed%2C%20Testing%2C%20%22PR%20Raised%22%2C%20Documentation%29%20and%20%22Severity%5BDropdown%5D%22%20in%20%28Blocker%2C%20critical%2C%20Major%2C%20Minor%29%20and%20affectedVersion%3D1.3.0-dp.1)

### **Repositories Released**

<table data-header-hidden><thead><tr><th width="491"></th><th></th></tr></thead><tbody><tr><td><strong>Repository Released</strong></td><td><strong>Tags</strong></td></tr><tr><td>partner-management-services</td><td><a href="https://github.com/mosip/partner-management-services/tree/v1.3.0-dp.1">v1.3.0-dp.1</a></td></tr><tr><td>partner-management-portal</td><td><a href="https://github.com/mosip/partner-management-portal/tree/v1.3.0-dp.1">v1.3.0-dp.1</a></td></tr><tr><td>keymanager</td><td><a href="https://github.com/mosip/keymanager/tree/v1.2.1.0">v1.2.1.0</a></td></tr><tr><td>artifactory-ref-impl</td><td><a href="https://github.com/mosip/artifactory-ref-impl/tree/v1.2.0.3">v1.2.0.3</a></td></tr></tbody></table>

### Compatible Modules

The following table outlines the tested and certified compatibility of PMS 1.3.0-dp.1 with other modules.

<table><thead><tr><th width="472">Module/Repo</th><th>Tags</th></tr></thead><tbody><tr><td>PMS UI (legacy PMS UI for admin activities)</td><td><a href="https://github.com/mosip/partner-management-portal/tree/v1.2.0.1">v1.2.0.1</a></td></tr><tr><td>IDA Auth</td><td><a href="https://github.com/mosip/id-authentication/tree/v1.2.0.1">v1.2.0.1</a></td></tr><tr><td>eSignet</td><td><a href="https://github.com/mosip/esignet/tree/v1.2.0">v1.2.0</a></td></tr><tr><td>Reg Proc</td><td><a href="https://github.com/mosip/registration/tree/v1.2.0.1">v1.2.0.1</a></td></tr><tr><td>Notifier (Kernel)</td><td><a href="https://github.com/mosip/commons/tree/v1.2.0.1-B1/kernel">v1.2.0.1-B1</a></td></tr><tr><td>Audit manager</td><td><a href="https://github.com/mosip/audit-manager/tree/v1.2.0.1-B1">v1.2.0.1-B1</a></td></tr><tr><td>ID Repo</td><td><a href="https://github.com/mosip/id-repository/tree/v1.2.0.1">v1.2.0.1</a></td></tr><tr><td>datashare</td><td><a href="https://github.com/mosip/durian/tree/v1.2.0.1">v1.2.0.1</a></td></tr><tr><td>mosip-pms table</td><td><a href="https://github.com/mosip/mosip-infra/tree/v1.2.0.2/deployment/v3/external/postgres">v1.2.0.2</a></td></tr><tr><td>Keycloak</td><td><a href="https://github.com/mosip/keycloak/tree/v1.2.0.1">v1.2.0.1</a></td></tr><tr><td>minio</td><td><a href="https://github.com/mosip/mosip-infra/tree/v1.2.0.2/deployment/v3/external/object-store">v1.2.0.2</a></td></tr><tr><td>config-server</td><td><a href="https://github.com/mosip/mosip-config/tree/v1.2.0.1">v1.2.0.1</a></td></tr><tr><td>Websub</td><td><a href="https://github.com/mosip/websub/tree/v1.2.0.1-B1">v1.2.0.1-B1</a></td></tr></tbody></table>



### Services

For code and implementation of Partner Management Services, refer [here](https://github.com/mosip/partner-management-services/tree/release-1.3.x).

### Partner Management Portal UI

For code and implementation of Partner Management Portal (revamp) , refer [here](https://github.com/mosip/partner-management-portal/tree/release-1.3.x).

To get started with the new interface of Partner Management Portal, refer to the [Partner Management Portal End User Guide](../../../id-lifecycle-management/support-systems/partner-management-services/functional-overview/end-user-guide.md).

### Build and Deploy

To access the build and read through the deployment instructions, refer to the [Partner Management Services Deployment Guide](../../../id-lifecycle-management/support-systems/partner-management-services/develop/technical-overview/build-and-development-guide.md).

**Note**: The deployment script for the PMS module-wise test rig will be addressed in the next release. Meanwhile, users who wish to run automation tests can refer to the [documentation](https://github.com/mosip/mosip-infra/tree/v1.2.0.2/deployment/v3/testrig) and deploy using the image `mosipid/apitest-pms:1.3.0-dp.1` .

### Configurations

For details related to partner management services revamp configurations, refer to the [PMS Revamp Configuration Guide](../../../id-lifecycle-management/support-systems/partner-management-services/develop/technical-overview/pms-configuration-guide.md)

### Developers Guide

For a detailed description of Partner Management System, code, design, and setup steps, refer to:

1. [UI Developer’s Guide](../../../id-lifecycle-management/support-systems/partner-management-services/develop/technical-overview/ui-developers-guide.md)
2. [Backend Developer’s Guide](../../../id-lifecycle-management/support-systems/partner-management-services/develop/technical-overview/backend-developers-guide.md)

### API

Refer [API Documentation](https://mosip.stoplight.io/docs/partner-management-portal-revamp).

### Test Report

For details on the test results, refer [here](test-report.md).

## Other Documentation

* [Technology Stack](../../../id-lifecycle-management/support-systems/partner-management-services/develop/technical-overview/technology-stack.md)
* [Browsers Supported](../../../id-lifecycle-management/support-systems/partner-management-services/develop/technical-overview/browsers-supported.md)
