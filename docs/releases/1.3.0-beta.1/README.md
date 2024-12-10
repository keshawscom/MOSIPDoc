# 1.3.0-beta.1

**Release Version**: 1.3.0-beta.1

**Release Type:** Beta Release

**Release Date**: Coming Soon

### **Overview**

This beta release introduces significant enhancements, including migration to Java 21 for improved compatibility and performance, the categorization of MOSIP data into default and seed data for streamlined deployment and customization and support for new cryptographic algorithms (SECP256K1, SECP256R1, and Ed25519) to strengthen security.

Additionally, transitioning from the landing zone folder to the MinIO object store addresses scalability and storage challenges, ensuring efficient data handling.

This release is tested and supports eSignet 1.3.0.

For users who have already deployed MOSIP and intend to upgrade to Java 21, please refer [here ](https://mosip.atlassian.net/wiki/spaces/MD/pages/1269760001)for a detailed, step-by-step process to ensure a seamless transition.

{% hint style="info" %}
**Note:**

* As the Inji stack continues to evolve, we are introducing the inji-config repository to manage the Spring Cloud configuration for the stack. You can find the inji-config repository [here](https://github.com/mosip/inji-config).
* Inji Wallet and Inji Web use Mimoto as their backend service. Since Mimoto is part of the Inji stack, its configuration properties have been moved to the inji-config repository. These properties can now be accessed to deploy the Inji stack.
{% endhint %}

As part of the Java 21 migration in this beta release, users must follow specific steps to migrate Artifactory and MOSIP configuration files. Before proceeding with the migration, ensure that two separate Artifactory servers are running:

1. **Java 11 Artifactory Server**: This is for repositories not yet compatible with Java 21 in this beta release.
2. **Java 21 Artifactory Server**: For repositories that support Java 21.

This setup ensures compatibility and seamless operation of Java 11 and Java 21-supported repositories. Any latest Java 11-compatible Artifactory server can be used for this purpose.

{% hint style="info" %}
**Note:** As we approach the MOSIP platform v1.2.1.0-beta.1 release, the v1.3.0-beta.1 is also part of the main MOSIP platform release.
{% endhint %}

#### **Major Areas of Work**

* Code Migration from JAVA 11 to JAVA 21
* Enabling Digital Signature with ECC Algorithm in Key Manager
* Data Segregation to Default, Seed, and Test
* Functional bug fixes
* Security bug fixes
* DSL Automation

#### **Repository Released**

<table><thead><tr><th width="374">Repositories</th><th>Tags Released</th></tr></thead><tbody><tr><td>bio-utils</td><td> To be updated</td></tr><tr><td>commons</td><td> To be updated</td></tr><tr><td>mosip-openid-bridge</td><td> To be updated</td></tr><tr><td>biosdk-client</td><td> To be updated</td></tr><tr><td>biosdk-services</td><td> To be updated</td></tr><tr><td>audit-manager</td><td> To be updated</td></tr><tr><td>keymanager</td><td> To be updated</td></tr><tr><td>khazana</td><td> To be updated</td></tr><tr><td>packet-manager</td><td> To be updated</td></tr><tr><td>admin-services</td><td> To be updated</td></tr><tr><td>registration</td><td> To be updated</td></tr><tr><td>registration-client</td><td> To be updated</td></tr><tr><td>print</td><td> To be updated</td></tr><tr><td>websub</td><td> To be updated</td></tr><tr><td>durian</td><td> To be updated</td></tr><tr><td>mosip-config</td><td> To be updated</td></tr><tr><td>mosip-functional-tests</td><td> To be updated</td></tr><tr><td>converters</td><td> To be updated</td></tr><tr><td>keycloak</td><td> To be updated</td></tr><tr><td>reporting</td><td> To be updated</td></tr><tr><td>mosip-ref-impl</td><td> To be updated</td></tr><tr><td>artifactory-ref-impl</td><td> To be updated</td></tr><tr><td>mosip/mock-smtp-sms</td><td> To be updated</td></tr><tr><td>mosip-helm</td><td> To be updated</td></tr><tr><td>mosip-infra</td><td> To be updated</td></tr><tr><td>K8s-infra</td><td> To be updated</td></tr></tbody></table>

#### **Documents for reference**

* For module wise Enhancements & Bug fixes please refer [here](https://docs.mosip.io/1.2.0/releases/1.3.0-beta.1/enhancements-and-bug-fixes).
* Functional test report&#x20;
* For Known issues. Please refer [here](https://mosip.atlassian.net/issues/?filter=11674).
