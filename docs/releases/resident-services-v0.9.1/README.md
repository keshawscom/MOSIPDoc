# Resident Services v0.9.1

**Release version**: v0.9.1

**Release Date**: Coming soon!

## Overview

This is a v0.9.1 release of Resident Services, offering valuable insights into the range of features and functionality. Resident Services is designed to run on the 1.2.0.1 version of the MOSIP platform. Resident Services are the self-services that the residents themselves use via a portal. [Resident Portal](../../modules/resident-services/) is a web-based UI application that provides residents of a country with services related to their Unique Identification Number (UIN). The residents can perform various operations related to their UIN/ VID and can also raise concerns if any through the portal.

The key features provided on the Resident portal are:

1. Avail UIN services using UIN/ VID (through [eSignet](https://docs.esignet.io)):
   * View My History
   * Manage My VID
   * Secure My ID
   * Track My Requests
   * Get Personalised Card
   * Share My Data
   * Update My Data
   * Login and Logout
2. Get Information
   1. Get the list of Registration Centres
   2. Get the list of Supporting Documents
3. Get My UIN (using UIN/ VID/ AID)
4. Verify Email ID and/ or phone number
5. Book an appointment for new enrolment (via the pre-registration portal)
6. Ancillary features
   * Multi-lingual support
   * Get Notifications (email and bell notifications)
   * View profile details of the logged in user (name, photo, and last login details)
   * Responsive UI support

For a quick overview of the design principles and to understand the relationship of Resident Services with other services, please refer to the [Resident Services Overview](https://docs.mosip.io/1.2.0/modules/resident-services#overview) section.

## **Major Highlights/Features** <a href="#id-2.-major-highlights-features" id="id-2.-major-highlights-features"></a>

(To be updated soon)

## Repository Released&#x20;

| Repositories      | Tags Released                                                       |
| ----------------- | ------------------------------------------------------------------- |
| resident-services | [1.2.1.1](https://github.com/mosip/resident-services/tree/v1.2.1.1) |
| resident-ui       | [0.9.1](https://github.com/mosip/resident-ui/tree/v0.9.1)           |
| mosip-config      | [1.2.3.1](https://github.com/mosip/mosip-config/tree/v1.2.3.1)      |
| mosip-data        | [1.2.2.0](https://github.com/mosip/mosip-data/tree/v1.2.2.0)        |
| admin-services    | [1.2.1.1](https://github.com/mosip/admin-services/tree/v1.2.1.1)    |
| postgres-init     | [1.2.0.2](https://github.com/mosip/postgres-init/tree/v1.2.0.2)     |

## **Enhancements**  <a href="#id-3.-enhancements" id="id-3.-enhancements"></a>

(To be updated soon)

## Summary

#### Services

For a detailed description of Resident services, the code, and the design, refer to the [resident services repo](https://github.com/mosip/resident-services/releases/tag/v1.2.1.0).

#### Resident Portal UI

MOSIP provides a reference implementation of the resident portal that can be customized to the country’s needs. The sample implementation is available [here](https://github.com/mosip/resident-ui/releases/tag/v0.9.0).

## Known Issues

#### Complete List

To get the complete list of known bugs please refer here (link to be updated soon)

#### Key Issues

| JIRA Issues                                                   | Issue Description                                                                            |
| ------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| [MOSIP-38771](https://mosip.atlassian.net/browse/MOSIP-38771) | Update my data feature is not working as expected for a few UINs. The issue is intermittent. |
| [MOSIP-35282](https://mosip.atlassian.net/browse/MOSIP-35282) | Video policy transactions allowed are not working as per policy.                             |

## **Compatible Modules** <a href="#id-6.-compatible-modules" id="id-6.-compatible-modules"></a>

The following table outlines the tested and certified compatibility of v0.9.1 with other modules.

| Module                                                          | Versions |
| --------------------------------------------------------------- | -------- |
| mosipid/authentication-service                                  | 1.2.1.0  |
| mosipid/authentication-internal-service                         | 1.2.1.0  |
| mosipid/authentication-otp-service                              | 1.2.1.0  |
| mosipid/credential-service                                      | 1.2.1.0  |
| mosipid/credential-request-generator                            | 1.2.1.0  |
| mosipid/id-repository-identity-service                          | 1.2.1.0  |
| mosipid/id-repository-vid-service                               | 1.2.1.0  |
| mosipid/partner-management-service                              | 1.2.1.0  |
| mosipid/policy-management-service                               | 1.2.1.0  |
| mosipid/kernel-notification-service                             | 1.2.0.1  |
| mosipid/kernel-keymanager-service                               | 1.2.0.1  |
| mosipid/registration-processor-stage-group-7                    | 1.2.0.1  |
| mosipid/registration-processor-common-camel-bridge              | 1.2.0.1  |
| mosipid/registration-processor-stage-group-1                    | 1.2.0.1  |
| mosipid/registration-processor-stage-group-2                    | 1.2.0.1  |
| mosipid/registration-processor-stage-group-3                    | 1.2.0.1  |
| mosipid/registration-processor-stage-group-4                    | 1.2.0.1  |
| mosipid/registration-processor-stage-group-5                    | 1.2.0.1  |
| mosipid/registration-processor-stage-group-6                    | 1.2.0.1  |
| mosipid/registration-processor-stage-group-7                    | 1.2.0.1  |
| mosipid/registration-processor-notification-service             | 1.2.0.1  |
| mosipid/registration-processor-dmz-packet-server                | 1.2.0.1  |
| mosipid/registration-processor-reprocessor                      | 1.2.0.1  |
| mosipid/registration-processor-registration-status-service      | 1.2.0.1  |
| mosipid/registration-processor-registration-transaction-service | 1.2.0.1  |
| mosipid/registration-processor-workflow-manager-service         | 1.2.0.1  |
| mosipid/kernel-auditmanager-service                             | 1.2.0.1  |
| mosipid/kernel-masterdata-service                               | 1.2.1.0  |
| mosipid/admin-service                                           | 1.2.1.0  |
| mosipid/hotlist-service                                         | 1.2.1.0  |
| mosipid/kernel-syncdata-service                                 | 1.2.1.0  |
| mosipid/digital-card-service                                    | 1.2.0.1  |
| mosipid/print                                                   | 1.2.0.1  |
| mosipid/commons-packet-service                                  | 1.2.0.1  |
| mosipid/mosip-artemis-keycloak                                  | 1.2.0.1  |
| mosipid/websub-service                                          | 1.2.0.1  |

## Documentation

* [Resident Services Developers Guide](https://docs.mosip.io/1.2.0/modules/resident-services/resident-services-developer-guide)
* [Resident Services UI Developers Guide](https://docs.mosip.io/1.2.0/modules/resident-services/resident-services-ui-developer-guide)
* [Resident Portal Configuration Guide](https://docs.mosip.io/1.2.0/modules/resident-services/resident-portal-configuration-guide)
* [Resident Services Deployment Guide](https://docs.mosip.io/1.2.0/modules/resident-services/resident-services-deployment-guide)
* [Configuring Resident OIDC Client](https://docs.mosip.io/1.2.0/modules/resident-services/resident-services-configure-resident-oidc-client)
* [Resident Portal User Guide](https://docs.mosip.io/1.2.0/modules/resident-services/resident-portal-user-guide)
* [Functional Overview](https://docs.mosip.io/1.2.0/modules/resident-services/functional-overview)
* [API Documentation](https://mosip.stoplight.io/docs/resident/9a5192571fc51-document)
* [Test Report](test-report.md)
