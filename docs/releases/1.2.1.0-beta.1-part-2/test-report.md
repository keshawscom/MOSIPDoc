# Test Report

## Testing Scope

The scope of testing is to verify fitment to the specification from the perspective of&#x20;

●     Functionality&#x20;

●     Deployability&#x20;

●     Configurability&#x20;

●     Customizability

Verification is performed from the end user perspective and the System Integrator (SI) point of view. Hence Configurability and Extensibility of the software are also assessed. This ensures the readiness of software for use in multiple countries. Since MOSIP is an “API First” product platform, the Verification scope required comprehensive automation testing for all the MOSIP APIs. An automation Test Rig is created for the same.

## Test Approach

Persona based approach has been adopted to perform the IV\&V, by simulating test scenarios that resemble a real-time implementation.

A Persona is a fictional character/user profile created to represent a user type that might use a product/or a service in a similar way. Persona based testing is a software testing technique that puts software testers in the customer's shoes, assesses their needs from the software, and thereby determines use cases/scenarios that the customers will execute. The persona's needs may be addressed through any of the following.

●     Functionality&#x20;

●     Deployability&#x20;

●     Configurability&#x20;

●     Customizability

The verification methods may differ based on how the need was addressed.

For regression check, “MOSIP Test Rig” - an automation testing suite - is indigenously designed and developed for supporting persona based testing. MOSIP Test Rig covers the end to end test execution and reporting. The end to end functional test scenarios are written starting from pre-registration, to the creation of the packet in the registration center, processing the packet through the registration process, generating UIN, and authenticating identity using IDA through various permutations and combinations of cases being covered. MOSIP Test Rig will be an open source artifact that can also be enhanced and used by countries to validate the SI deliveries before going live. Persona classes include both negative and positive personas. Negative persona classes include users like Bribed Registration Office, Malicious Insider, etc. The needs of positive persona classes must be met, whereas the needs of negative persona classes must be effectively restricted by the software.

## Verified configuration

Verification is performed on various configurations as mentioned below

Default configuration - with 6 Languages (English/Arabic/French/Hindi/Tamil/Kannada)

Main feature tested:

▪         Admin

▪         Pre-Registration

▪         Registration Client

▪         Registration Processor

## Test execution statistics

### Functional test results

Below are the test metrics by performing functional testing using mock MDS, mock Auth, and mock ABIS. The process followed was black box testing which based its test cases on the specifications of the software component under test. The functional test was performed in combination with individual module testing as well as integration testing. Test data were prepared in line with the user stories. Expected results were monitored by examining the user interface. The coverage includes GUI testing, System testing, End-To-End flows across multiple languages and configurations. The testing cycle included the simulation of multiple identity schema and respective UI schema configurations.

#### API Based Testing:

| **Module**         | **Total** | **Passed** | **Failed** | **Skipped** |
| ------------------ | --------- | ---------- | ---------- | ----------- |
| Master Data (Eng.) | 937       | 933        | 4          | 0           |
| PreReg             | 281       | 271        | 10         | 0           |
|                    | **1218**  | **1204**   | **14**     | 0           |

#### UI Based Testing:

| **Module**     | **Total** | **Passed** | **Failed** | **Skipped** |
| -------------- | --------- | ---------- | ---------- | ----------- |
| Admin UI       | 16        | 15         | 1          | 0           |
| Reg. Client UI | 32        | 28         | 4          | 0           |
|                | **48**    | **43**     | **5**      | 0           |

#### DSL - End-to-end scenarios results:

| **Total** | **Passed** | **Failed** | **Skipped** |
| --------- | ---------- | ---------- | ----------- |
| 177       | 142        | 35         | 0           |

### Detailed Test metrics

Below are the detailed test metrics for manual/automation testing. The project metrics are derived from Defect density, Test coverage, Test execution coverage, test tracking, and efficiency.

The various metrics that assist in test tracking and efficiency are as follows:

●   Passed Test Cases Coverage: This measures the percentage of passed test cases. (Number of passed tests / Total number of tests executed) x 100

●    Failed Test Case Coverage: It measures the percentage of all the failed test cases. (Number of failed tests / Total number of test cases executed) x 100

API Test rig reports were generated by the below sha id for mosipqa/automationtests:1.3.x image:

```
sha256:ea4fd28e6e01552ebbd2842875a257294e80fd83b1060bc3578a7636ce2fcb44
```
