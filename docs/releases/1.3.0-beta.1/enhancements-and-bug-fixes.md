# Enhancements and bug fixes

### **Enhancements**

1. ([MOSIP-26804](https://mosip.atlassian.net/browse/MOSIP-26804)) **Data Segregation:** MOSIP data which was considered to be master data have been categorized into default data and seed data. Default data refers to data that are mandatory to proceed with the deployment of MOSIP. Seed data refers to the data that are not mandatory during the deployment but are required for the functionality. this data will be fed by the countries based on their requirement. In this release, the categorization of the data performed and CSV files related to default data have been placed along with the source code while the CSV files that are related to seed data have been moved to the mosip-data repo. As part of this process, data that are not required anymore also have been removed. please refer below for the changes:

* Few language specific data which was identified as default data have been moved to the admin repo also modified these tables to be language agnostic. Below is the list of changes made under this category:

```
app_details
authentication_method
biometric_attribute
biometric_type
module_details
process_list
reason_category
```

* **below tables which are placed under admin\_service were deleted as they are not in use anymore in LTS- - 1.2.x**

```
master-admin_param.sql
master-appl_form_type.sql
master-message_list.sql
master-doc_format.sql
master-gender.sql
master-global_param.sql
master-id_type.sql
master-individual_type.sql
master-introducer_type.sql
master-status_list.sql
master-status_type.sql
```

* **The below tables were identified as seed data and hence moved to dml in mosip-data**

```
days_of_week_list
doc_category
registration_center
registration_center_h
template
```

* **removed dml data from mosip\_data as it is present already in the admin repo as default data**

```
app_authentication_method
app_details
app_role_priorityy
authentication_method
biometric_attribute
biometric_type
process_list
module_details
reason_category
role_details
screen_authorization
screen_details
template_file_format
template_type
blacklisted_words
sync_job_def
```

To modify all the tables as mentioned above the user needs to execute the SQL script given [here](https://github.com/mosip/admin-services/blob/release-1.3.x/db_scripts/mosip_master/default_data_cleanup/cleanup.sql).

2. **(**[**MOSIP-33780**](https://mosip.atlassian.net/browse/MOSIP-33780)**) Support for SECP256K1, SECP256R1, and Ed25519 Cryptographic Algorithms**: The system is enhanced to support additional cryptographic algorithms based on Elliptic Curve Cryptography (ECC), specifically SECP256K1, SECP256R1, and Ed25519. These algorithms were integrated into the key management system to enable secure key generation, signing, and verification functionalities. Please refer [here ](https://docs.mosip.io/1.2.0/modules/keymanager)for more details
3. **(**[**MOSIP-21117**](https://mosip.atlassian.net/browse/MOSIP-21117)**) Codebase Enhancements with Java 21 for released repos:** This release introduces extensive enhancements to align the codebase with the latest features, optimizations, and requirements of Java 21. These updates ensure seamless compatibility, improved functionality, and optimized performance with the new Java version. As a part of Java migration, the Spring boot version also got updated. Here on, the platform will support the Spring boot **v3.2.3.**

Refer to the below repos that are released with JAVA 21&#x20;

* admin-services
* audit-manager
* otp manager
* print
* websub
* biosdk-client
* biosdk-services
* nfiq
* mosip-config
* registration
* mosip-openid-bridge
* captcha
* digital-card-service
* admin-ui
* packet-manager
* reg-client
* mosip-ref-impl

4. ([#MOSIP-34253](https://mosip.atlassian.net/browse/MOSIP-34253)) **Standalone Data Share Service:** enhanced the system's ability to run the data share as a standalone service, eliminating the dependency on the Partner Management Service and Key Manager Service. In this mode, the data share process is simplified: INJI will trigger the Durian service with a profile configured for standalone mode. When enabled, static values for **policyid**, **subscriberid**, and **transactions allowed** will be picked from a configuration file. Durian will then generate a datashareURL based on these static values, which will be shared with INJI for further use. This enhancement ensures that data sharing can proceed independently of the default setup, streamlining the process for specific use cases. The data is stored as plain text, with a unique resource location per VC, ensuring persistence without automatic purging. This feature is to support the request from Inji Stack only
5.  **Code Enhancement: Updates in Artifactory and MOSIP Configuration for Java Migration**

    As part of the Java migration efforts, several updates have been made to the Artifactory and MOSIP configurations to align with Java 21. Key changes include:

    * **HSM Client Updates**: The HSM client file in Artifactory has been updated to support Java 21.
    * **Kernel Transliteration Dependency**: The kernel-transliteration dependency has been moved to the pom.xml file to centralize commonly used files within a centralized repository.
    * **New JAR Files Added**:
      * registration-api-stub-impl.jar
      * image-compressor-jar-with-dependencies.jar
      * redis-cache-provider.jar
    * **ChildAuthFilter Refactor**: The childAuthFilter JAR file has been removed from Artifacory. Related code snippets have been moved to ID Repo to eliminate Artifactory dependency in the ID Repo module.
    * **Multilingual Support**: To enhance multilingual capabilities and support data segregation, the i18n bundle has been introduced for **Admin**, **PMS**, and **Pre-registration** modules.

    These enhancements aim to streamline dependencies, optimize configuration management, and improve system functionality.

### **Bug Fixes**

| Jira id                                                       | Issue description                                                                                                                                                                                                                                                |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [MOSIP-32283](https://mosip.atlassian.net/browse/MOSIP-32283) | Fixed an issue where zero-byte packets were being uploaded to the landing zone bucket when configured as an object store.                                                                                                                                        |
| [MOSIP-20535](https://mosip.atlassian.net/browse/MOSIP-20535) | Fixed an issue where the Name and Description fields in Dynamic Fields could not be edited if filled and focus was moved to the next field before creation.                                                                                                      |
| [MOSIP-21585](https://mosip.atlassian.net/browse/MOSIP-21585) | Fixed a technical error that occurred when clicking on the "Document Category - Type Mapping" feature in the Admin UI.                                                                                                                                           |
| [MOSIP-30261](https://mosip.atlassian.net/browse/MOSIP-30261) | Fixed an issue in the PMP portal where partner policies were not reflecting correctly after user creation, requiring manual database updates. This was observed during ABIS and Print partner onboarding.                                                        |
| [MOSIP-23873](https://mosip.atlassian.net/browse/MOSIP-23873) |  Fixed an issue in the center creation page where the location hierarchy was not functioning correctly. Changes were made to clear lower location hierarchy field values when the higher location hierarchy (Province) value was changed, resolving the problem. |
