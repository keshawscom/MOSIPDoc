# 1.2.0.2

**Release Version: 1.2.0.2**

**Release Date: Coming soon**

### **Overview**

This release launches an enhancement in the Registration Processor to support the [Custom Handle](https://docs.mosip.io/1.2.0/modules/id-repository/custom-handle) feature to be enabled during the new registration process using the Android Registration Client. As part of this release, changes were made in the packet manager, ID repo & registration processor to process packets that contain demographic fields with datatype as an array.

### **Major Highlights**

* Registration
* Packet Manager
* ID Repository

### **New Features**

* **Supporting Array DataType in packet processing** :\
  The handle attribute is passed as an array datatype in the packet during packet creation with the custom handle feature enabled. This change has modified the registration processor and packet manager to handle both string and array values.&#x20;

### **Bug Fixes**

* **Unable to authenticate using handles:**\
  Fix was provided through this release by introducing a new endpoint in ID Repository which will retrieve the identity based on handle and idtype.

### **Repository Released**

| Repositories            | Tag version                                                       |
| ----------------------- | ----------------------------------------------------------------- |
| mosip-config            | [v1.2.3.0](https://github.com/mosip/mosip-config/tree/v1.2.3.0)   |
| id-repository           | [v1.2.2.0](https://github.com/mosip/id-repository/tree/v1.2.2.0)  |
| packet-manager          | [v1.2.0.2](https://github.com/mosip/packet-manager/tree/v1.2.0.2) |
| registration            | [v1.2.0.2](https://github.com/mosip/registration/tree/v1.2.0.2)   |
| bio-utils/biometric-api | [v1.2.03](https://github.com/mosip/bio-utils/tree/v1.2.0.3)       |

### **Compatible Modules**

The following table outlines the tested and certified compatibility of [**1.2.0.1**](../release-notes-1.2.0.1/) with other modules.

| Module    | Version               |
| --------- | --------------------- |
|  Platform |    1.2.0.1 B3 version |

### Documentation

* Functional test reports (link to be updated)&#x20;
* [Known Issues](https://mosip.atlassian.net/issues/?jql=labels%20%3D%20%22known-issue-1.2.0.2%22)\
